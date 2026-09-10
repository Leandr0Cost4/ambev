# Valores medidos por passo - Maturadores

**Periodo:** 22/08/2026 a 10/09/2026 | **Ciclos:** 6 (CIP) e 16 (Shot)

Media, minimo e maximo sao os **valores medidos** por ciclo.
A faixa e a **referencia usada hoje na nota** (herdada da ADP, ainda nao validada para os maturadores).

**Setpoint de vazao: 350 hl/h.** Confirmado no programa do CLP - existe a malha PID `FIC796680`,
cujo setpoint vem da IHM (`FIC796680.IHM_SP`). E um setpoint unico para o ciclo inteiro, o que
explica a mediana de vazao ser praticamente identica em todos os passos.
Nao ha setpoint localizado para condutividade nem para pressao.

Unidades: vazao em hl/h, condutividade em mS, pressao em bar.

---

## CIP Maturadores - receita MISTO

| Passo | Etapa | Item | Media | Minimo | Maximo | Setpoint | Faixa da nota |
|---|---|---|---|---|---|---|---|
| 13 | Enxague Inicial | Vazao | sem leitura | - | - | 350 | 110 a 400 |
| 15 | Alcalino 1 | Vazao | 342,11 | 307,79 | 350,05 | 350 | 140 a 300 |
| 15 | Alcalino 1 | Condutividade | 63,88 | 53,92 | 73,62 | - | 100 a 140 |
| 15 | Alcalino 1 | Pressao | 2,05 | 2,05 | 2,06 | - | 0,3 a 3,0 |
| 17 | Enxague Intermediario 1 | Vazao | 283,23 | 116,10 | 365,93 | 350 | 110 a 400 |
| 20 | Alcalino 2 | Vazao | 347,78 | 326,61 | 355,52 | 350 | 140 a 300 |
| 20 | Alcalino 2 | Condutividade | 114,97 | 111,21 | 121,53 | - | 100 a 140 |
| 20 | Alcalino 2 | Pressao | 1,65 | 1,56 | 1,79 | - | 0,3 a 3,0 |
| 22 | Enxague Intermediario 2 | Vazao | 243,13 | 66,23 | 350,59 | 350 | 110 a 400 |
| 43 | Acido | Vazao | 332,53 | 268,28 | 349,24 | 350 | 140 a 300 |
| 43 | Acido | Condutividade | 40,11 | 34,49 | 50,38 | - | 25 a 55 |
| 43 | Acido | Pressao | 2,01 | 1,77 | 2,06 | - | 0,3 a 3,0 |
| 45 | Enxague Intermediario 3 | Vazao | 172,10 | 146,28 | 191,07 | 350 | 110 a 400 |
| 47 | Sanitizacao | Vazao | 331,80 | 258,10 | 350,35 | 350 | 160 a 340 |
| 47 | Sanitizacao | Pressao | 1,99 | 1,63 | 2,06 | - | 0,3 a 3,0 |

## Shot Maturadores - receita SHOT_1

| Passo | Etapa | Item | Media | Minimo | Maximo | Setpoint | Faixa da nota |
|---|---|---|---|---|---|---|---|
| 6 | Shot Caustico | Vazao | 112,43 | 101,25 | 133,57 | 350 | 140 a 300 |
| 6 | Shot Caustico | Condutividade | 27,96 | 19,75 | 41,07 | - | 100 a 140 |
| 6 | Shot Caustico | Pressao | 1,53 | 0,48 | 1,73 | - | 0,3 a 3,0 |
| 8 | Enxague Agua Recuperada | Vazao | 315,30 | 210,51 | 345,58 | 350 | 110 a 400 |
| 10 | Circulacao Acido | Vazao | 351,05 | 340,96 | 380,03 | 350 | 140 a 300 |
| 10 | Circulacao Acido | Condutividade | 39,00 | 34,88 | 47,00 | - | 25 a 55 |
| 10 | Circulacao Acido | Pressao | 2,12 | 0,43 | 4,74 | - | 0,3 a 3,0 |
| 12 | Empurre Agua Recuperada | Vazao | 313,10 | 155,67 | 365,50 | 350 | 110 a 400 |
| 14 | Circulacao Sanitizante | Vazao | 340,56 | 180,92 | 379,94 | 350 | 160 a 340 |
| 14 | Circulacao Sanitizante | Pressao | 2,12 | 0,37 | 4,75 | - | 0,3 a 3,0 |

---

## Quatro notas rapidas

1. **O passo 13 nao existe nos maturadores** - zero amostras em 6 ciclos. O enxague inicial de fato
   acontece no passo 12, que nao e pontuado (310 amostras, vazao mediana 348,23 hl/h).

2. **O passo 22 so aparece em 3 dos 6 ciclos**, com 5 amostras no total. A estatistica desse item
   nao e confiavel.

3. **A vazao esta acima do teto da nota em 6 itens porque o setpoint da maquina e 350 hl/h e o teto
   da nota e 300.** Nao ha desvio de processo: o desvio medido e de 2% a 3% em torno do setpoint.

4. **O Shot Caustico circula a 112 hl/h**, um terco dos demais passos, de forma consistente em
   16 ciclos (desvio de 8,06). Isso nao e ajuste de faixa - e pergunta de processo.
