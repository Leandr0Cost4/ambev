# Aldox 1 - Rungs de correcao do controle de nivel da coluna (TESTE)

Todas as rungs novas comecam com `XIC(test_bits.1)`:

- `test_bits.1 = 0`: o programa se comporta exatamente como hoje (a velocidade da P21 e so a saida da
  LC21 e o hold da FC11 nao atua).
- `test_bits.1 = 1`: as correcoes ficam ativas.

`test_bits` e uma tag DINT de escopo do controlador que ja existe. O bit 1 nao e usado em nenhum outro
lugar do programa.

## Arquivos

| Arquivo | Onde importar | Rungs |
|---|---|---|
| `Aldox1_FC11_Hold.L5X` | `Lad_099_Controllers`, **entre a rung 3** `XIC(M_FC11_MAN)OTE(FC11.SWM);` **e a rung 4** | 4 |
| `Aldox1_LC21_Feedforward.L5X` (versao 2) | `Lad_099_Controllers`, **logo DEPOIS da rung do** `PID(LC21,...)` e antes da rung `XIC(M_PB_LC22_MAN)...` | 2 |
| `rungs_texto.txt` | O mesmo texto das rungs, para colar no editor ASCII caso a importacao nao funcione | - |

Os numeros 3, 4 e 24 (PID da LC21) sao do L5X exportado em 27/09/2026. Se o programa mudou, guie-se pelo
conteudo das rungs, nao pelo numero. **A posicao importa:**

- As rungs da FC11 precisam ficar **depois** do `OTE(FC11.SWM)` e **antes** do `PID(FC11,...)`.
- As rungs da LC21 precisam ficar **depois** do `PID(LC21,...)`. Elas sobrescrevem o `SP_P21` (calculado
  no `Lad_028`) antes de ele ir para a saida analogica no `Lad_100`.

## Tags criadas pela importacao (escopo do controlador)

| Tag | Tipo | Valor inicial | Funcao |
|---|---|---|---|
| `FC11_HOLD` | BOOL | 0 | FC11 congelada enquanto a alimentacao esta cortada |
| `FC11_OUT_MEM` | REAL | 25.0 | Ultima saida boa da FC11 |
| `LC21_FF_GAIN` | REAL | 0.15 | Ganho do feedforward (% de P21 por hl/h de desvio de FT11) |

## Como importar (RSLogix 5000 v19)

1. Abra a rotina `Lad_099_Controllers` e selecione a rung de referencia da tabela acima.
2. Clique com o botao direito e escolha **Import Rungs...**. Selecione o arquivo `.L5X`.
3. Na janela de importacao, as tags novas aparecem como **Create**. As tags que ja existem (FC11,
   LC21, INLET_FT11 etc.) devem aparecer como **Use Existing**.
4. Confira se as rungs entraram na posicao certa e faca a verificacao da rotina (*Verify Routine*).
5. Online: use *Accept / Test / Assemble* nas edicoes. `test_bits.1` continua em 0, entao nada muda
   ate voce ligar o bit.

Se a sua versao nao tiver **Import Rungs**, insira rungs vazias na posicao certa, de duplo clique no
numero da rung e cole o texto de `rungs_texto.txt`. Depois crie as tags da tabela acima.

## Como testar

1. Abra um trend no RSLogix (100-200 ms) com `COLUMN_LT21`, `LC21.OUT`, `SP_P21`, `INLET_FT11`,
   `FC11.OUT`, `FC11_HOLD` e `COLUMN_STOP_FEED`.
2. Com o Aldox em producao (passo 115), faca o toggle de `test_bits.1` para **1**.
3. O que esperar:
   - Com a vazao no setpoint, `SP_P21` fica praticamente igual a `LC21.OUT` (sem tranco ao ligar o bit).
   - Se a alimentacao for cortada, `SP_P21` cai ~67 % abaixo de `LC21.OUT` (0,15 x 450) e a P21
     desacelera na hora. `FC11_HOLD` liga e a `FC11.OUT` fica parada na ultima posicao boa.
4. Para voltar ao original, faca o toggle de `test_bits.1` para **0**.

## Ajustes depois do teste

- **`LC21_FF_GAIN`:** comece em 0,15. Se o nivel ainda sobe quando a vazao aumenta, suba ate ~0,19.
  Se a P21 ficar tremendo com o ruido do FT11, desca.
- **Sintonia da LC21** (valores online em 27/09: equacao Dependent, Kc 0,7, Ti 1,3 min, Td 0, UPD
  0,05 s): suba o Kc para 1,0 e depois 1,5, mantendo o Ti em 1,3 min. Faca um passo de cada vez e
  observe pelo menos 3 ciclos entre um passo e outro.
- **Observacao:** durante o hold da FC11, o bit de manual da FC11 no supervisorio
  (`ALDOX_2_ADFM.BITS.2`) aparece ligado. Isso e esperado.

## Versao 2 do arquivo da LC21 (27/09)

A primeira versao escrevia o feedforward no `LC21.BIAS`. Online, a LC21 esta em equacao **Dependent**
com **No Bias Calculation desmarcado**. Nessa configuracao, a propria PID pode recalcular o BIAS
quando vai para manual, e isso brigaria com a rung. A versao 2 nao mexe na PID: ela soma a correcao
direto na velocidade da bomba (`SP_P21`), e so sobre o **desvio** da vazao em relacao ao setpoint.
Por isso, ao ligar o `test_bits.1` com a vazao no setpoint, nao ha tranco.

**Se voce ja importou a versao 1:**
1. Apague as duas rungs dela (a do `CPT(LC21.BIAS,...)` e a do `ONS(LC21_FF_ONS_ON)`).
2. Confira se `LC21.BIAS = 0`.
3. As tags `LC21_FF_ONS_ON` e `LC21_FF_ONS_OFF` podem ser apagadas.
