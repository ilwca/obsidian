Um grafo e denotado por um $G(V, E)$, que e um conjunto finito e não vazio de vértices, denotados por V. Dizemos que o grafo e trivial ou não orientado quando $|V|=1$.
Quando isso, o numero de vértices pode ser dado por: $V = \{v_1, v_2, v_3, . . ., n\}$.
O conjunto $E$, denota as arestas de G. Cada aresta $e \in E$, e é composta pelo par de vértices $e=(v,w)$ ou $e=(v_i , v_k)$. Neste caso, $v$ e $w$ estão nas extremidades das arestas, e são denominados **adjacentes**. Por fim, denotamos o conjunto de arestas como $E\{e_1, e_2, e_3, . . ., m\}$.

## Arestas
As vezes podemos encontrar alguns tipos exóticos de arestas que também são validas apesar de fugirem um pouco do conceito central, como quando existe uma aresta do tipo $e=(v, v)$, sendo chamada de **Laço** (a). Uma outra extensão que também é possível se chama **Arestas Paralelas** (b), que é quando temos duas arestas formadas pelo mesmo par de vértices, como na imagem a seguir:
![[tipo-aresta.png]]


## Grau
Denota-se o grau de um vértice (grua$(v)$), a quantidade de vértices adjacentes de um $v \in V$. Um grafo $G(V, E)$ tem grau regular de $r$, quando o grau de todos os vértices e igual a $r$. Um vértice que possui grau zero é chamado _isolado_.

---

# Caminho ou Passeio
Denominamos caminho ou passeio quando em uma sequencia de vértices, como $v_1, v_2, v_3, v_4$, é possível sair de $v_1$ e chegar a $v_4$ sendo ligado por arestas, exemplo:
$$v_1 \rightarrow v_2 \rightarrow v_3 \rightarrow v_4$$ Então, dizemos que $v_1$ *alcança* $v_4$, com um *comprimento* do caminho igual a 3. Pois, se o caminho envolve $k$ vértices, o comprimento é dado por $k-1$ que é o número de arestas, ou seja, o comprimento é a contagem de arestas e não dos vértices envolvidos. 

## Caminho simples ou Elementar
temos um *caminho* *simples* ou *elementar* quando o trajeto percorrido não envolve os mesmo vértices anteriores. Exemplo:
$$v_1 \rightarrow v_2 \rightarrow v_3 \rightarrow v_7$$
Desta forma, passamos por cada vértice uma única vez.

## Trajeto
No trajeto os vértices podem se repetir, porem, as aresta não. Exemplo:
$$v_2 \rightarrow v_3 \rightarrow v_7 \rightarrow v_6 \rightarrow v_2 \rightarrow v_1 \rightarrow v_5$$Percebe-se que $v_2$ aparece duas vezes, porem, por meio de arestas diferentes, sendo a primeira em $(v_2, v_3)$ e na outra por $(v_6, v_2)$ ou $(v_2, v_1)$.

## Ciclo
ciclos, são caminhos que contêm pelo menos 3 vértices e tem final no mesmo vértice de origem, por exemplo:
$$v_1 \rightarrow v_3  \rightarrow v_7 \rightarrow v_1 $$
Se o caminho for simples, o ciclo $v_1,...v_k,v_{k-1}$ também é denominado ciclo *simples* ou *elementar*.

## Caminho Hamiltoniano
Um caminho que passe por cada vértice do grafo exatamente uma vez é chamado de Hamiltoniano.
$$v_1 \rightarrow v_3 \rightarrow v_4 \rightarrow v_2$$
Note, que as arestas de $V(E)$ denominadas de $v_k$ não se repetem, sendo esta a propriedade essencial de um caminho Hamiltoniano .

## Caminho Euleriano
Diferentemente, um caminho ou ciclo que contenha *exatamente uma vez* cada *aresta* do grafo é denominado euleriano.
$$v_1 \rightarrow v_3 \rightarrow v_4 \rightarrow v_2$$
Nesta caso, o que deve ser exclusivo são as arestas do caminho ou ciclo $E(G)$, acima sendo representadas como "$\rightarrow$", mas também podem ser denotadas como $e_i$.

### Caminho Euleriano
Um **caminho euleriano** é **se e somente se** possui apenas **dois** vértices de grau ímpar. 
### Ciclo Euleriano
Enquanto um **ciclo é euleriano se não possuí vértices de grau ímpar**.

#### Teorema
"Um grafo $G$ conexo possui ciclo euleriano se e somente se todo vértice de $G$ possuir grau par"
#### Prova
Dado um grafo $G$ com todos o vértices de grau par:
- existe pelo menos um ciclo simples $C_1$.
- remove-se do grafo as arestas de $C_1$ (e ignora-se vértices isolados).
- O grafo restante continua tendo todos os vértices de grau par. _alguns casos, numero impares de arestas são removidas, mas os vértices continuam com grau par._
- Se ainda houver arestas, existe um novo ciclo simples $C_2$.
- Repete-se o processo ate que não reste nenhuma aresta.
- As arestas ficam particionadas em ciclos simples.
- Como o grafo original e conexo, esses ciclos compartilham vértices.
- Pela fusão sucessiva dos ciclos obtém-se um ciclo euleriano.


Se um grafo $G$ é euleriano e hamiltoniano ele e chamado de hamiltoniano e euleriano respectivamente.

## Distância
Denomina se distancia $d(v,w)$ entre dois vértices de um grafo ao comprimento do menor caminho entre $v$ e $w$. _conta somente de arestas!_

## Operações em Grafos
Em um grafo também é possível aplicar algumas operações. Seja um grafo $G(V, E)$, e uma aresta $e\in E$  Denota-se $G$ o grafo obtido de exclusão da aresta $e$. Se $v,w$ e um par de vértices não adjacentes em $G$, a notação $G+(v,w)$ representa o grafo obtida da criação da aresta ligando $v$ e $w$ Analogamente, dado um $v \in V$ um vértice de $G$, o grafo $G-v$  denota o grafo obtido pela remoção deste vértices e a todas as arestas a ele ligadas.
![[operacoes-grafos.png]]


## Complemento
Denomina-se *complemento* de um grafo $G(V,E$) ao grafo $\bar{G}$ , o qual possui o mesmo conjunto $V$ do que $G$, e tal que para todo par de vértices distintos $(v,w)\in V$, tem se que $(v,w)$ e aresta de $\bar{G}$ se e somente se $(v,w)$ não for de $G$.

## Grafo Completo
Um grafo e completo quando existe uma aresta entre cada par de seus vértices. Utiliza-se a notação $K_n$ para designar um grado completo com $n$ vértices. Ou seja, cada vértice desse grafo e ligado a todos os outros vértices desse grafo, desta forma, todos os vértices tem grau $n-1$.
![[grafro-completo.png]]

o numero máximo de arestas de um grafo com $n$ vértices e denotado como $(\frac{n}{2})$ ou seja $\frac{n(n-1)}{2}$ .
aplicando ao grafo $k_5$ teremos $\frac{5\cdot4}{2}= 10$.

## Grafo Bipartido
Um grafo é um grafo bipartido cujos vértices podem ser divididos em dois conjuntos separados. Ou seja onde $G(V,E)$ e $V$ pode ser dividido em $V_1$ e $V_2$. podendo tambem ser denotado como $G(V_1\cup V_2,E)$ 
$$V = V_1 \cup V_2$$

de modo que:
- todas as arestas ligam um vértice de $V_1$ a um vértice de $V_2$ _(em caso de um **bipartido Completo)_.
- **nenhuma aresta liga vértices dentro do mesmo conjunto**
Um grafo bipartido completo e denotado como $K_{n1,n2}$ e obviamente possui $n_1$ e $n_2$ arestas, sendo $n_1=|V_1|$ e $n_2=|V_2|$, como nas imagens a seguir.
![[grafo-bipartido.png]]
