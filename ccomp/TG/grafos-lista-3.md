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


## Referencias
SZWARCFITER, Jayme Luiz. **Teoria computacional de grafos: Os Algoritmos**. Elsevier Brasil, 2018.