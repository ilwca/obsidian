# 1
Suponha que $\pi$ corresponde ao problema de ordenação de elementos alocados em um vetor, e que $A$ e um algoritmo ótimo de ordenação por comparação que resolve $\pi$. Nessas condições, e possível que exista um algoritmo $\pi '$, assintoticamente falando mais rápido que $\pi$ Explique.

**R:**
No aspecto mencionado, **Não** é possível existir outro algoritmo que seja melhor assintoticamente que um algoritmo ótimo, porem em outro âmbito seja possível, porém algoritmos de outro natureza podem performar melhor que um algoritmo ótimo de comparação. Como mencionado por Jayme, qualquer algoritmo que envolva comparação requer no pior caso complexidade $O(n\text{ }log \text{ } n)$.  Como o algoritmo $A$ é ótimo já pressupõe-se este complexidade em pior caso.

## 2
Como podemos encontrar as pontes de um grafo utilizando uma busca em profundidade e o conceito de demarcador?
**R:**
De forma direta, poderíamos fazer a localização de pontes por meio de algoritmos de busca em profundidade por meio da função $lowpt(v)$. Considere a arvore $T$ oriunda da aplicação de uma função de busca em profundidade em um grafo $G$. Uma ponde em $T$ poderia ser definida da seguinte forma: Caso existam vértices $v$ e $w$ onde $v$ é pai de $w$ e $lowpt(w)=w$. Pois, desta forma o único caminho entre $w$ e $v$ seria a aresta direta $(v,w)$. Ou seja, uma ponte.

## 3
Dado o Grafo da Figura 1, aplicar os Algoritmo de Prim e Kruskal e responder às perguntas a seguir. 
- As árvores geradoras encontradas por cada algoritmo são iguais? Se forem diferentes, elas tem pesos diferentes?
- A árvore gerada por ambos algoritmos é única?
- Qual é a diferença de execução entre os algoritmos citados?
**R:**
- As arvores geradas serão sempre diferentes, pela regra de seleção das arestas, a menos que o peso de todas as arestas seja distinto. Porem o peso total da soma do valor das arestas será sempre o mesmo pois nos dois algoritmos chegarão na arvore geradora mínima.
- Assim como na resposta anterior a arvore gerada pelos algoritmos só e única se todos os pesos das arestas dos  grafos fores distintas .
- A principal diferença entre os algoritmo é que o algoritmo de Prim cresce uma única arvore a partir de um ponto central, enquanto o de Kruskal fundo vários componentes isolados ate que eles formem uma única arvore.
## 4
Demonstrar que M é um emparelhamento máximo se, e somente se, G não possui caminho M-aumentante.
**R:**
"Um emparelhamento $M$ em um grafo $G$ é um emparelhamento perfeito se e somente se $G$ **não** contém caminho $M-aumentante$".

**Destrinchando o teorema...**
`M é perfeito` $\Longleftrightarrow$   `Não possui M-aumentante ` 
bicondicional, deve ser provada ida $(P\Rightarrow Q)$ e volta $(Q \Rightarrow P)$, que será feita da seguinte maneira:
$(P\Rightarrow Q)$ por contrapositiva. $(\rightharpoondown Q \Rightarrow \rightharpoondown P)$ 
$(Q \Rightarrow P)$ por contrapositiva $(\rightharpoondown P \Rightarrow \rightharpoondown Q)$

### $(\Rightarrow)$
$(\rightharpoondown Q \Rightarrow \rightharpoondown P)$ "se existe caminho aumentante em $M$, então, $M$ e não máximo"

Como existe um caminho aumentante, entao seja um caminho aumentante $P$ e um $M$ nao maximo.

Entao exite um matching $M'$ contendo a diferenca simetrica de $M$ e $P$
sendo $M\Delta P$:
Desta forma a diferença simétrica $\Delta = \{M \cup P\} - \{M \cap P \}$
### Exemplo da Operação
![[grafos-berge]]
$M=\{(2,3),(4,5),(7,8)\}\text{  }\text{  }\text{  }\text{  }|M|=3$
$P=\{1,2,3,4,5,6\}$
$M'=M - E(P) = \{(1,2), (3,4), (5,6), (7,8)\}\text{  }\text{  }\text{  } |M'|=4$

Percebe-se
$$|M'|> |M|$$
Assim provamos que $M$ não é máximo.

### $(\Leftarrow)$
se $M$ não e máximo então existe $M-aumentante$.
$(\rightharpoondown P \Rightarrow \rightharpoondown Q)$

Se $M$ não e máximo, vamos supor um $M^{*}$ que seja máximo.

Definimos o grafo $H$ como $H = G[M\Delta M^{*}]$

Como o grafo induzido $H$ é formado por dois emparelhamentos, por propriedade sabemos que **Um emparelhamentos não pode conter arestas que incidem sobre o mesmo vértice**.

Como temos 2 emparelhamentos induzindo um conjunto de vértices, o grau dos vértices tem que ser $d(v)\leq 2$. Ou seja, os vértices podem ter grau 0, 1 ou 2. Então cada componente conexas só pode ser um ciclo ou um caminho.
![[grados-ciclo-caminho.png]] Em ciclos, a diferença entre arestas alternantes é 0.
E como supomos que  $|M^{*}|>|M|$

Nestes tipos de componentes a diferença é 0, a menos que haja um caminho que comece em $M^{*}$ e termine em $M^{*}$
$$v_1 - M^{*} - v_2 - M - v_3 - M^{*} - v_{k}$$
Como os vértices de extremidade são insaturados por $M$.

Concluindo, para este caminho as arestas são:
- $M$ expostas no inicio.
- Alternam entre $M^{*}$ e $M$, ou seja, $M-alternante$
- Aresta $M$ exposta no final.

Ou seja, todas as propriedades de $M-aumentante$, então:
**$M$ não é máximo** $\Rightarrow$ Existe caminho aumentante para $M$.

## 5
"Seja $\alpha (G)$ a cobertura mínima e $\beta(G)$ o emparelhamento máximo. Provar que se $G$ é um grafo bipartido, então $\alpha (G) = \beta(G)$"
### Prova Direta
dado um grafo bipartido $G[X, Y ]$ e um emparelhamento máximo dado por $M^{*}$. 
Definimos $U$, como o conjunto de todos os vértices não saturados por $M^{*}$, e um $Z$ sendo o caminho $M-alternante$ dos vértices alcançados a partir de $U$.

Assim podemos criar dois conjuntos de vértices, sendo:
$$R = Z \cup X$$
$$B = Z \cup Y$$
ou seja, $R$ contém todos os vértices de $X$ alcançados por um caminho alternante $Z$ de origem em $U$.
e $B$ contém todos os vértices de $Y$ alcançados por um caminho alternante $Z$ de origem em $U$
Propomos uma cobertura candidata:
$$K^{*} = (X-R)\cup B$$
ou seja, todos os vértices de $X$ que não foram alcançados por $Z$ e todos os de $Y$ que foram.

**Por que $K^{*}$ cobre todas as arestas?**
Considere uma aresta $(x,y)$, se ela não estiver coberta por $K^{*}$, então $x\in R$ (alcançado) e $y\in B$ (não alcançado).
- Se $(x,y)$ estiver em $M^{*}$, $y$ teria sido alcançado a partir de $x$ pelo caminho alternante, logo $y\in B.$
- Se $(x,y)$ não estiver em $M^{*}$, o caminho que chega em $x$ poderia ser estendido ate $y$, logo $y\in B.$
Portanto, $K^{*}$ é uma cobertura.

**Por que $|K^{*}| = |M^{*}|$?**
- Não existe vértice saturado em $K^{*}$ que não seja saturado por $M^{*}$
- Cada aresta de $M^{*}$ toca $B$ e sua outra extremidade, esta em $R$ (portanto fora de $X-R$).
- E se não toca $B$ sua extremidade em $X$ deve estar em $X-R$.

Portanto construímos uma cobertura $K^{*}$, com o mesmo número de elementos do emparelhamento máximo $M^{*}$. E sabemos que não existe cobertura menos que $K^{*}$, portanto $K^{*}$ e cobertura mínima. logo...
$$\alpha (G) = \beta(G)$$
Esta provada para grafos bipartidos.

## 6
O algorirmo de Dijkstra é utilizado quando se deseja encontrar o caminho mínimo a partir de um vértice de origem para todos os demais vértices do grafo e funciona em grafos direcionados. O algoritmo é ineficaz em casos de grafos ponderados com arestas de pesos negativos.
O algoritmo de Bellman-Ford, assim como o de Dijkstra, busca caminhos a partir de uma única origem. No entanto, é a escolha ideal quando o grafo possui arestas com pesos negativos. Porém para a sua efetividade o grafo não pode conter ciclos de peso total negativo que sejam alcançáveis a partir da origem.
O algoritmo de Floyd é utilizado quando o objetivos é determinar o comprimento dos caminhos mínimos entre todos os pares de vértices do grafo. Assim como o de Bellman-Ford, exige que o grafo não possua ciclos de comprimento negativo.

| Algoritmo        | Pontos Positivos                                                                                                                                         | Pontos Negativos                                                                                                                   |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Dijkstra**     | Extremamente eficiente em grafos com pesos positivos. Com o uso de **filas de prioridade (heaps)**, atinge complexidade de $O(m\text{ } log \text{ } n)$ | Não funciona com pesos negativos. Se houver ciclos negativos, torna-se inútil.                                                     |
| **Bellman-Ford** | Consegue lidar com arestas de **peso negativo**. É capaz de **detectar a existência de ciclos negativos**                                                | Mais lento que o Dijkstra, com complexidade de $O(nm)$                                                                             |
| **Floyd**        | Resolve o problema de **todos para todos** em uma única execução. Implementação simples baseada em três laços aninhados                                  | Possui complexidade alta de $O(n³)$, o que pode ser pesado para grafos com muitos vértices, independentemente do número de arestas |
## 7
**Árvore de Caminhos Mínimos** (Raiz $v_2$) : As arestas da árvore ($v_{origem}$​→$v_{destino}​$) e as distâncias acumuladas do caminho mínimo são:
- $v_2​→v_1​$ (distância 13)
- $v_2​→v_3​$(distância 13)
    - $v_3​→v_8$​ (distância 22)
        - $v_8​→v_{11}$​ (distância 31)
    - $v_3​→v_4​$ (distância 24)
        - $v_4​→v_9$​ (distância 33)
            - $v_9​→v_10$​ (distância 44)
            - $v_9​→v_{12}​$ (distância 45)
        - $v_4​→v_5​$ (distância 36)

**Vértices Isolados** (Não alcançáveis por $v_2$​): Estes vértices não possuem predecessores na busca iniciada em $v_2​$:
- $v_6​$ (distância ∞)
- $v_7​$ (distância ∞)

## 8
Abaixo estão os valores finais de distância acumulada (d) e o predecessor (p) de cada vértice na árvore de caminhos mínimos:

| Vértice   | Distância Mínima (d) | Predecessor (p) | Caminho a partir de v2​               |
| --------- | -------------------- | --------------- | ------------------------------------- |
| $v_2​$    | **0**                | -               | (Origem)                              |
| $v_1$​    | **0**                | $v_2​$          | v2​→v1​                               |
| $v_3$​    | **1**                | v2​             | v2​→v3​ (ou via v2​→v1​→v10​→v8​→v3​) |
| $v_4$​    | **12**               | v3​             | v2​→v3​→v4​                           |
| $v_5​$    | **10**               | v4​             | v2​→v3​→v4​→v5​                       |
| $v_6$​    | **19**               | v4​             | v2​→v3​→v4​→v6​                       |
| $v_7$​    | ∞                    | -               | Não alcançável                        |
| $v_8$​    | **2**                | v10​            | v2​→v1​→v10​→v8​                      |
| $v_9$​    | **20**               | v5​             | v2​→v3​→v4​→v5​→v9​                   |
| $v_{10}$​ | **5**                | v1​             | v2​→v1​→v10​                          |
| $v_{11}$​ | **11**               | v8​             | v2​→v1​→v10​→v8​→v11​                 |
| $v_{12}$​ | **18**               | v5​             | v2​→v3​→v4​→v5​→v12​                  |
## 9
A matriz final abaixo apresenta o comprimento do caminho mínimo entre cada par de vértices $(i,j)$. 

|       | A     | B     | C      | D     |
| ----- | ----- | ----- | ------ | ----- |
| **A** | **0** | ∞     | **-1** | **3** |
| **B** | **1** | **0** | **0**  | **2** |
| **C** | **2** | ∞     | **0**  | **5** |
| **D** | **0** | ∞     | **-2** | **0** |
Dada a tabela de saída, com a presença de ∞  na coluna de $B$, podemos afirmar que nenhum outro vértices alcança $B$.
## Referencias
SZWARCFITER, Jayme Luiz. **Teoria computacional de grafos: Os Algoritmos**. Elsevier Brasil, 2018.