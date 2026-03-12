# 26/02


**O que é um problema fácil em computação**: problemas resolvidos em tempo polinomial, ou seja, de complexidade conhecida. Das mesma forma, um problema difícil é um problema que é resolvido em tempo exponencial.

## Grafo
Um **Grafo** é qualquer conjunto de vértices ligados por arestas, modelando relações entre objetos.
Portanto, um grafo pode ser denotado por G=(V, E), sendo:

**G** → grafo
**V** → Conjunto de vértices. ex:  $\{v_1, v_2, v_3,..., n\}$
**E** → Conjunto de Arestas. ex: $\{e_1, e_2, e_3,..., m\}$


portanto, definimos a cardinalidade, dos vértices de um grafo como:
$$|V(G)| = n$$
e de mesmo modo para o conjunto de Arestas.
$$|E(G|=m$$

considerando o grafo:
![[5-star.png]]




## Grafo atravessável
um grafo é atravessável, se e somente se, contêm somente **dois** vértices de paridade ímpar.
Em todo grafo, a quantidade de vértices de grau impar é sempre par!

## Grafo Euleriano
um grafo é euleriano, quando o vértice de origem e de destino são os mesmo e **todos** os vértices contem grau par.

# Grau do Vértice

---
# 05/03

---
# 12/03

## Grafos Caminho $P$
um grafo caminho denotado como $P_n$ é um grafo com $n$ vértices e $n-1$ arestas.
$P_1$ 
$$\cdot$$
$P_2$
$$\cdot \rightarrow \cdot$$
$P_3$
$$\cdot \rightarrow \cdot \rightarrow \cdot$$
## Grafos Ciclo $C_n$

Grafo que contem $n$ vértices e $n$ arestas que formam um caminho.

## Grafos Roda $W_n$
Grafos $W_n$ que contem um ciclo simples e um vertice universal que tem grau $n-1$, portanto, $E(W_n)=(n-1)(n-1)$ .
![[Wheel_graphs.svg]]



## Grafos Estrela $k-sum$
Grafos que seu núcleo tem possui um grafo completo de tamanho $k_n$.


## Clique
Denomina-se clique de um grafo $G$, um subgrafo de $G$ que seja completo.
![[]]



## Problemas Computacionais
Os problemas computacionais podem ser classificados em tres tipos:
- Localização
- Decisão
- Otimização

Os problemas de **Otimização** podem derivar em mais dois subproblemas
### Otimização
- Maximização
- Minimização

## Conjuntos Minimal e Maximal
Seja um conjunto $S'\subset S$. Diz-se que $S'$ e maximal em relação a uma certa propriedade $P$.

### Maximal
maximal é denotado pelo conjunto $S' \subset S$ de modo que $S$ atenda a propriedade $P$, e quando não existe um subconjunto $S''$ que também atenda à $P$ e que não seja $S''\supseteq S'$,. Ou seja, $S'$ deve ser o **maior** conjunto possível que atenta a $P$ para ser maximal.  

Então, caso exista um $S' \subseteq S''$ que seja máximo.

### Minimal
De mesmo modo, denomina-se minimal um conjunto $S' \subset S$ de modo que $S$ atenda a propriedade $P$, e quando não existe um subconjunto $S''$ que também atenda à $P$ e que não seja $S''\supseteq S'$

## Corte de Vértices
por definição, o Corte de vértices é o conjunto mínimo de vértices a serem removidos de modo que o grafo fique desconexo.

## Corte de Arestas
por definição, é o conjunto mínimo de arestas que ao serem removidas geram um grafo desconexo.


## Componente Conexos
Componentes conexos são subgrafos maximais de $G$ 