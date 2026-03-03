Um grafo e denotado por um $G(V, E)$, que e um conjunto finito e não vazio de vértices, denotados por V. Dizemos que o grafo e trivial ou não orientado quando $|V|=1$.
Quando isso, o numero de vértices pode ser dado por: $V = \{v_1, v_2, v_3, . . ., n\}$.
O conjunto $E$, denota as arestas de G. Cada aresta $e \in E$, e é composta pelo par de vértices $e=(v,w)$ ou $e=(v_i , v_k)$. Neste caso, $v$ e $w$ estão nas extremidades das arestas, e são denominados **adjacentes**. Por fim, denotamos o conjunto de arestas como $E\{e_1, e_2, e_3, . . ., m\}$.

## Arestas
As vezes podemos encontrar alguns tipos exóticos de arestas que também são validas apesar de fugirem um pouco do conceito central, como quando existe uma aresta do tipo $e=(v, v)$, sendo chamada de **Laço** (a). Uma outra extensão que também é possível se chama **Arestas Paralelas** (b), que é quando temos duas arestas formadas pelo mesmo par de vértices, como na imagem a seguir:
![[tipo-aresta.png]]


## Grau
Denota-se o grau de um vértice (grua$(v)$), a quantidade de vértices adjacentes de um $v \in V$. Um grafo $G(V, E)$ tem grau regular de $r$, quando o grau de todos os vértices e igual a $r$. Um vértice que possui grau zero é chamado _isolado_.

---

## Caminho ou Passeio
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

