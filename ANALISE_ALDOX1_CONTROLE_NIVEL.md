# Aldox 1 - Oscilacao de nivel da coluna no passo 115 (Producao)

**Data:** 27/09/2026
**Fontes:** programa `Continuous.L5X` (controlador ALDOX_CA0104, exportado em 27/09/2026 16:58) e
gravacao de tela de 30 s do supervisorio durante a producao a 450 hl/h.

---

## 1. O que o video mostra

A tela do supervisorio atualiza a cada ~6 s, por isso os valores andam "em degraus".

| Tempo | Bomba entrada B421506 (P11) | Valvula AV11 | FCV421501 (saida FC11) | Vazao FT11 | Nivel LT21 (SP 65%) | Bomba saida B421507 (P21) |
|---|---|---|---|---|---|---|
| 0-4 s | ligada | aberta | 23,75 % | 442,6 hl/h | **103,2 %** | 89,0 % |
| 5 s | **desliga** | **fecha** | 30,00 % | 108 -> 11 hl/h | 103,2 % | 100 % |
| 5-18 s | desligada | fechada | 30,00 % | ~11 hl/h | 103,2 % (transmissor saturado) | 100 % |
| 19 s | desligada | abre | 30,00 % | 5 hl/h | 82,9 % | 94,9 % |
| 25 s | religando | aberta | 30,00 % | 281,6 hl/h | **38,3 %** | 60,7 % |

Ou seja: a coluna enche alem do topo do transmissor, a **alimentacao e cortada por completo**, a bomba
de saida continua a 100 % e o nivel despenca de >100 % para 38 % em poucos segundos. Em seguida a
alimentacao volta com tudo e o ciclo recomeca.

Detalhe importante: o nivel caiu ~45 % em ~6 s. A faixa de 0-100 % do LT21 corresponde a um volume
muito pequeno (da ordem de 15-20 s de producao a 450 hl/h). Qualquer diferenca entre a vazao que
entra e a que sai aparece no nivel em segundos.

---

## 2. Como o programa controla a coluna hoje

| Malha | Onde | O que faz | Parametros no L5X |
|---|---|---|---|
| **FC11** - vazao de entrada | `Lad_099` rung 6, `Lad_016` | Controla a FCV421501 para manter FT11 no setpoint (450 hl/h). Nao olha o nivel. | KP 0,2 / KI 1,0 (dependente) / MAXO 38 % |
| **LC21** - nivel da coluna | `Lad_099` rung 24, `Lad_028` rung 11 | Controla a velocidade da **bomba de saida** P21 (`SP_P21 = LC21.OUT`) | KP 1,0 / KI 0,005 1/s (Ti = 200 s) / **BIAS 0** |
| **COLUMN_STOP_FEED** - intertravamento | `Lad_028` rung 13, `Lad_015` rungs 2 e 4 | Se LT21 > 90 % por 5 s (ou chave LS21 atuada): **fecha AV11 e desliga P11** | REG_HIGH_LEVEL_IN_COLUMN1 = 90 %, atraso 5 s |
| Religamento da P11 | `Lad_015` rungs 1 a 3 | P11 e liga/desliga (velocidade fixa), com **retardo de 10 s** (`INLET_P11_S_RETARDO_LIGA`) | - |

A cascata da vazao pelo nivel do tanque pulmao (LC31, `Lad_016` rungs 16 a 19) esta desabilitada (AFI).
Portanto a vazao de entrada e fixa e **so a bomba de saida corrige o nivel**.

---

## 3. Causa do ciclo

1. **A bomba de saida so reage depois que o nivel ja mudou.** A LC21 nao sabe quanta agua esta
   entrando. Com Kp = 1, para a P21 subir 17 % de velocidade (o necessario para ir de ~350 para
   ~450 hl/h) o nivel precisa ficar ~17 % acima do setpoint. O integral, com Ti = 200 s, e lento demais
   para uma coluna que enche em ~15-20 s. Resultado: o nivel passa de 65 % para mais de 90 %.
2. **Ao passar de 90 %, o intertravamento corta a alimentacao inteira** (450 -> 0 hl/h de uma vez). A
   LC21 continua com a P21 a 100 % porque o nivel ainda esta alto. Entao a coluna esvazia em segundos
   e cai muito abaixo de 65 %.
3. **A FC11 dispara enquanto a alimentacao esta parada.** Com vazao zero, a malha de vazao leva a
   saida para o limite (23,75 % -> 30 %). Quando a P11 religa, a valvula esta fora da posicao de
   trabalho e a vazao entra em degrau.
4. Com o nivel baixo, a LC21 reduz a P21 (60 %). A alimentacao volta com vazao cheia, o nivel sobe
   rapido, a P21 nao acompanha, o nivel volta a 90 % e o ciclo reinicia.

O corte por nivel alto e uma protecao e deve continuar existindo. O problema e que a malha de nivel
esta deixando o nivel chegar nele a cada ciclo.

---

## 4. Correcoes propostas

Faca **uma por vez** e acompanhe em trend do RSLogix, que e bem mais rapido que o supervisorio.
Registre `COLUMN_LT21`, `LC21.OUT`, `INLET_FT11`, `FC11.OUT` e `COLUMN_STOP_FEED` com amostragem
de 100-200 ms.

Tags novas a criar (escopo do programa `Continuous`):

| Tag | Tipo | Valor inicial |
|---|---|---|
| `LC21_FF_GAIN` | REAL | 0.0 |
| `FC11_HOLD` | BOOL | - |
| `FC11_OUT_MEM` | REAL | 25.0 |

### 4.1 Feedforward da vazao de entrada na bomba de saida (principal)

A P21 passa a acompanhar diretamente a vazao que entra. O PID so faz o ajuste fino. O membro
`.BIAS` da instrucao PID e somado a saida (feedforward) e respeita os limites MAXO/MINO.

**Nova rung em `Lad_099_Controllers`, imediatamente ANTES da rung 24** (a do `PID(LC21,...)`):

```
CPT(LC21.BIAS,INLET_FT11*LC21_FF_GAIN);
```

Quando a alimentacao para, `INLET_FT11` cai para zero e a P21 desacelera na hora, sem esperar o
nivel despencar.

**Como calcular o ganho:** no L5X exportado, a coluna estava estavel com 360 hl/h e P21 = 69,5 %.
Isso da ~0,19 % por hl/h. Comece com **80 % disso**:

- `LC21_FF_GAIN = 0.15`. A 450 hl/h, o feedforward vale 67,5 % e o integral cobre o restante.

**Para entrar sem tranco:**

1. Coloque a rung com `LC21_FF_GAIN = 0` (sem efeito).
2. Com o Aldox fora de producao, ou com a LC21 em **manual**, escreva `0.15` em `LC21_FF_GAIN`.
3. Volte a LC21 para automatico. A passagem manual -> automatico e bumpless e reacomoda o integral.

Se o feedforward acompanhar bem, ajuste entre 0,15 e 0,19. Se a P21 ficar tremendo com o ruido do
FT11, use um ganho menor ou filtre o `INLET_FT11` antes.

### 4.2 Congelar a FC11 enquanto a alimentacao estiver parada

Evita que a valvula de vazao va para o limite durante o corte e cause um degrau na volta.

**Nova rung em `Lad_099`, ANTES da rung 3:**

```
XIC(M_115_FORWARD_FLOW_PROD)[XIC(COLUMN_STOP_FEED) ,XIO(INLET_P11_S) ]OTE(FC11_HOLD);
```

**Nova rung logo em seguida (memoriza a ultima saida boa):**

```
XIO(FC11_HOLD)XIO(M_FC11_MAN)XIC(INLET_P11_S)GRT(INLET_FT11,100)MOV(FC11.OUT,FC11_OUT_MEM);
```

**Nova rung logo em seguida (durante o corte, segura a valvula na ultima posicao boa):**

```
XIC(FC11_HOLD)XIO(M_FC11_MAN)MOV(FC11_OUT_MEM,FC11.SO);
```

**Alterar a rung 3 existente:**

```
de:   XIC(M_FC11_MAN)OTE(FC11.SWM);
para: [XIC(M_FC11_MAN) ,XIC(FC11_HOLD) ]OTE(FC11.SWM);
```

Com `FC11.SWM` ligado, a PID fica em manual com `OUT = SO`. A rung 25 do `Lad_016` continua
calculando `SP_AV12 = 100 - FC11.OUT` normalmente. Ao religar a P11, a FC11 volta ao automatico sem
tranco, a partir da posicao em que trabalhava.

O `FC11_HOLD` tambem fica ligado durante os 10 s de retardo de partida da P11. Isso e intencional: a
valvula fica parada na posicao certa ate a bomba entrar.

### 4.3 Resintonia da LC21 (so depois de 4.1 funcionando)

Com o feedforward fazendo o grosso, o PID pode ser um pouco mais firme:

| Parametro | Hoje | Sugestao inicial |
|---|---|---|
| `LC21.KP` | 1,0 | 1,5 -> 2,0 |
| `LC21.KI` (1/s) | 0,005 (Ti 200 s) | 0,01 (Ti ~150-200 s com o novo Kp) |
| `LC21.KD` | 0 | 0 (nao usar; o sinal de nivel oscila) |

Suba um degrau de cada vez. Se o nivel comecar a oscilar rapido (periodo de poucos segundos), volte ao
valor anterior. O `DIV(1,LC21_TI,LC21.KI)` da rung 23 esta em AFI, entao o KI e escrito direto no
`LC21.KI`.

---

## 5. Pontos a verificar no campo

1. **Tempo de execucao das PIDs.** As PIDs estao no programa `Continuous` e executam em toda
   varredura, sem temporizador, com `UPD = 0,02 s`. Se esse programa estiver na **tarefa continua**, a
   instrucao PID calcula o integral como se tivessem passado 20 ms, qualquer que seja o tempo real de
   varredura. O KI efetivo fica diferente do configurado e varia com o scan. Confira em *Tasks ->
   Properties -> Monitor* qual e a tarefa e o tempo de scan. Se for continua, o recomendado pela
   Rockwell e condicionar a PID com um TON do mesmo periodo do UPD, ou passar as PIDs para uma tarefa
   periodica. Faca isso antes da resintonia do item 4.3, porque muda a base dos ganhos.
2. **Capacidade da P21 a 450 hl/h.** A 360 hl/h a P21 roda a ~70 %. A 450 hl/h deve precisar de algo
   entre 80 e 90 %. Se, com o nivel estavel, a P21 estiver acima de ~90 %, a bomba esta no limite e
   nao tem folga para corrigir o nivel. Nesse caso, a 450 hl/h o sistema nao se sustenta e e preciso
   ver a frequencia maxima do inversor e as restricoes de descarga (trocador, tanque pulmao).
3. **Rampa do inversor da P21.** Com uma coluna que enche em ~15-20 s, rampas de aceleracao e
   desaceleracao longas (acima de ~5 s) atrasam a correcao e alimentam a oscilacao.
4. **Transmissor LT21 saturando em ~103 %.** Durante ~13 s o nivel ficou "parado" em 103 % com a P21 a
   100 % e sem entrada. A agua estava acima da faixa do transmissor, entao o transbordo real e maior
   do que o supervisorio mostra.
5. **Alarme "Nivel de oxigenio alto"** aparece na tela durante a oscilacao. A desaeracao depende de
   vazao e nivel estaveis na coluna, entao e provavel que ele melhore junto.

---

## 6. Resumo

- **Causa:** o nivel e controlado so pela bomba de saida, com PID lento e sem saber a vazao de
  entrada. O nivel passa de 90 %, o intertravamento corta a alimentacao inteira, a coluna esvazia e o
  ciclo se repete. A FC11 dispara durante o corte e piora a volta.
- **Correcao:** feedforward da vazao de entrada na LC21 (`LC21.BIAS`) e hold da FC11 durante o corte
  de alimentacao. Depois disso, resintonia moderada da LC21.
- **Verificar:** tipo de tarefa e scan das PIDs, folga da P21 a 450 hl/h e rampas do inversor.

---

## 7. Atualizacao 27/09 - trend do RSLogix (100 ms), `test_bits.1` desligado

**Antes da producao** (18:40:10 a 18:41:35): vazao ~40 % de 600 = ~240 hl/h, P21 ~52 %, nivel estavel
em ~65 %. A malha de nivel funciona.

**Passo 115** (a partir de 18:41:35): vazao ~76-78 % = ~455-470 hl/h (acima dos 450 do setpoint). A P21
sobe ate **100 % e fica la**, e mesmo assim o nivel continua subindo ate ~100 %. O `COLUMN_STOP_FEED`
corta a alimentacao, o nivel cai para ~30 %, a alimentacao volta e o ciclo se repete com periodo de
~60 s. Na volta, a FC11 esta no limite (30 %).

**Conclusao:** nas condicoes atuais, a bomba de saida B421507 **a 100 % nao consegue tirar ~450 hl/h
da coluna**. A oscilacao e consequencia desse limite de capacidade. Nenhuma sintonia de PID resolve
isso, porque a saida ja esta no maximo.

**Por que as rungs de teste pioraram:** o corte da alimentacao acontece justamente porque o nivel esta
alto. O feedforward, ao ver a vazao cair a zero, desacelerava a P21. Com isso o nivel ficava mais
tempo acima de 90 % e o corte durava mais. Com a causa agora identificada, as rungs do `test_bits.1`
(feedforward e hold da FC11) devem continuar desligadas.

**Proximos passos:**
1. Teste de producao com `FC11_SP1` = 400 hl/h. Se a P21 estabilizar abaixo de ~90 % e o nivel ficar
   em 65 % sem corte, o diagnostico esta confirmado.
2. Verificar em campo a B421507:
   - frequencia real no inversor com 100 % de referencia (esta chegando na frequencia maxima?);
   - parametro de frequencia maxima e limite de corrente;
   - escala da saida analogica;
   - restricoes na descarga (trocador, filtro, valvulas, pressao do tanque pulmao);
   - cavitacao na succao.
   Se o Aldox ja produziu a 450 hl/h no passado, algo degradou.
3. Depois disso, opcional: logica de override que reduz o setpoint de vazao automaticamente quando a
   P21 fica saturada, para a producao rodar na maior vazao sustentavel sem bater no intertravamento.
