# Nota de CIP - Maturadores
## Levantamento de valores medidos por passo para definicao das faixas

**Estacao:** CIP Maturadores + Shot Maturadores
**Periodo analisado:** 22/08/2026 a 10/09/2026
**Ciclos avaliados:** 6 (CIP, receita MISTO) e 16 (Shot)
**Data do levantamento:** 10/09/2026

---

## 1. Leitura importante antes dos numeros

A nota de CIP dos maturadores esta **em operacao de teste**. As faixas (valor minimo e maximo
de cada item) que estao hoje no sistema **nao foram definidas por engenharia para os
maturadores** - foram copiadas por analogia da Adega de Pressao (ADP), que ja tinha a nota
implantada, apenas para que o painel comecasse a produzir numero.

Por isso:

> **A nota media de 6,00 nao significa que o CIP dos maturadores esta ruim.**
> Significa que ainda nao existe uma faixa de referencia validada para esta estacao.

O objetivo deste levantamento e mostrar o **valor real medido em cada item de cada passo**,
para que se decida, item por item, se:

- **(A)** a faixa e que precisa ser corrigida (o processo esta estavel, so a referencia esta errada), ou
- **(B)** o processo/instrumento e que precisa de acao (o valor medido realmente nao atende).

---

## 2. Situacao atual

| Estacao | Receita | Ciclos | Nota media | Menor | Maior | % conforme (>= 9,0) | Itens fora por ciclo |
|---|---|---|---|---|---|---|---|
| CIP Maturadores | MISTO | 6 | **6,00** | 5,50 | 7,00 | 0% | 6,3 de 15 |
| Shot Maturadores | SHOT_1 | 16 | **5,47** | 4,00 | 6,00 | 0% | 4,0 de 10 |

A conta fecha exatamente: 10,00 - 4,00 pontos perdidos = 6,00 (CIP) e 10,00 - 4,53 = 5,47 (Shot).
Os dados sao consistentes.

**Sobre o tamanho da amostra:** o Shot tem 16 ciclos, base solida. O CIP tem 6 ciclos - suficiente
para enxergar tendencia, mas apertado. Onde o CIP aparecer com poucos ciclos, isso esta marcado.

---

## 3. Onde a nota esta sendo perdida

### 3.1 CIP Maturadores - 4,00 pontos perdidos por ciclo

| # | Etapa | Item | Peso | Reprovou | Pts perdidos | Valor medio | Faixa atual | Motivo |
|---|---|---|---|---|---|---|---|---|
| 1 | Limpeza 1 - Alcalino 1 | CONDUTIVIDADE | 1,0 | 6 de 6 | **1,00** | 63,88 mS | 100 a 140 | Abaixo do minimo |
| 2 | Sanitizacao | VAZAO | 1,0 | 4 de 6 | **0,67** | 331,80 hl/h | 160 a 340 | Acima do maximo |
| 3 | Limpeza 2 - Alcalino 2 | VAZAO | 0,5 | 6 de 6 | **0,50** | 347,78 hl/h | 140 a 300 | Acima do maximo |
| 4 | Enxague Inicial | VAZAO | 0,5 | 6 de 6 | **0,50** | sem leitura | 110 a 400 | Passo nao existe |
| 5 | Limpeza 1 - Alcalino 1 | VAZAO | 0,5 | 6 de 6 | **0,50** | 342,11 hl/h | 140 a 300 | Acima do maximo |
| 6 | Limpeza 3 - Acido | VAZAO | 0,5 | 5 de 6 | **0,42** | 332,53 hl/h | 140 a 300 | Acima do maximo |
| 7 | Enxague Intermediario 2 | VAZAO | 0,5 | 4 de 6 | 0,33 | 243,13 hl/h | 110 a 400 | Passo quase sem dado |
| 8 | Enxague Intermediario 1 | VAZAO | 0,5 | 1 de 6 | 0,08 | 283,23 hl/h | 110 a 400 | Ciclo sem dado |
| | | | | | **4,00** | | | |

**A pressao nao perde nenhum ponto no CIP dos maturadores.** Os quatro itens de pressao atendem
em 100% dos ciclos, com desvios minusculos (0,01 a 0,17 bar). O instrumento esta confiavel.

### 3.2 Shot Maturadores - 4,53 pontos perdidos por ciclo

| # | Etapa | Item | Peso | Reprovou | Pts perdidos | Valor medio | Faixa atual | Motivo |
|---|---|---|---|---|---|---|---|---|
| 1 | Shot Caustico | CONDUTIVIDADE | 2,0 | 16 de 16 | **2,00** | 27,96 mS | 100 a 140 | Abaixo do minimo |
| 2 | Circulacao Acido | VAZAO | 1,0 | 16 de 16 | **1,00** | 351,05 hl/h | 140 a 300 | Acima do maximo |
| 3 | Shot Caustico | VAZAO | 1,0 | 16 de 16 | **1,00** | 112,43 hl/h | 140 a 300 | Abaixo do minimo |
| 4 | Circulacao Sanitizante | VAZAO | 0,5 | 14 de 16 | **0,44** | 340,56 hl/h | 160 a 340 | Acima do maximo |
| 5 | Circulacao Acido | PRESSAO | 1,0 | 1 de 16 | 0,06 | 2,12 bar | 0,3 a 3,0 | Excursao pontual |
| 6 | Circulacao Sanitizante | PRESSAO | 0,5 | 1 de 16 | 0,03 | 2,12 bar | 0,3 a 3,0 | Excursao pontual |
| | | | | | **4,53** | | | |

O item 4 merece destaque: a vazao media e **340,56 hl/h contra um teto de 340,0**. Reprova em
14 de 16 ciclos por **0,56 hl/h**.

---

## 4. As quatro decisoes

### DECISAO 1 - O teto de vazao esta abaixo do setpoint da maquina (2,09 pts no CIP + 1,44 no Shot)

Esta e a maior perda das duas estacoes somadas, e a de causa mais clara.

**O que os dados mostram:**

| Etapa | Media | Mediana | Minimo | Maximo | Desvio | Faixa atual | Atende |
|---|---|---|---|---|---|---|---|
| Limpeza 2 - Alcalino 2 | 347,78 | 352,03 | 326,61 | 355,52 | 10,71 | 140 a 300 | 0% |
| Limpeza 1 - Alcalino 1 | 342,11 | 349,24 | 307,79 | 350,05 | 16,87 | 140 a 300 | 0% |
| Limpeza 3 - Acido | 332,53 | 347,17 | 268,28 | 349,24 | 31,90 | 140 a 300 | 17% |
| Sanitizacao | 331,80 | 349,26 | 258,10 | 350,35 | 36,69 | 160 a 340 | 33% |
| Shot - Circulacao Acido | 351,05 | 349,58 | 340,96 | 380,03 | 8,04 | 140 a 300 | 0% |
| Shot - Circulacao Sanitizante | 340,56 | 349,93 | 180,92 | 379,94 | 43,34 | 160 a 340 | 13% |

Repare no desvio: 10,71 hl/h sobre uma media de 347,78 no Alcalino 2 (3%), e 8,04 sobre 351,05 na
Circulacao Acido do Shot (2%). **Isso nao e um processo oscilando - e uma malha de controle
trabalhando bem.**

**A causa foi localizada no programa do CLP.** Existe um controlador PID de vazao, `FIC796680`,
alimentado pelo transmissor `FIT796680`:

```
MOVE(FIT796680.Out, FIC796680.AUX_PV)      <- a vazao medida alimenta o PID
MOVE(FIC796680.IHM_SP, FIC796680.PID.SP)   <- o setpoint vem da IHM
```

Tres consequencias:

1. **E um setpoint unico, nao um por passo.** A mesma malha fica ativa o ciclo inteiro. Por isso a
   mediana de vazao e praticamente identica em todos os passos: 348,2 / 349,8 / 349,8 / 350,2 /
   348,5 / 349,3 / 349,7 / 349,8 / 349,7 / 349,7 hl/h.

2. **O setpoint vem da IHM**, nao da receita nem de constante gravada no programa. Por isso o valor
   nao aparece no L5X - ele esta no supervisorio.

3. **O valor em operacao e 350 hl/h.** As medias menores que 350 sao o transitorio de subida no
   inicio de cada passo puxando a media para baixo.

> **O teto da nota (300 hl/h) esta 50 hl/h abaixo do setpoint da propria maquina (350 hl/h).**
> Enquanto o maximo for 300, a nota reprova o CIP por fazer exatamente o que foi mandado fazer.

**Proposta:** manter o **minimo em 140 hl/h** (o limite critico para a limpeza, que ninguem esta
propondo afrouxar) e subir o **maximo de 300 para 390 hl/h**. Na Sanitizacao e na Circulacao
Sanitizante, de 340 para 390. Com essa faixa, **todos os ciclos medidos passam** - o minimo
observado (258,10) e o maximo observado (380,03) ficam dentro.

**Pergunta para decisao:**
> Quem definiu o setpoint de 350 hl/h na IHM, e com base em que? Se veio de calculo de velocidade
> no spray-ball, o numero esta certo e e a faixa da nota que precisa ser corrigida. Se ninguem
> sabe a origem, essa e a hora de definir.

O caminho mais rapido para confirmar o valor exato e olhar a tela de CIP no supervisorio. Pela via
do CLP a tag e `FIC796680.PID.SP`, mas o `FIT796680` esta com `OpcUaAccess="None"` no programa,
entao talvez precise ser exposto para leitura por OPC.

---

### DECISAO 2 - Condutividade do alcalino (1,00 pt no CIP + 2,00 no Shot)

**O que os dados mostram:**

| Etapa | Condutividade media | Mediana | Minimo | Maximo | Desvio | Faixa atual | Atende |
|---|---|---|---|---|---|---|---|
| Limpeza 1 - **Alcalino 1** | **63,88 mS** | 64,14 | 53,92 | 73,62 | 6,97 | 100 a 140 | **0 de 6** |
| Limpeza 2 - **Alcalino 2** | **114,97 mS** | 114,18 | 111,21 | 121,53 | 3,78 | 100 a 140 | **6 de 6** |
| Shot - **Shot Caustico** | **27,96 mS** | 27,06 | 19,75 | 41,07 | 5,54 | 100 a 140 | **0 de 16** |

O Alcalino 2 esta perfeito: 114,97 mS com desvio de 3,78, atende em todos os ciclos. O Alcalino 1
esta em **56% da concentracao do Alcalino 2**, de forma estavel.

O Alcalino 1 tambem e mais curto: circula cerca de **24% do tempo** do Alcalino 2 (561 amostras
contra 2.358).

Isso e o padrao tipico de um **primeiro alcalino de pre-lavagem**, que sai diluido porque se
mistura com a agua residual do enxague anterior e arrasta a sujeira grossa.

**Pergunta para decisao:**
> O Alcalino 1 e, por projeto, uma pre-lavagem alcalina diluida - e nesse caso precisa de **faixa
> propria** (algo como 50 a 80 mS), diferente do Alcalino 2?
> Ou os 63,88 mS sao concentracao insuficiente, e a **dosagem de soda do primeiro alcalino precisa
> de correcao na logica do CIP**?

O caso do **Shot Caustico a 27,96 mS** e mais forte, e aqui a base e solida: **16 ciclos, desvio de
apenas 5,54 mS**. Um shot deveria ser uma aplicacao concentrada, e 27,96 mS e um quarto do que o
Alcalino 2 entrega. Vale conferir se a soda esta realmente sendo dosada nesse passo.

---

### DECISAO 3 - Passos que nao chegam ao banco (0,83 pt no CIP)

| Passo | Papel na nota | Amostras em 6 ciclos | Ciclos com dado |
|---|---|---|---|
| **13** | **Enxague Inicial** | **0** | **0 de 6** |
| **22** | **Enxague Intermediario 2** | **5** | **3 de 6** |
| 12 | (nao pontuado) | 310 | 6 de 6 |

Dois achados:

1. **O passo 13 nao existe nos maturadores.** Nao aparece uma unica amostra em nenhum dos 6 ciclos.
   A spec do MISTO aponta o Enxague Inicial para o passo 13, entao esse item reprova em 6 de 6 por
   ausencia - nao por processo. Enquanto isso, o **passo 12 tem 310 amostras com vazao mediana de
   348,23 hl/h**: e nele que o enxague inicial de fato acontece.

2. **O passo 22 e capturado em apenas 3 dos 6 ciclos**, com 5 amostras no total. Com tao pouco dado,
   a estatistica desse item nao significa nada: desvio de 154,38 sobre media de 243,13. O relatorio
   classifica como "processo instavel", mas o que existe de fato e falta de amostra.

**Pergunta para decisao:**
> O enxague inicial da receita e o passo 12? Se for, a nota deve pontuar o passo 12 e o item volta
> a ser avaliavel. E por que o passo 22 so aparece em metade dos ciclos - ele e curto demais para a
> taxa de amostragem, ou nao roda sempre?

Essa e uma decisao de processo, nao de sistema.

---

### DECISAO 4 - Vazao do Shot Caustico (1,00 pt no Shot)

| Etapa | Media | Mediana | Minimo | Maximo | Desvio | Faixa atual | Atende |
|---|---|---|---|---|---|---|---|
| Shot Caustico - VAZAO | 112,43 | 110,94 | 101,25 | 133,57 | 8,06 | 140 a 300 | 0 de 16 |

Este item **nao e caso de ajuste de faixa**. Com 16 ciclos e desvio de apenas 8,06 hl/h, o passo
circula de forma consistente a cerca de **112 hl/h** - um terco da vazao dos demais passos, que
rodam a 350 hl/h.

Olhando as amostras cruas do passo, a **mediana cai para 14,33 hl/h**: dentro do passo, a vazao
fica baixa a maior parte do tempo e sobe em rajadas. O passo esta rodando com vazao baixa de
verdade, nao e artefato de medicao.

**Pergunta para decisao:**
> Por que o Shot Caustico circula a 112 hl/h enquanto todos os outros passos circulam a 350?
> A malha de vazao esta desabilitada nesse passo, a valvula esta estrangulada, ou o circuito do
> shot e por projeto de vazao menor? Se for por projeto, o item precisa de faixa propria.

---

## 5. Projecao: quanto cada decisao vale na nota

### CIP Maturadores (hoje 6,00)

| Etapa | Nota projetada |
|---|---|
| Situacao atual | **6,00** |
| + Decisao 1 (teto de vazao 300 -> 390) | **8,09** |
| + Decisao 2 (condutividade do Alcalino 1) | **9,09** |
| + Decisao 3 (passos 13 e 22) | **9,92** |

### Shot Maturadores (hoje 5,47)

| Etapa | Nota projetada |
|---|---|
| Situacao atual | **5,47** |
| + Decisao 1 (teto de vazao) | **6,91** |
| + Decisao 2 (condutividade do shot caustico) | **8,91** |
| + Decisao 4 (vazao do shot caustico) | **9,91** |

**Conclusao:** no CIP, as Decisoes 1 e 2 sozinhas ja levam a nota a 9,09 - acima do corte de 9,0
da norma ZBS-503661. No Shot sao necessarias as tres.

---

## 6. Resumo do que precisa de decisao

| # | Assunto | Quem decide | Impacto |
|---|---|---|---|
| 1 | Quem definiu o setpoint de 350 hl/h na IHM e com base em que? | Processo / Automacao | 2,09 + 1,44 pts |
| 2 | O Alcalino 1 e pre-lavagem diluida (faixa propria) ou a dosagem esta baixa? | Processo | 1,00 + 2,00 pts |
| 3 | O enxague inicial e o passo 12? Por que o passo 22 so aparece em metade dos ciclos? | Processo / Automacao | 0,83 pt |
| 4 | Por que o Shot Caustico circula a 112 hl/h e nao a 350? | Processo / Manutencao | 1,00 pt |

---

## 7. Origem dos dados

Todos os numeros deste relatorio vem da base `adegas` do PostgreSQL, extraidos em 10/09/2026 sobre
6 ciclos do CIP (01/09 a 10/09) e 16 ciclos do Shot (22/08 a 07/09).

As medias apresentadas sao a **media por ciclo**, que e a que entra no calculo da nota.

O mapa de passos e a malha de controle de vazao foram conferidos contra o programa do CLP do
Grafset `CIP_TANQUES_MAT`.
