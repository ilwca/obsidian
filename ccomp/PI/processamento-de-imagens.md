 
# Imagens, Visão

## Processo de formação de imagens no Olho humano
A Luz entra no olho pela córnea de acordo com o ajuste da íris e dilatação da pupila que define a quantidade desta luz que entra, assim a córnea recebe o estímulo de frequência visível e o cristalino ajuda com a projeção da imagem no fundo do olho, só que de forma invertida por conta de seu formato convexo. Por sua vez, a retina capta a projeção feita na parte interna do olho e decodifica as informações em sinais neurais para enviá-los ao cérebro.

## Luz
A luz é uma pequena parte do espectro eletromagnético, que é sensível às células fotorreceptoras presentes no olho humano, que são os cones e os bastonetes. Ou seja, é o espectro visível que pertence ao espectro eletromagnético que se propaga por meio de fótons que são percebidos pelo olho.
## Cor
A cor é definida pela frequência da onda recebida pelas cones. Assim, ondas de de 400 a 780 nanômetros de frequência são percebidas, variando do vermelho (menor frequência) ao violeta (maior frequência).

## Luminância
Intensidade de energia luminosa recebida na retina.

## Contraste
Influência da luminância de objetos vizinhos.

## Brilho
Luminância percebida influenciada pelo contraste.

## Bandas de Mach
Em bandas de Mach nosso sistema visual tende a alterar os níveis de intensidade de brilho em áreas de borda ou limites de regiões de intensidades diferentes.
## Inibição Lateral
A inibição lateral ocorre porque quando a informação chega a célula, a mesma comunica para sua proximidade, que a cor enxergada é o contrário, e quando a informação chega a periferia, está também passa a informação inversa, havendo assim um choque de informações, fazendo com que seja percebi o meio termo da informação.
## Contraste Simultaneo
O contraste simultâneo alega que o brilho percebido de uma figura ou superfície é afetado diretamente por sua proximidade, contexto ou background.
## Ilusão de Ótica
As ilusões de ótica são causadas por interpretações precipitadas do cérebro que ao receber a informação tenta preencher as lacunas com informações criadas, assim percebendo propriedades geométricas de objetos de maneira equivocada.

---

# Digitalização
Para ser efetuado o processo de digitalização, o alvo deve estar bem iluminado, entoa mecanismos como espelhos, lentes, filtros e sensores, fazem a cabeça de leitura. Esta é movida por todo o objeto para refletir a imagem deste por um espelho em ângulo para outro espelho. O último reflete a imagem para uma lente que foca a imagem através de um filtro no sensor CCD. O sensor CCD é composto por diodos fotossensíveis, que transformam brilho recebido em carga elétrica, mapeando todo o objeto e transformando o brilho refletido em elétrons

## Amostragem
É o processo de converter uma imagem contínua (do mundo real) em uma matriz discreta de pontos, definindo a resolução espacial por meio da quantização.
![[pi-amostragem.png]]

A quantidade de linhas e colunas que envolvem a amostragem de uma representacao real e a resolucao espacial da (amostragem) imagem.
## Vizinhanca-4 $N_4(p)$ 
Dado um pixel $P$ definido por $(x,y)$, sua vizinhança-4 é dada por :$\{(x+1,y), (x,y+1), (x-1,y), (x,y-1)\}$. sendo os pixels adjacentes horizontais e verticais.
## Vizinhanca Diagonal $N_D(p)$
á Vizinhança diagonal é, considerando o mesmo $P$, sua vizinhança diagonal seria $\{(x+1,y+1),(x+1,y-1),(x-1,y+1) , (x-1,y-1)\}$, ou seja, os pixels adjacentes diagonais.
## Vizinhanca-8 $N_8(p)$
A vizinhança de 8 é a junção de vizinhança-4 e diagonal. Para o mesmo $P$, temos $\{(x+1,y), (x,y+1), (x-1,y) (x+1,y+1),(x+1,y-1),(x-1,y+1),(x-1,y-1)\}$. Assim sendo, todos os pixels adjacentes a $P$.

---

# Interpolação
Interpolação é o processo de usar dados conhecidos para estimar valores em locais desconhecidos. Interpolação é extensivamente usada em tarefas como ampliação (zoom), redução, rotação e correções geométricas.

## Interpolação por
### Vizinho Mais Proximo
A **redução** é o processo de eliminação dos pixels proximos por meio da remoção de linhas ou colunas.
Na **ampliação** acontece inserindo colunas e linhas com indice 0. Exeemplo, na matrix  a seguir foram adicionadas a linha 1 e 3.
$$\begin{bmatrix} 1 & 3 & 5 & 6 & 1\\ 0 & 0 & 0 & 0 & 0\\ 7 & 2 & 5 & 4 & 1\\ 0 & 0 & 0 & 0 & 0 \end{bmatrix}$$
Em seguida os valores nulos recebem o vizinho mais proximo.
$$\begin{bmatrix} 1 & 3 & 5 & 6 & 1\\ 1 & 3 & 5 & 6 & 1\\ 7 & 2 & 5 & 4 & 1\\ 7 & 2 & 5 & 4 & 1 \end{bmatrix}$$
### Bilinear
Na **Redução** bilinear, considerando a imagem:
$$\begin{bmatrix} f(x,y) & f(x,y+1) \\ f(x+1,y) & f(x+1, y+1) \\ \end{bmatrix}$$
Ira gerar um unico pixel dado pela media dos 4, ou seja
$$\frac{f(x,y) + f(x,y+1) + f(x+1,y) + f(x+1, y+1)}{4}$$

Para a **Ampliação** Considerandoa imagem :

Considere os quatro pixels vizinhos:
$$
\begin{array}{ccc}
f(i,j) & a & f(i,j+1) \\[6pt]
b & c & d \\[6pt]
f(i+1,j) & e & f(i+1,j+1)
\end{array}
$$


Substitua os valores intermediários pelas seguintes expressões:

$$
a = \frac{f(i,j) + f(i,j+1)}{2}
$$

$$
e = \frac{f(i+1,j) + f(i+1,j+1)}{2}
$$

$$
b = \frac{f(i,j) + f(i+1,j)}{2}
$$

$$
d = \frac{f(i,j+1) + f(i+1,j+1)}{2}
$$

$$
c = \frac{
f(i,j) + f(i,j+1) + f(i+1,j) + f(i+1,j+1)
}{4}
$$
### Bicubica
A interpolaação bicubica é o metodo mais sofisiticado de interpolação, porém exige uma maior custo para o calculo. Na **Redução** é feita uma media de um quadrante 3x3, ou seja, a media de 9 pixels vizinhos. Assim como na bilinear, so que maior.
![[pi-bicubica.png]]

### Interpolação Bilinear — Acréscimo de linhas e colunas

Considere a seguinte disposição dos pixels:

$$\begin{bmatrix}
\begin{array}{ccc}
f(i,j) & f(i,j+1) & f(i,j+2) \\[6pt]
f(i+1,j) & f(i+1,j+1) & f(i+1,j+2) \\[6pt]
f(i+2,j) & f(i+2,j+1) & f(i+2,j+2)
\end{array}
\end{bmatrix}$$

Os novos valores são calculados pela média dos pixels vizinhos.
$$\begin{bmatrix}
\begin{array}{ccc}
f(i,j) & a & f(i,j+2) \\[6pt]
b & c & d \\[6pt]
f(i+2,j) & e & f(i+2,j+2)
\end{array}
\end{bmatrix}$$

### Valores intermediários

Para o ponto $a$:

$$
a =
\frac{
f(i,j) + f(i,j+1) + f(i,j+2)
}{3}
$$

Para o ponto $e$:

$$
e =
\frac{
f(i+1,j) + f(i+1,j+1) + f(i+1,j+2)
}{3}
$$

Para o ponto $b$:

$$
b =
\frac{
f(i,j) + f(i+1,j) + f(i+2,j)
}{3}
$$

Para o ponto $d$:

$$
d =
\frac{
f(i,j+1) + f(i+1,j+1) + f(i+2,j+1)
}{3}
$$

Para o ponto $c$, é calculada a média de todos os **9 pixels**:

$$
c =
\frac{
\begin{aligned}
&f(i,j) + f(i,j+1) + f(i,j+2) \\
&+ f(i+1,j) + f(i+1,j+1) + f(i+1,j+2) \\
&+ f(i+2,j) + f(i+2,j+1) + f(i+2,j+2)
\end{aligned}
}{9}
$$
---
# Quantização
Como tambem utilizado em tecnicas de compressão de redes [[pg1-notas#Quantização |quantização]]. Imagine que temos um problema. Precisamos representar uma imagem que possui 256 niveis de cinza para um espaco que contem apenas 2 niveis. Uma solução possivel seria:
```
para todo pixel da imagem

for x in weigth
	for y in heigth
		if f(x,y) < 127
			f'(x,y) = 0
		else
			f(x,y) = 255
``` 

Ou seja, se o valor do pixel for menor que 127, passas aser 0 agora, se for maior, passa a ser 255.

O valor do numero de niveis, representado por $L$ deve ser sempres um inteiro potência de 2:
$$L=2^k$$
Assim os numeros entre o invervalo quantizado, devem ser espacados de forma igual. no intervalo $[0,...,L-1]$ .

### Representação Digital
A represendação digital de uma imagem é dada pela sua quantidade de bits que define a quantidade de cores nela presente. Quando dito que uma imagem é de 8 bits, significa que ela possui $2⁸$ cores. Se $n$ for a quantidade de bits de uma imagem, sua quantidade de cores pode ser denotada por:
$$n\ bits=2^ncores$$ ---
# Criterios de Conectividade entre Pixels
Dois pixels estao conectasdos se:
- Sao vizinnhos. Isto é [[#Vizinhanca-4 $N_4(p)$ |N4]], [[#Vizinhanca-8 $N_8(p)$| N8]] ou [[#Vizinhanca Diagonal $N_D(p)$| Nd]].
- Seus niveis de cinza satisfazem algum criterio de similaridade. (Isto é, se os niveis de cinza são proximos)
### Tons de Cinza
Um pixel $p(x,y)$ pertence a um conjunto $V$, se seu valor estiver contido no cojunto.
$V={80,85,90,95,100,120,125}$
Ou no caso de uma imagem binaria com 0 e 1
$V={1}$

## Adjacencia entre pixels
tipos de adjacencia:
- 4-adjacencia
- 8-adjacencia
- M-adjacencia

### 4-Adjacencia
Dois pixels $p$ e $q$ com valores de tom de cinza em $V$, sao 4-adjacentes se $q\in N_4(p)$. Ou seja, deve se atender os DOIS criterios, o de Vizinhanca e o de Ton de Cinza. Exemplo:
$V={1}$
$q\in N_4(p)$

### 8-Adjacencia
Dois pixels $p$ e $q$ com valores de tom de cinza em $V$, sao 8-adjacentes se $q\in N_8(p)$. Ou seja, deve se atender os DOIS criterios, o de Vizinhanca e o de Ton de Cinza. Exemplo:
$V={1}$
$q\in N_8(p)$

### M-Adjacencia
m-conectados se satisfazem $Cs$ e
1. $q\in N_4(p)$ ou
2. $q\in N_D(p)\ e\ N_4(p)\bigcap N_4(q)\ é\ vazio$. 
Ou seja, um pixel $q$ em relação a $p$ só é $m-adjacente$ se ele for 4-adjacente ou for D-adjacente e a 4-vizinhanca de p e a 4-vizinhanca de q, não possuem pixels em comum.

## Conectividade
Considerando agora um subconjunto $S$ de pixels em uma imagem, dois pixels $p$ e $q$ são conectados em $S$ se todos os pixels do caminho entre $p$ e $q$ tambem estao contidos em $S$.

O conjunto $S$ pode conter uma ou mais regiões. Estas regiões podem ser adjacentes.
### Regiões
Seja $R$ um subconjunto de pixels, $R$ é uma região, se:
- $R$ é um subconjunto conectado.
- Sua borda ou contorno, é um subconjunto de pixels, onde cada pixel deve conter pelo menos um pixel fora do conjunto.

---
# Distância
Metricas de distancia entre pixels podem ser medidos por formas diferentes. Considerando pixels $p(x,y)$ e $q(v,w)$. podemos calcular a distancia entre eles por:
### Distancia Euclidiana
$$D_e(p,q)=\sqrt{(x-v)²+(y-w)²}$$
### Distancia City-Block (Distancia $D_4$)
$$D_{cb}(p,q)=|x-v|+|y-w|$$
### Distancia ChessBoard(Distancia $D_8$)
$$D_{ch}(p,q)=max(|x-v|,|y-w|)$$
---
# Dominio Espacial
Refere-se ao proprio plano da imagem.
Por meio dos **Metodos** e feito a manipulacao diretamento nos pixels de uma imagem

## Metodos
Os principais metodos de intensidade sao:
- Transformacao de itensidade
- Filtragem Espacial
### Transformacao de Itensidade
Operam diretamento nos pixels de uma imagem, para fins de manipulacao de contraste e limiarizacao da imagem.
### Filtragem Espacial
Trabalham diretamente na vizinhanca de cada pixel, em operacoes como o realce de imagens.

## Funcoes de transformacao de Itensidade
Podem ser clasificadas como:
### Pontual
Quando o valor de saida na coordenada, depende somente do valor de entrada da mesma cordenada.
### Local
Quando o valor de saida de uma cordenada depende dos valores da vizinhanca desta cordeanda.
### Global
Quando o valor de saida especificada depende de todos os valores de entrada da imagem.