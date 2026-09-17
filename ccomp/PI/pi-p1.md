# Prova 1 — Processamento de Imagens

**Disciplina:** Processamento de Imagens  
**Professora:** Glenda Botelho  
**Prova 1 (02/2025)**

---

## Questão 1 — Valor: 5

### 1.1 — Valor: 2,5 — POSCOMP 2016

No contexto de processamento de imagens, um filtro do tipo passa-baixa produz o seguinte resultado:

**A.** Realça os detalhes da imagem, produzindo um efeito de _sharpening_ (aumento da nitidez).

**B.** Realça as propriedades geométricas da imagem a partir de máscaras pré-definidas.

**C.** Suaviza as frequências dentro de um intervalo pré-determinado de valores.

**==D==.** Suaviza a imagem atenuando as altas frequências, que correspondem às transições abruptas.

**E.** Realça e suaviza de forma simultânea os componentes da imagem.

### 1.2 — Valor: 2,5 — POSCOMP 2010

Assinale a alternativa que indica a função de transformação $T(r)$ utilizada para se obter a imagem negativa de uma imagem monocromática, em que os pixels podem assumir valores no intervalo entre $0$ e $L-1$ e em que $r$ representa o valor do pixel na imagem original.

**==A==** $T(r) = (L - 1) - r$

**B.** $T(r) = -r$

**C.** $T(r) = c \log(1 + |r|)$, onde $c$ é uma constante de escala.

**D.** $T(r) = 1-r$

**E.** $T(r) = (L - 1)/r$

---

## Questão 2 — Valor: 10

Dada a imagem abaixo com $L=8$ níveis de cinza, calcule a **equalização do histograma**.

$$\begin{bmatrix} 0 & 0 & 0 & 0 & 1\\ 0 & 0 & 0 & 2 & 1\\ 0 & 2 & 2 & 1 & 1\\ 3 & 3 & 3 & 3 & 3 \end{bmatrix}$$

**R -**
$$\begin{bmatrix} 3 & 3 & 3 & 3 & 4\\ 3 & 3 & 3 & 5 & 4\\ 3 & 5 & 5 & 4 & 4\\ 7 & 7 & 7 & 7 & 7 \end{bmatrix}$$

---

## Questão 3 — Valor: 10

Assinale **V** para as respostas verdadeiras e **F** para as respostas falsas.

1. (F) A correção do _gamma_ é uma função de transformação de brilho, principalmente, de imagens que são exibidas em uma tela de computador.
    
2. (V) A resolução espacial de uma imagem (amostragem) envolve a quantidade de linhas e colunas utilizadas.
    
3. (V) A decomposição da imagem em _bit-planes_ pode ser muito útil para compressão de imagens.
    
4. (V) Duas regiões $R_1$ e $R_2$ serão adjacentes somente se todos os pixels de $R_1$ também pertencerem a $R_2$.
    
5. (V) Na quantização uniforme o espaço de cor é dividido em intervalos estocásticos definidos de acordo com a aplicação.
    
6. (V) Dois pixels são considerados conectados se forem vizinhos (N4, N8 e ND).
    
7. (V) A comparação do histograma de duas imagens é uma medida de similaridade que indica se as duas imagens são impressões visuais de uma mesma imagem.
    
8. (V) Existem duas classes de receptores de luz distribuídos pela superfície da retina, os cones com cerca de 75 a 150 milhões e os bastonetes com cerca de 6 a 7 milhões.
    
9. (V) As funções da transformação logarítmica são definidas pela equação:
    
s=clog⁡(1−r)s = c\log(1-r)

1. (V) Considerando dois pixels $p(x,y)$ e $q(s,t)$, a distância D4 (_City Block_) é dada pela equação:
    

$D4(p,q)=∣x−s∣+∣y−t∣D_4(p,q)=|x-s|+|y-t|$

---

## Questão 4 — Valor: 5

Defina **transformação pontual, local e global**.
**R -** Na transformacao pontual a cordenada de sair depende somente do valor do pixel de entrada. Na local, a cordenada de saida depende da vizinhanca do pixel de entrada. Na global a cordenada de saida depende de todos os pixels da imagem.

---

## Questão 5 — Valor: 10

Calcule a **ampliação bilinear** e a **redução por vizinho mais próximo**.

**Indique o tratamento que foi dado às bordas.**

Dada a imagem:

$$\begin{bmatrix} 10 & 100 & 110 & 40 & 80\\ 90 & 20 & 190 & 25 & 20\\ 50 & 210 & 220 & 190 & 150\\ 30 & 240 & 255 & 200 & 130\\ 140 & 110 & 150 & 60 & 90 \end{bmatrix}$$
**R -** 
$$\begin{bmatrix}55 &  91 & 50\\
132 & 216 & 140\\
115 & 105 & 75 \end{bmatrix}$$
