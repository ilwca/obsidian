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
$$|E(G)|=m$$

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
$S'$ pode ser maximal e não ser máximo. Pode existir um outro conjunto $S''$ que contenha **ou** **não** $S'$ e que satisfaça a propriedade $P$.

### Revisando
Para um conjunto ser maximal ele deve:
- Atender a propriedade  $P$;
- Ser o **maior** conjunto a fazer isso para ser maximal e máximo;
### Minimal
De mesmo modo, denomina-se minimal um conjunto $S' \subset S$ de modo que $S$ atenda a propriedade $P$, e quando não existe um subconjunto $S''$ que também atenda à $P$ e que não seja $S''\supseteq S'$. De mesmo modo, $S'$ pode ser minimal e não ser mínimo.

### Revisando
Para um conjunto ser minimal ele deve:
- Atender a propriedade $P$;
- Ser o **menor** conjunto a fazer isso

Todos os problemas que envolvem maximizacao e minimizacao sao vistos de forma mais aprofundada em [[Grafos]].
## Corte de Vértices
por definição, o Corte de vértices é o conjunto mínimo de vértices a serem removidos de modo que o grafo fique desconexo.

## Corte de Arestas
por definição, é o conjunto mínimo de arestas que ao serem removidas geram um grafo desconexo.


## Componente Conexos
Componentes conexos são subgrafos maximais de $G$ 


---
# 26/03

## Grafos Planares
Um grafo $G$ é planar se e somente se atende a propriedade de $m\leq 3n-6$. como já vimos anteriormente, temos $|V(G)|=n$ e $|E(G)|=m$.

Como exemplo, os grafos $K_{3,5}$ e $K_5$ são planares?

Analisando $K_5$, temos que:
$|V(K_5)|=5$
$|E(K_{5})|=10$

aplicando na condição, temos que:
$$m\leq 3n-6$$
$$10\leq 3\cdot5-6$$
$$10\leq 9$$
como não atende a condição necessária, também não é suficiente.

Analisando $K_{3,3}$, temos que:
$|V(K_{3,3})|=6$
$|E(K_{3,3})|=9$
Aplicando na condição, temos que:
$$m\leq 3n-6$$
$$9\leq 3 \cdot 6 - 6$$
$$9\leq 12$$
Então, $K_{3,3}$ atende a condição necessária, **porém isso não é suficiente**
Pois para o grafo ser **planar** tem que atender também a propriedade:

$$2m\geq4(m-n+2)$$
$$2m\geq 4m- 4n + 8$$
==Resolver!!

## Grafo Bicoloríveis
se $G$ possui uma k-coloração, então o grafo é k-colorível.

## Ciclos Hamiltonianos
Um grafo é hamiltoniano se possui ciclo hamiltoniano. Ciclos hamiltonianos é um ciclo que sai de um grafo de origem, percorre todos os vértices e volta para o vértice original. 
$$v_1 \rightarrow v_2 \rightarrow v_3 \rightarrow v_1$$
## Grafos biconexos
Um grafo $G$ é biconexo se e somente se torna desconexo a partir da remoção de 2 vértices.

**Todo grafo biconexo é hamiltoniano, porém, nem todos biconexo é hamiltoniano**

## Grafos Direcionados
Até então, examinamos grafos não direcionados. Estes são compostos por conjuntos de arestas $E$, formado por arestas $e_i$ que são pares não ordenados, sendo $e_i(v,w) = e_i(w,v)$.
Porém em grafos direcionados, sendo conhecidos também por **Digrafos** as arestas possuem direção única, sendo $e_i(v,w) \neq e_i(w,v)$. pois agora as arestas são direcionadas.
$$v \rightarrow w$$
![[grafo-direcionado.png]]

Desta forma é justo pensar em graus de saída e graus de entradas, que são denotados como:
$d^+(v)$ = grau de saída
$d^-(v)$ = grau de entrada

### Grafo subjascente
Caso retiremos o sentido das arestas, teremos um grafo subjascente.
### Fracamente conexo 
