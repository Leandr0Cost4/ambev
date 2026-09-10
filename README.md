# Nota de CIP - Adega

Levantamento dos valores medidos por passo nas estacoes de CIP da Adega, para definicao das faixas
da nota conforme a norma **ZBS-503661**.

**Data do levantamento:** 10/09/2026

---

## Leia isto antes dos numeros

A nota de CIP destas estacoes esta **em operacao de teste**. As faixas (valor minimo e maximo de
cada item) que estao hoje no sistema **nao foram definidas por engenharia para estas estacoes** -
foram copiadas por analogia da Adega de Pressao (ADP), que ja tinha a nota implantada, apenas para
que o painel comecasse a produzir numero.

> **As notas abaixo nao significam que o CIP esta ruim.**
> Significam que ainda nao existe uma faixa de referencia validada para estas estacoes.

O objetivo destes relatorios e mostrar o valor real medido em cada item de cada passo, para que se
decida, item por item, se e a **faixa** que precisa ser corrigida ou se e o **processo** que precisa
de acao.

---

## Fermentadores

| Estacao | Ciclos | Nota media | Menor | Maior | Itens fora por ciclo |
|---|---|---|---|---|---|
| CIP Fermentadores | 23 | 5,76 | 2,00 | 8,00 | 6,8 de 15 |
| Shot Fermentadores | 4 | 4,75 | 1,00 | 6,00 | 4,5 de 10 |

Periodo: 26/08/2026 a 10/09/2026.

- **[Relatorio completo](RELATORIO_FERMENTADORES.md)** - as quatro decisoes, projecoes de nota e
  perguntas para o processo
- [Tabela de valores por passo](TABELA_VALORES_POR_PASSO_FERMENTADORES.md) - media, minimo, maximo
  e faixa de cada item

---

## Maturadores

| Estacao | Ciclos | Nota media | Menor | Maior | Itens fora por ciclo |
|---|---|---|---|---|---|
| CIP Maturadores | 6 | 6,00 | 5,50 | 7,00 | 6,3 de 15 |
| Shot Maturadores | 16 | 5,47 | 4,00 | 6,00 | 4,0 de 10 |

Periodo: 22/08/2026 a 10/09/2026.

- **[Relatorio completo](RELATORIO_MATURADORES.md)** - as quatro decisoes, projecoes de nota e
  perguntas para o processo
- [Tabela de valores por passo](TABELA_VALORES_POR_PASSO_MATURADORES.md) - media, minimo, maximo,
  setpoint e faixa de cada item

---

## O achado principal

A maior perda de nota nas duas estacoes vem do **teto de vazao**, e a causa foi localizada no
programa do CLP.

Existe uma malha PID de vazao em cada estacao - `FIC796702` nos fermentadores e `FIC796680` nos
maturadores - cujo setpoint vem da IHM:

```
MOVE(FIT796680.Out, FIC796680.AUX_PV)      <- a vazao medida alimenta o PID
MOVE(FIC796680.IHM_SP, FIC796680.PID.SP)   <- o setpoint vem da IHM
```

E um setpoint **unico para o ciclo inteiro**, nao um por passo.

**Nos maturadores o valor esta confirmado pelos dados: 350 hl/h.** A mediana de vazao fica em
349,x em todos os passos de circulacao, com desvio de 2% a 3%.

**Nos fermentadores o valor ainda nao esta confirmado.** Os maximos batem em 349-350, mas as
medianas ficam entre 319 e 345 - a estacao chega perto de 350 e nao sustenta. Pode ser setpoint
configurado mais baixo, ou setpoint em 350 com a malha nao segurando (bomba, valvula, restricao).

> **Nas duas estacoes, o teto da nota (300 hl/h) esta abaixo da vazao praticada.**
> Enquanto o maximo for 300, a nota reprova o CIP por circular na vazao em que ele circula.

O setpoint vem da IHM, nao da receita nem de constante gravada no programa - por isso o valor nao
aparece no L5X. Para confirmar o numero exato de cada estacao, o caminho mais rapido e a tela de
CIP no supervisorio.

---

## Origem dos dados

Os numeros vem da base `adegas` do PostgreSQL, alimentada pela coleta OPC das estacoes de CIP.
As medias apresentadas sao a **media por ciclo**, que e a que entra no calculo da nota.

Os mapas de passos e as malhas de controle foram conferidos contra os programas do CLP dos
Grafsets `CIP_FERMENTADORES` e `CIP_TANQUES_MAT`.
