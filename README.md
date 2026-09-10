# Nota de CIP - Fermentadores
## Levantamento de valores medios por passo para definicao das faixas

**Estacao:** CIP Fermentadores + Shot Fermentadores
**Periodo analisado:** 26/08/2026 a 10/09/2026
**Ciclos avaliados:** 23 (CIP, receita MISTO) e 4 (Shot)
**Data do levantamento:** 10/09/2026

---

## 1. Leitura importante antes dos numeros

A nota de CIP dos fermentadores esta **em operacao de teste**. As faixas (valor minimo e
maximo de cada item) que estao hoje no sistema **nao foram definidas por engenharia para os
fermentadores** - elas foram copiadas por analogia da Adega de Pressao (ADP), que ja tinha a
nota implantada, apenas para que o painel comecasse a produzir numero.

Por isso:

> **A nota media de 5,76 nao significa que o CIP dos fermentadores esta ruim.**
> Significa que ainda nao existe uma faixa de referencia validada para esta estacao.

O objetivo deste levantamento e exatamente esse: mostrar o **valor real medido em cada item de
cada passo**, para que se decida, item por item, se:

- **(A)** a faixa e que precisa ser corrigida (o processo esta estavel, so a referencia esta errada), ou
- **(B)** o processo/instrumento e que precisa de acao (o valor medido realmente nao atende).

---

## 2. Situacao atual

| Estacao | Receita | Ciclos | Nota media | Menor | Maior | % conforme (>= 9,0) | Itens fora por ciclo |
|---|---|---|---|---|---|---|---|
| CIP Fermentadores | MISTO | 23 | **5,76** | 2,00 | 8,00 | 0% | 6,8 de 15 |
| Shot Fermentadores | SHOT_1 | 4 | **4,75** | 1,00 | 6,00 | 0% | 4,5 de 10 |

A conta fecha exatamente: 10,00 - 4,24 pontos perdidos = 5,76 (CIP) e 10,00 - 5,27 = 4,75 (Shot).
Os dados sao consistentes.

---

## 3. Onde a nota esta sendo perdida

### 3.1 CIP Fermentadores - 4,24 pontos perdidos por ciclo

| # | Etapa | Item | Peso | Reprovou | Pts perdidos | Valor medio | Faixa atual | Motivo |
|---|---|---|---|---|---|---|---|---|
| 1 | Limpeza 1 - Alcalino 1 | CONDUTIVIDADE | 1,0 | 23 de 23 | **1,00** | 54,07 mS | 100 a 140 | Abaixo do minimo |
| 2 | Enxague Inicial | VAZAO | 0,5 | 23 de 23 | **0,50** | 0,93 hl/h | 110 a 400 | Passo sem dado |
| 3 | Enxague Intermediario 1 | VAZAO | 0,5 | 23 de 23 | **0,50** | sem leitura | 110 a 400 | Passo sem dado |
| 4 | Limpeza 3 - Acido | VAZAO | 0,5 | 21 de 23 | **0,46** | 328,82 hl/h | 140 a 300 | Acima do maximo |
| 5 | Sanitizacao | VAZAO | 1,0 | 10 de 23 | **0,43** | 328,99 hl/h | 160 a 340 | Acima do maximo |
| 6 | Limpeza 1 - Alcalino 1 | VAZAO | 0,5 | 20 de 23 | **0,43** | 323,07 hl/h | 140 a 300 | Acima do maximo |
| 7 | Sanitizacao | PRESSAO | 1,0 | 5 de 23 | 0,22 | 2,14 bar | 0,3 a 3,0 | Excursao pontual |
| 8 | Enxague Intermediario 3 | VAZAO | 0,5 | 10 de 23 | 0,22 | 116,93 hl/h | 110 a 400 | Instavel |
| 9 | Limpeza 2 - Alcalino 2 | VAZAO | 0,5 | 9 de 23 | 0,20 | 278,32 hl/h | 140 a 300 | Pico isolado |
| 10 | Limpeza 1 - Alcalino 1 | PRESSAO | 0,5 | 5 de 23 | 0,11 | 2,09 bar | 0,3 a 3,0 | Excursao pontual |
| 11 | Limpeza 3 - Acido | PRESSAO | 0,5 | 4 de 23 | 0,09 | 2,11 bar | 0,3 a 3,0 | Excursao pontual |
| 12 | Limpeza 3 - Acido | CONDUTIVIDADE | 1,0 | 1 de 23 | 0,04 | 36,24 mS | 25 a 55 | Ciclo sem dado |
| 13 | Enxague Intermediario 2 | VAZAO | 0,5 | 1 de 23 | 0,02 | 265,82 hl/h | 110 a 400 | Ciclo sem dado |
| 14 | Limpeza 2 - Alcalino 2 | PRESSAO | 0,5 | 1 de 23 | 0,02 | 1,50 bar | 0,3 a 3,0 | Ciclo sem dado |
| | | | | | **4,24** | | | |

### 3.2 Shot Fermentadores - 5,27 pontos perdidos por ciclo

| # | Etapa | Item | Peso | Reprovou | Pts perdidos | Valor medio | Faixa atual | Motivo |
|---|---|---|---|---|---|---|---|---|
| 1 | Shot Caustico | CONDUTIVIDADE | 2,0 | 4 de 4 | **2,00** | 26,13 mS | 100 a 140 | Abaixo do minimo |
| 2 | Shot Caustico | VAZAO | 1,0 | 4 de 4 | **1,00** | 65,45 hl/h | 140 a 300 | Abaixo do minimo |
| 3 | Circulacao Acido | VAZAO | 1,0 | 3 de 4 | **0,75** | 311,20 hl/h | 140 a 300 | Acima do maximo |
| 4 | Circulacao Acido | CONDUTIVIDADE | 2,0 | 1 de 4 | 0,50 | 36,74 mS | 25 a 55 | Ciclo sem dado |
| 5 | Shot Caustico | PRESSAO | 1,0 | 1 de 4 | 0,25 | 0,83 bar | 0,3 a 3,0 | Ciclo sem dado |
| 6 | Circulacao Acido | PRESSAO | 1,0 | 1 de 4 | 0,25 | 2,05 bar | 0,3 a 3,0 | Ciclo sem dado |
| 7 | Circulacao Sanitizante | PRESSAO | 0,5 | 1 de 4 | 0,13 | 2,05 bar | 0,3 a 3,0 | Ciclo sem dado |
| 8 | Circulacao Sanitizante | VAZAO | 0,5 | 1 de 4 | 0,13 | 311,38 hl/h | 160 a 340 | Ciclo sem dado |
| 9 | Empurre Agua Recuperada | VAZAO | 0,5 | 1 de 4 | 0,13 | 198,51 hl/h | 110 a 400 | Ciclo sem dado |
| 10 | Enxague Agua Recuperada | VAZAO | 0,5 | 1 de 4 | 0,13 | 247,64 hl/h | 110 a 400 | Ciclo sem dado |
| | | | | | **5,27** | | | |

**Observacao sobre o Shot:** dos 4 ciclos, **um unico ciclo ficou praticamente sem dados** e
tirou nota 1,00. Os outros 3 tiraram 6,00. Esse ciclo sozinho derruba a media de 6,00 para 4,75.
Os itens 4 a 10 da tabela acima reprovaram **so por causa dele** - o valor medido nos demais
ciclos esta dentro da faixa.

---

## 4. As quatro decisoes

Os 14 itens do CIP e os 10 do Shot se agrupam em **quatro decisoes**. Nenhuma delas sozinha leva
a nota acima do corte de 9,0. As quatro juntas levam.

### DECISAO 1 - Teto de vazao (1,49 pts no CIP + 0,75 no Shot)

**O que os dados mostram:** a bomba de CIP dos fermentadores circula de forma muito estavel
entre **320 e 345 hl/h**. As faixas atuais terminam em 300 hl/h.

| Etapa | Media | Mediana | Minimo | Maximo | Desvio | Faixa atual | Atende |
|---|---|---|---|---|---|---|---|
| Limpeza 1 - Alcalino 1 | 323,07 | 337,23 | 192,90 | 349,98 | 36,17 | 140 a 300 | 14% |
| Limpeza 3 - Acido | 328,82 | 341,40 | 234,56 | 349,59 | 26,97 | 140 a 300 | 9% |
| Sanitizacao | 328,99 | 336,70 | 265,42 | 350,38 | 22,37 | 160 a 340 | 62% |
| Limpeza 2 - Alcalino 2 | 278,32 | 291,29 | 151,12 | 445,73 | 64,35 | 140 a 300 | 61% |
| Shot - Circulacao Acido | 311,20 | 329,50 | 273,51 | 330,59 | 32,64 | 140 a 300 | 33% |

O desvio e de 7% a 11% da media nas etapas de circulacao. **Isso e um processo estavel.** O
problema nao e a bomba oscilar - e o teto de 300 hl/h nao corresponder a vazao que a bomba
instalada entrega.

**Proposta:** manter o **minimo em 140 hl/h** (o limite critico para a limpeza, que ninguem
esta propondo afrouxar) e subir o **maximo de 300 para 390 hl/h**.

**Pergunta para decisao:**
> O teto de 300 hl/h tem base fisica (limite do spray-ball, limite de pressao no tanque) ou foi
> herdado do padrao da ADP? Se for herdado, subir o teto e a correcao. Se for limite fisico
> real, a bomba e que precisa ser estrangulada e ai e obra.

---

### DECISAO 2 - Condutividade do alcalino (1,00 pt no CIP + 2,00 no Shot)

**O que os dados mostram:** dentro da mesma estacao, os dois alcalinos tem concentracoes bem
diferentes.

| Etapa | Condutividade media | Desvio | Faixa atual | Atende |
|---|---|---|---|---|
| Limpeza 1 - **Alcalino 1** | **54,07 mS** | 5,20 | 100 a 140 | **0 de 21** |
| Limpeza 2 - **Alcalino 2** | **115,63 mS** | 6,08 | 100 a 140 | **21 de 21** |
| Shot - **Shot Caustico** | **26,13 mS** | 11,11 | 100 a 140 | **0 de 3** |

O Alcalino 2 esta perfeito e absolutamente dentro da faixa. O Alcalino 1 esta em **47% da
concentracao do Alcalino 2**, de forma estavel (desvio de apenas 5,20 mS em 21 ciclos).

O Alcalino 1 tambem e mais curto: circula cerca de **38% do tempo** do Alcalino 2.

Isso e o padrao tipico de um **primeiro alcalino de pre-lavagem**, que sai diluido porque se
mistura com a agua residual do enxague anterior e arrasta a sujeira grossa.

**Pergunta para decisao:**
> O Alcalino 1 e, por projeto, uma pre-lavagem alcalina diluida - e nesse caso ele precisa de
> **faixa propria** (algo como 40 a 70 mS), diferente do Alcalino 2?
> Ou os 54 mS sao concentracao insuficiente e a **dosagem/retorno de soda do primeiro alcalino
> precisa de correcao na logica do CIP**?

O caso do **Shot Caustico a 26 mS** e mais forte: um shot deveria ser uma aplicacao concentrada,
e 26 mS e um quarto do que o Alcalino 2 entrega. Vale conferir se a soda esta realmente sendo
dosada nesse passo. **Atencao:** so ha 3 ciclos com dado, entao a amostra ainda e pequena.

---

### DECISAO 3 - Passos que nao chegam ao banco (1,00 pt no CIP)

Dois itens do CIP reprovam em **23 de 23 ciclos** simplesmente porque o passo nunca e capturado.

| Passo | Rotina no PLC | Papel na nota | Amostras em 23 ciclos |
|---|---|---|---|
| **13** | `CIP_AGUA_ENXAGUE` | **Enxague Inicial** | **5** (vazao ~0,9 hl/h) |
| **17** | `CIP_AGUA_REC_EMPURRE` | **Enxague Intermediario 1** | **0** |
| 18 | `CIP_DRENO_EMPURRE` | (nao pontuado) | 0 |
| 19 | `CIP_ALCALINO_2_INICIA` | (nao pontuado) | 0 |
| 12 | `CIP_AGUA_REC_ENXAGUE` | (nao pontuado) | **939** (vazao 252 hl/h) |

Dois achados:

1. **O passo 12 e onde o enxague inicial realmente acontece.** Ele tem 939 amostras com vazao
   continua de 252 hl/h. O passo 13, que e o que esta sendo pontuado, tem 5 amostras em 23
   ciclos e vazao praticamente zero - ou seja, o CIP entra nesse passo mas nao passa agua por
   ele. A diferenca e que o passo 12 usa **agua recuperada** e o 13 usa **agua industrial**.

2. **Os passos 17, 18 e 19 nunca aparecem** em nenhum ciclo, embora o 16 (376 amostras) e o 20
   (7.158 amostras) aparecam normalmente. Ou esses passos sao curtos demais para a taxa de
   amostragem atual, ou a receita esta pulando eles.

**Pergunta para decisao:**
> O enxague inicial da receita e o de agua recuperada (passo 12) ou o de agua industrial
> (passo 13)? Se for o 12, a nota deve pontuar o passo 12 e o item volta a ser avaliavel.
> E o "empurre com agua recuperada" (passo 17) esta realmente sendo executado?

Essa e uma decisao de processo, nao de sistema - por isso nao mudei nada por conta propria.

---

### DECISAO 4 - Confiabilidade dos instrumentos (0,44 pt no CIP + 0,63 no Shot)

Aparecem dois valores fixos repetidos em passos que nao tem relacao entre si, o que e assinatura
de falha de instrumento ou de comunicacao, e nao de processo:

| Valor | Onde aparece |
|---|---|
| **0,07 bar** (pressao) | Valor minimo identico nos passos 15, 20, 43 e 47 |
| **1046,25 hl/h** (vazao) | Valor maximo identico nos passos 20, 21, 22, 44, 45 e no passo 7 do Shot |

A media de pressao esta boa em todos os passos (1,50 a 2,14 bar, bem dentro de 0,3 a 3,0). As
reprovacoes acontecem em ciclos isolados onde a leitura vai a praticamente zero ou passa de
3,9 bar.

O valor de **1046,25 hl/h e ~3x a vazao normal da bomba**, e se repete exatamente igual em seis
passos diferentes. Isso e quase certamente saturacao de escala do transmissor ou leitura invalida.

**Importante:** esses valores estao **contaminando as medias** deste proprio relatorio. O caso
mais claro e o Enxague Intermediario 3 (passo 45): media de 116,93 hl/h com 83% das amostras
proximas de zero e picos de 1046,25. Essa media nao descreve nada real.

**Acao proposta (tecnica, nao precisa de decisao de processo):** filtrar essas duas leituras na
coleta antes de recalibrar qualquer faixa, para nao calibrar em cima de ruido.

---

## 5. Questao em aberto: a vazao e continua ou pulsada?

Em varios passos, um terco ou mais das amostras registra vazao praticamente zero enquanto a
mediana registra vazao normal:

| Passo | Etapa | Amostras | Vazao media | Vazao mediana | % amostras quase zero |
|---|---|---|---|---|---|
| 20 | Alcalino 2 | 7.158 | 281,17 | 319,22 | **33%** |
| 21 | Alcalino 2 - empurre | 274 | 278,18 | 312,10 | **36%** |
| 44 | Acido - empurre | 107 | 337,80 | 91,78 | **40%** |
| 45 | Enxague Intermediario 3 | 576 | 56,54 | 0,93 | **83%** |
| 6 (Shot) | Shot Caustico | 218 | 65,41 | 0,93 | **75%** |
| 7 (Shot) | Empurre | 339 | 184,12 | 0,93 | **77%** |

Quando isso acontece, **a media aritmetica nao representa o processo** - ela fica entre dois
estados (parado e circulando) e nao descreve nenhum dos dois.

**Pergunta para decisao:**
> A circulacao nesses passos e pulsada por projeto (enche / esvazia / repete), ou o medidor
> FIT796702 esta na linha de alimentacao e le zero enquanto o tanque esta drenando?

Se for pulsada por projeto, **a nota nao pode usar media simples nesses passos** - tem que usar
a media apenas dos periodos em que ha circulacao. Isso muda a forma de calcular, nao a faixa.

---

## 6. Projecao: quanto cada decisao vale na nota

### CIP Fermentadores (hoje 5,76)

| Etapa | Nota projetada |
|---|---|
| Situacao atual | **5,76** |
| + Decisao 1 (teto de vazao 300 -> 390) | ~7,25 |
| + Decisao 2 (condutividade do Alcalino 1) | ~8,25 |
| + Decisao 3 (capturar os passos 13 e 17) | ~9,25 |
| + Decisao 4 (filtrar leituras invalidas) | ~9,70 |

### Shot Fermentadores (hoje 4,75)

| Etapa | Nota projetada |
|---|---|
| Situacao atual | **4,75** |
| + corrigir o ciclo sem dados | ~6,00 |
| + Decisao 1 (teto de vazao) | ~6,75 |
| + Decisao 2 (condutividade do shot caustico) | ~8,75 |

**Conclusao:** o corte de conformidade de 9,0 da norma ZBS-503661 so e alcancavel com as
quatro decisoes tomadas. Nenhuma isolada resolve.

---

## 7. Resumo do que precisa de decisao

| # | Assunto | Quem decide | Impacto |
|---|---|---|---|
| 1 | O teto de 300 hl/h e limite fisico ou herdado da ADP? | Processo / Automacao | 1,49 + 0,75 pts |
| 2 | O Alcalino 1 e pre-lavagem diluida (faixa propria) ou a dosagem esta baixa? | Processo | 1,00 + 2,00 pts |
| 3 | O enxague inicial da receita e o passo 12 ou o 13? O passo 17 roda? | Processo / Automacao | 1,00 pt |
| 4 | Filtrar 0,07 bar e 1046,25 hl/h na coleta | Automacao (ja encaminhavel) | 0,44 + 0,63 pts |
| 5 | A circulacao e pulsada por projeto? | Processo | muda o calculo |

---

## 8. Origem dos dados

Todos os numeros deste relatorio vem de `06_relatorio_medias_por_passo.sql`, executado sobre a
base `adegas` do PostgreSQL em 10/09/2026:

- Bloco 1 - media, mediana, minimo, maximo e desvio por item/passo
- Bloco 2 - pontos perdidos por ciclo, por item
- Bloco 3 - amostras brutas, usado para detectar vazao pulsada
- Bloco 4 - detalhe ciclo a ciclo
- Bloco 5 - panorama das notas

O mapa de passos foi conferido contra o arquivo L5X do Grafset `CIP_FERMENTADORES`
(ver `analise_l5x_fermentadores_maturadores.md`, secao 2.2).

**Proximo passo:** repetir este mesmo levantamento para os **Maturadores**, apos a estacao
completar ciclos suficientes.

---

## Anexo

- [Tabela resumida de valores medidos por passo](TABELA_VALORES_POR_PASSO_FERMENTADORES.md)
