# Equalização de Histograma — Resumo do Código

Arquivo: `equalizacao_histograma.py`

## Objetivo

Melhorar o **contraste** de uma imagem em tons de cinza. Imagens com pouco contraste têm os pixels concentrados em uma faixa estreita de níveis de cinza. A equalização **espalha** esses níveis por toda a faixa disponível (0 a 255), deixando o histograma mais uniforme.

A imagem usada é `img/resized-pout.jpg`, convertida para tons de cinza (`"L"`), ou seja, cada pixel é um valor inteiro entre 0 e 255.

---

## Passo a passo

O algoritmo é dividido em 4 funções, chamadas em sequência por `equalizar_histograma()`.

### 1. Montar o histograma — `montar_histograma(imagem)`

Conta **quantos pixels existem de cada nível de cinza**.

- Cria um vetor de 256 posições zerado (`NIVEIS = 256`).
- Percorre todos os pixels e soma 1 na posição correspondente ao seu valor.

```
histograma[k] = quantidade de pixels com intensidade k
```

### 2. Soma acumulada normalizada — `calcular_soma_normalizada(histograma, total_pixels)`

Duas etapas:

1. **Normaliza** o histograma dividindo pelo total de pixels → cada posição vira uma **probabilidade** `p(k)`.
2. **Acumula** essas probabilidades → obtém a função de distribuição acumulada (CDF):

```
soma_normalizada[k] = p(0) + p(1) + ... + p(k)
```

O resultado vai de próximo de 0 até exatamente 1. Ela diz "qual fração dos pixels tem intensidade ≤ k".

### 3. Criar a tabela de mapeamento — `criar_lookup_table(soma_normalizada)`

Transforma a CDF (valores entre 0 e 1) em novos níveis de cinza (0 a 255):

```
lut[k] = round(soma_normalizada[k] × 255)
```

A **LUT (lookup table)** é um "dicionário": para cada nível de cinza original `k`, ela informa qual será o novo valor.

### 4. Aplicar a tabela — `aplicar_lookup_table(imagem, lut)`

Percorre cada pixel da imagem e substitui seu valor pelo valor da LUT:

```
imagem_saida[i, j] = lut[imagem[i, j]]
```

---

## Fluxo geral

```
Imagem original
      │
      ▼
Histograma (contagem por nível)
      │
      ▼
Normalização + soma acumulada (CDF)
      │
      ▼
LUT = CDF × 255 (arredondado)
      │
      ▼
Substituição pixel a pixel → Imagem equalizada
```

---

## Visualização do resultado

Após equalizar, o código:

1. Calcula também o histograma da imagem equalizada.
2. Monta uma figura 2×2 com `matplotlib`:

| Imagem original | Histograma original |
|---|---|
| **Imagem equalizada** | **Histograma equalizado** |

3. Salva em `output/comparacao.png` (300 dpi).

> Observação: no início do script, se não houver interface gráfica (`DISPLAY`/`WAYLAND_DISPLAY` vazios), o backend `Agg` é usado para que o gráfico possa ser salvo em arquivo sem abrir janela.

---

## Intuição rápida

- Níveis de cinza **muito frequentes** fazem a CDF subir rápido → eles são "esticados" e ficam mais distantes entre si.
- Níveis **pouco frequentes** fazem a CDF subir pouco → acabam agrupados.
- Resultado: o histograma equalizado ocupa toda a faixa 0–255 e a imagem ganha contraste.

## Observação sobre implementação

O código usa laços `for` explícitos (em vez de operações vetorizadas do NumPy como `np.bincount` ou `lut[img]`) por motivo **didático**: deixa visível cada etapa do algoritmo, mas é mais lento em imagens grandes.
