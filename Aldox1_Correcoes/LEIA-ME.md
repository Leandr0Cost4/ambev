# Aldox 1 - Rungs de correcao do controle de nivel da coluna (TESTE)

Todas as rungs novas comecam com `XIC(test_bits.1)`:

- `test_bits.1 = 0`: o programa se comporta exatamente como hoje (o BIAS da LC21 fica em 0 e o hold
  da FC11 nao atua).
- `test_bits.1 = 1`: as correcoes ficam ativas.

`test_bits` e uma tag DINT de escopo do controlador que ja existe. O bit 1 nao e usado em nenhum outro
lugar do programa.

## Arquivos

| Arquivo | Onde importar | Rungs |
|---|---|---|
| `Aldox1_FC11_Hold.L5X` | `Lad_099_Controllers`, **entre a rung 3** `XIC(M_FC11_MAN)OTE(FC11.SWM);` **e a rung 4** | 4 |
| `Aldox1_LC21_Feedforward.L5X` | `Lad_099_Controllers`, **entre a rung 23** `[MOV(100,LC21.MAXS) ...]` **e a rung do** `PID(LC21,...)` | 2 |
| `rungs_texto.txt` | O mesmo texto das rungs, para colar no editor ASCII caso a importacao nao funcione | - |

Os numeros 3, 4, 23 e 24 sao do L5X exportado em 27/09/2026. Se o programa mudou, guie-se pelo
conteudo das rungs, nao pelo numero. **A posicao importa:**

- As rungs da FC11 precisam ficar **depois** do `OTE(FC11.SWM)` e **antes** do `PID(FC11,...)`.
- As rungs da LC21 precisam ficar **depois** do `OTE(LC21.SWM)` (rung 19) e **imediatamente antes**
  do `PID(LC21,...)`.

## Tags criadas pela importacao (escopo do controlador)

| Tag | Tipo | Valor inicial | Funcao |
|---|---|---|---|
| `FC11_HOLD` | BOOL | 0 | FC11 congelada enquanto a alimentacao esta cortada |
| `FC11_OUT_MEM` | REAL | 25.0 | Ultima saida boa da FC11 |
| `LC21_FF_GAIN` | REAL | 0.15 | Ganho do feedforward (% de P21 por hl/h de FT11) |
| `LC21_FF_ONS_ON` / `LC21_FF_ONS_OFF` | BOOL | 0 | Memorias dos ONS da transferencia sem tranco |

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

1. Abra um trend no RSLogix (100-200 ms) com `COLUMN_LT21`, `LC21.OUT`, `LC21.BIAS`, `INLET_FT11`,
   `FC11.OUT`, `FC11_HOLD` e `COLUMN_STOP_FEED`.
2. Com o Aldox em producao (passo 115), faca o toggle de `test_bits.1` para **1**.
3. O que esperar:
   - `LC21.BIAS` passa a ~67 % (a 450 hl/h). A saida da P21 nao deve dar tranco. Se der, desligue o
     bit e me avise.
   - Se a alimentacao for cortada, `LC21.BIAS` vai a 0 e a P21 desacelera na hora. `FC11_HOLD` liga e
     a `FC11.OUT` fica parada na ultima posicao boa.
4. Para voltar ao original, faca o toggle de `test_bits.1` para **0**.

## Ajustes depois do teste

- **`LC21_FF_GAIN`:** comece em 0,15. Se o nivel ainda sobe quando a vazao aumenta, suba ate ~0,19.
  Se a P21 ficar tremendo com o ruido do FT11, desca.
- **`LC21.KP` / `LC21.KI`:** so depois do feedforward funcionando. Suba o KP de 1,0 para 1,5 e depois
  2,0, e o KI de 0,005 para 0,01, um passo de cada vez (veja `ANALISE_ALDOX1_CONTROLE_NIVEL.md`).
- **Observacao:** durante o hold da FC11, o bit de manual da FC11 no supervisorio
  (`ALDOX_2_ADFM.BITS.2`) aparece ligado. Isso e esperado.
