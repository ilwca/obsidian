Um grafo e denotado por um $G(V, E)$, que e um conjunto finito e não vazio de vértices, denotados por V. Dizemos que o grafo e trivial ou não orientado quando $|V|=1$.
Quando isso, o numero de vértices pode ser dado por: $V = \{v_1, v_2, v_3, . . ., n\}$.
O conjunto $E$, denota as arestas de G. Cada aresta $e \in E$, e é composta pelo par de vértices $e=(v,w)$ ou $e=(v_i , v_k)$. Neste caso, $v$ e $w$ estão nas extremidades das arestas, e são denominados **adjacentes**. Por fim, denotamos o conjunto de arestas como $E\{e_1, e_2, e_3, . . ., m\}$.

## Arestas
As vezes podemos encontrar alguns tipos exóticos de arestas que também são validas apesar de fugirem um pouco do conceito central, como quando existe uma aresta do tipo $e=(v, v)$, sendo chamada de **Laço** (a). Uma outra extensão que também é possível se chama **Arestas Paralelas** (b), que é quando temos duas arestas formadas pelo mesmo par de vértices, como na imagem a seguir:
![[tipo-aresta.png]]


## Grau
Denota-se o grau de um vértice (grau$(v)$), a quantidade de vértices adjacentes de um $v \in V$. Um grafo $G(V, E)$ tem grau regular de $r$, quando o grau de todos os vértices e igual a $r$. Um vértice que possui grau zero é chamado _isolado_. Desta forma denotamos:
$\delta(G) \rightarrow$ Grau mínimo de $G$.
$\Delta(G)\rightarrow$ Grau máximo de $G$.

### Formas de Representação
Grafos podem ser representados por diversas formas, como:
- Vetores
- Matrizes (Adjacência, LaPlaciana)
- Listas encadeadas (de adjacência)

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

## Caminho Hamiltoniano
Um caminho que passe por cada vértice do grafo exatamente uma vez é chamado de Hamiltoniano.
$$v_1 \rightarrow v_3 \rightarrow v_4 \rightarrow v_2$$
Note, que os vértices $V(G)$ denominadas de $v_k$ não se repetem, sendo esta a propriedade essencial de um caminho Hamiltoniano .

## Ciclo
ciclos, são caminhos que contêm pelo menos 3 vértices e tem final no mesmo vértice de origem, por exemplo:
$$v_1 \rightarrow v_3  \rightarrow v_7 \rightarrow v_1 $$
Se o caminho for simples, o ciclo $v_1,...v_k,v_{k-1}$ também é denominado ciclo *simples* ou *elementar*.

Grafos ciclo são denotados por $C_n$ onde $n$ é o numero de arestas que compõem aquele ciclo.

### Ciclo Hamiltoniano
Um ciclo é um caminho denotado por $C$ de modo que  $C \subseteq V$, onde cada vértice é visitado somente uma vez, o vértice de destino é igual ao vértice de origem, ou seja, $v_1 = v_k$, onde $k \geq 3$. exemplo:
$$v_1 \rightarrow v_2 \rightarrow v_3 \rightarrow v_1$$

## Caminho Euleriano
Diferentemente, um caminho ou ciclo que contenha *exatamente uma vez* cada *aresta* do grafo é denominado euleriano.
$$v_1 \rightarrow v_3 \rightarrow v_4 \rightarrow v_2$$
Nesta caso, o que deve ser exclusivo são as arestas do caminho ou ciclo $E(G)$, acima sendo representadas como "$\rightarrow$", mas também podem ser denotadas como $e_i$.

Um **caminho euleriano** é **se e somente se** possui apenas **dois** vértices de grau ímpar. No caso acima, percebe-se que somente $v_1$ e $v_2$  possuem grau impar e o restante par. 
### Circuito Euleriano
Um **ciclo é euleriano se não possuí vértices de grau ímpar**. Ou seja, todos os vértices tem grau par.
![[grafo-C-euleriano.png]]
Este é um exemplo de um grafo que possui **ciclo euleriano** e **não possui ciclo hamiltoniano**, devido a repetição do vértice 3.
#### Teorema
"Um grafo $G$ conexo possui ciclo euleriano se e somente se todo vértice de $G$ possuir grau par"
#### Prova
Dado um grafo $G$ com todos o vértices de grau par:
- existe pelo menos um ciclo simples $C_1$.
- remove-se do grafo as arestas de $C_1$ (e ignora-se vértices isolados).
- O grafo restante continua tendo todos os vértices de grau par. _(alguns casos, numero impares de arestas são removidas, mas os vértices continuam com grau par.)_
- Se ainda houver arestas, existe um novo ciclo simples $C_2$.
- Repete-se o processo ate que não reste nenhuma aresta.
- As arestas ficam particionadas em ciclos simples.
- Como o grafo original e conexo, esses ciclos compartilham vértices.
- Pela fusão sucessiva dos ciclos obtém-se um ciclo euleriano.

Se um grafo $G$ é euleriano e hamiltoniano ele e chamado de hamiltoniano e euleriano respectivamente.

## Grafo Atravessável
Um grafo é atravessável se e possível percorrer todas as suas arestas exatamente uma vez. Isso só é possível se todos os vértices tem grau par ou exatamente dois vértices tem grau par.
## Distância
Denomina se distancia $d(v,w)$ entre dois vértices de um grafo ao comprimento do menor caminho entre $v$ e $w$. (se tratando de arestas), Ou seja, quantas arestas há de $v$ a $w$.

## Operações em Grafos
Em um grafo também é possível aplicar algumas operações. Seja um grafo $G(V, E)$, e uma aresta $e\in E$  Denota-se $G$ o grafo obtido de exclusão da aresta $e$. Se $v,w$ e um par de vértices não adjacentes em $G$, a notação $G+(v,w)$ representa o grafo obtida da criação da aresta ligando $v$ e $w$ Analogamente, dado um $v \in V$ um vértice de $G$, o grafo $G-v$  denota o grafo obtido pela remoção deste vértices e a todas as arestas a ele ligadas.
![[operacoes-grafos.png]]


## Complemento
Denomina-se *complemento* de um grafo $G(V,E$) ao grafo $\bar{G}$ , o qual possui o mesmo conjunto $V$ do que $G$, e tal que para todo par de vértices distintos $(v,w)\in V$, tem se que $(v,w)$ e aresta de $\bar{G}$ se e somente se $(v,w)$ não for de $G$. 
## Grafo Completo
Um grafo e completo quando existe uma aresta entre cada par de seus vértices. Utiliza-se a notação $K_n$ para designar um grafo completo com $n$ vértices. Ou seja, cada vértice desse grafo e ligado a todos os outros vértices desse grafo, desta forma, todos os vértices tem grau $n-1$.
![[grafro-completo.png]]

o numero máximo de arestas de um grafo com $n$ vértices e denotado como $(\frac{n}{2})$ ou seja $\frac{n(n-1)}{2}$ .
aplicando ao grafo $k_5$ teremos $\frac{5\cdot4}{2}= 10$.

## Grafo Bipartido
Um grafo é um grafo bipartido cujos vértices podem ser divididos em dois conjuntos separados. Ou seja onde $G(V,E)$ e $V$ pode ser dividido em $V_1$ e $V_2$. podendo também ser denotado como $G(V_1\cup V_2,E)$ 
$$V = V_1 \cup V_2$$
de modo que:
- todas as arestas ligam um vértice de $V_1$ a um vértice de $V_2$ _(em caso de um **bipartido Completo)_.
- **nenhuma aresta liga vértices dentro do mesmo conjunto**
Um grafo bipartido completo e denotado como $K_{n1,n2}$ e obviamente possui $n_1$ e $n_2$ vértices, sendo $n_1=|V_1|$ e $n_2=|V_2|$, como nas imagens a seguir.
![[grafo-bipartido.png]]
Na imagem acima temos um grafo bipartido completo $K_{2,3}$, que se a notação de $K_{|V_1|,|V_2|}$.
### Teorema 
Um grafo $G$ é bipartido, se e somente se, $G$ não possui ciclo de tamanho ímpar.

---
## Problemas Computacionais
Os problemas computacionais podem ser classificados em três tipos:
- Localização
- Decisão
- Otimização

Os problemas de **Otimização** podem derivar em mais dois subproblemas
### Otimização
- Maximização
- Minimização

# Conjuntos Minimal e Maximal
Seja um conjunto $S'\subset S$. Diz-se que $S'$ e maximal em relação a uma certa propriedade $P$.

### Maximal
maximal é denotado pelo conjunto $S' \subset S$ de modo que $S$ atenda a propriedade $P$, e quando não existe um subconjunto $S''$ que também atenda à $P$ e que não seja $S''\supseteq S'$,. Ou seja, $S'$ deve ser o **maior** conjunto que atenta a $P$ para ser maximal.
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

### Lembrando:
- **minimal** → remover qualquer vértice faz perder $P$.
- **maximal** → não é possível adicionar vértices sem perder $P$.


# Problemas de Maximização e Minimização
Os problemas a seguir são problemas de minimização ou de minimização
- [[#Conjunto Dominante]]
- [[#Conjunto Independente]]
- [[#Clique]]
- [[#Corte de Vértices]]
- [[#Corte de Arestas]]
- [[#Emparelhamento]]
- [[#Cobertura por Vértices]]

## Conjunto Dominante
Um conjunto $S$ é considerado dominante se todas os vértices estão em $S$ ou todo vértice tem um vizinho contido em $S$.

## Conjunto Independente
Um par de vértices (se houver) é independente se e somente se não são adjacentes, ou seja, não possuem arestas entre si.
Por definição temos que:
$$\forall v,w \in S, (v,w)\notin E$$
Ou seja, para todos os vértices de $S$, eles são independentes se não houver arestas entre eles, **caso haja dois vértices**, pois um conjunto unitário também e independente.
pois caso $S=\{v\}$ esta atendendo a propriedade de independência. 
de mesmo modo se $S=\{w\}$, $S$ também atende a propriedade de independência.

# Clique
Uma clique e um subconjunto de um grafo $G$ de modo que este subconjunto seja um [[#Grafo Completo]]. Assim como no conjunto $\{2, 3, 4, 6\}$ do grafo (a) da imagem a seguir.
![[grafo-complemento.png]]
O conjunto citado forma uma clique de tamanho 4, ou seja, esta é a cardinalidade deste conjunto.

## Corte de Vértices
Seja um grafo $G(V,E)$ conexo. O corte de vértices de $G$ é um subconjunto minimal de vértices $V' \subseteq V$ cujo sua remoção de $G$, causa a desconexão de $G$, tornando-o um grafo desconexo.
ou seja, a operação mínima qualquer que seja **relacionada a um vértice** sendo $V'-G$ tornando $G$ desconexo e denominada de corte de vértices.
Exemplo, ao excluir os vértice 1 em $\bar{G}$ aumenta seu numero de componentes para 3. se desconsiderarmos o vértice 6, a principio, isso tornaria o grafo desconexo, atendendo a definição, pois criaríamos mais um componente ao grafo, que seria o vértice 4. desta forma, teríamos os componentes $\{2,3,5\}$ e $\{4\}$. Este problema esta relacionado a [[#conectividade]].

## Corte de Arestas
Analogamente ao Corte de vértices, para um grafo $G$, exista um conjunto minimal de arestas $E'$ de modo que $G-E'$ causando a desconexão de $G$. Ou seja, a operação minimal qualquer que seja relacionada a uma vértice. por exemplo, se considerarmos o grafo da figura 2.7(a).
$$E'=\{(5,6), (5,4)\}$$
Este seria um conjunto minimal de corte de arestas.
$$E'=\{(4,5), (4,6), (4,2), (4,3)\}$$
Este também seria um conjunto minimal de corte de arestas com relação ao vértice 4.

## Emparelhamento
 Sega um grafo $G$, emparelhamento e um conjunto de arestas com extremidades distintas duas a duas em que não possuem vértices em comum.

## Cobertura por Vértices
dado um grafo $G(V, E)$, a cobertura por vértices consiste em um subconjunto de vértices $C \subseteq V$, de modo que cara aresta tenha extremidade em um vértice de $C$, sempre buscando a cardinalidade mínima do conjunto.

![[6n-graf.svg.png]]


Considerando o grafo acima, buscamos um conjunto minimal de $S$ que cubra todos os vértices de $V$. Assim, podemos propor:
$$C_1=\{4,2\}$$
ou 
$$C_2=\{4,1\}$$

a seguir, exercícios envolvendo maximal e minimal...

---
# Exercícios 
## Ex.1 Conjunto Independente

Considere o grafo $G$ que visualmente ele seria algo assim:
```
A ----- B  
 \    /  
   C ----- D ----- E
```
A propriedade PPP será:

$P(S):S$ eˊ um conjunto independente.

ou seja, **nenhum par de vértices de $S$ possui aresta entre si**.

Analise os conjuntos abaixo.

### Conjuntos candidatos
-  $S_1 = \{A,D\}$
- $S_2 = \{B,E\}$    
- $S_3 = \{A,D,E\}$
- $S_4 = \{B,D\}$

### Perguntas

Para cada conjunto:
- Ele satisfaz a propriedade $P$?  
- Ele é **minimal**?  
- Ele é **maximal**?

### Resposta

-  $S_1 = \{A,D\}$ $\rightarrow$ satisfaz $P$ e maximal 
- $S_2 = \{B,E\}$ $\rightarrow$ satisfaz $P$ e maximal
- $S_3 = \{A,D,E\}$ $\rightarrow$ **não** satisfaz $P$.
- $S_4 = \{B,D\}$ $\rightarrow$ satisfaz $P$ e maximal
## Ex.2 — Conjunto Dominante

Agora considere a propriedade:

$P(S):S$ eˊ um conjunto dominante
ou seja:

todo vértice **está em $S$** ou é **vizinho de algum vértice de $S$**.z
### Pergunta
Encontre **um conjunto dominante minimal**.

### Resposta
conjuntos dominantes:
$S_1=\{C, E\}$
$S_2=\{D, A\}$
$S_3=\{D, B\}$


## Ex3. 
Dado um grafo $G(V,E)$, visualmente :
![[grafo-isomorfo.png]]



---

# Árvore
Denomina-se arvore $T(V, E)$ um grafo conexo e acíclico. Se um vértice deste grafo possui grau $\leq 1,$ então $v$ e uma folha. Caso contrario, $v$ e um vértice interior.

Caso o grafo  $T$ seja desconexo e acíclico, este é uma floresta. Pode-se provar por indução que toda arvore com $n$ vértices, possui $n-1$ arestas.

### Caracterização
Um grafo $T$ é uma arvore, se e somente se, existe somente um único caminho entre cada par de vértices. Esta é uma das caracterizações de uma arvore, pois ela pode ser caracterizada como:
- $G$ é uma arvore
- $G$ é conexo e $|E(G)|$ e mínimo
- Existe somente um caminho entre cada par de vértices de $G$
- $G$ e acíclico é $|E(G)| = |V|-1$
- $G$ e conexo é $|E(G)| = |V|-1$
- A adição de uma aresta em $G$ gera somente um ciclo.
## Centro
A _excentricidade_ de um vértice $v \in V$ é a distancia máxima entre este e qualquer outro $w \in V$. É denominado o _centro_ do grafo, o conjunto de $v \in V$ de excentricidade mínima.

## Subgrafo Gerador
Dado um grafo $G$, o subgrafo gerador é denotado por $G_1(V_1, E_1)$ de modo que $V_1 = V$ onde $E_1$ é o conjunto mínimo de arestas que mantenha $G_1$ conexo. Quando $G_1$ é uma arvore, este pode ser denotado como [[#Árvore Geradora]].
## Árvore Geradora
considerando um grafo $G$ conexo, para a obtenção de uma arvore geradora, considera-se um $e$ de modo que $G-e$ seja conexo. A repetição desta subtração ate que não haja mais $e$ que seja possível subtrair de $G$ de modo que esta ainda seja conexo, origina uma **arvore geradora**.
Ou seja, a arvore geradora e a versão mínima de arestas de $G$ que ainda o mantêm conexo.

## Conectividade
A conectividade esta diretamente relacionada ao [[#Corte de Vértices]] e o [[#Corte de Arestas]], que, dado um grafo $G$ consistem em um conjunto minimal de vértices e arestas $V'$ e $E'$ de modo que $G-V'$ ou $G-E'$ cause a desconexão de $G$.
**Conectividade de vértices** denotado por $c_v$ , consiste no corte de menor cardinalidade em $G$ que gere um grafo desconexo ou trivial.
**Conectividade de Arestas** analogamente ao corte de vértices é o $c_e$ sendo o conjunto de arestas de cardinalidade mínima que cause a desconexão ou trivialidade de $G$.
Para todo grafo vale que $c_v \leq c_e$, , ou seja, o número do corte de vértices, sempre será menor ou igual ao numero do corte de arestas.

Um grafo $G$ é _**k-conexo**_  em vértice ou arestas quando $k$ é o numero mínimo de cortes (respectivo a arestas ou vértices) para a desconexão de $G$. Ou seja, não existe corte de vértices < $k$ para um grafo _k-conexo_. De mesmo modo, não existe um corte de arestas < $k$ para um grafo _k-conexo_.


---
# Planaridade
 seja $G$ um grafo e $R$ a representação geométrica de $G$ em um plano $P$. A representação $R$ e chamada *plana* quando não a interseção entre os vértices, a não ser que seja por meio de uma aresta. Deste modo, um grafo é planar quando for *plano*.
 ![[grafo-planar.png]]
Tomando como exemplo o grafo $K_4$ acima, temos que a figura (a) não e plana, pois há um cruzamento de arestas. Por outro lado o grafo isomorfo apresentado em (b) e (c) é planar.

Percebe-se que cada ciclo (normalmente de cardinalidade 3) em $K_4$ gera um $f$ , como representado em (b). Cada aresta é divida entre dois planos e cada plano, está limitado por no mínimo 3 arestas exceto a face externa.

**Todo grafo planar** atende a condição $n+f=m+2$, sendo assim também conhecida pela formula de Euler como $n-m+f = 2$.
### Formula de Euler
A formular de Euler e usada para manipulação e descobrimento de número de faces, arestas ou vértices de um grafo completo. **O número de faces** pode ser denotado como:
$$f=m-n+2$$

### Grafo $K_n$ Planar
Deste modo, observa-se que  quanto maior a quantidade de arestas de um grafo, mais difícil e atender a condição de planaridade. Então, de fato, existe um numero máximo de aresta de um grafo planar, dado pelo seguinte lema:

Seja um grafo planar. Então $m\leq 3n-6$.

Isso e dado pela condição de que cada face e delimitada por no mínimo 3 arestas, e cada aresta pertence a exatamente duas faces.
![[Excalidraw/grafos-planaridade|grafos-planaridade]]

Como cada aresta esta em dois planos $f$, ela sempre e contada 2x, como mostra na imagem acima na descrição de cada face. por isso $2m$.
Percebe-se também, que o numero total de arestas das faces e de $12$. resultado que pode ser descrito como 3x o numero de faces. Por isso $3f$.
Deste modo, temos a notação $2m\leq3f$.

Aplicando na formula de Euler:
$$f=m-n+2\Rightarrow \frac{2}{3}m \geq m-n+2 \Rightarrow m \leq3n-6$$
Por isso o número de arestas de um grafo planar e delimitado por:
$$m\leq3n-6$$
### Grafo $K_{i,j}$ Planar
Diferente de uma grafo planar completo, em um [[#Grafo Bipartido]] seu menor ciclo tem tamanho 4. Ou seja, cada plano $f$ é delimitado por no mínimo 4 arestas e sempre um numero par de arestas. Além disso, cada aresta pertence exatamente a duas faces. logo:
$$2m\geq4f$$ ---
# Grafos Direcionados (Digrafos)
Até então, examinamos grafos não direcionados. Estes são compostos por conjuntos de arestas $E$, formado por arestas $e_i$ que são pares não ordenados, sendo $e_i(v,w) = e_i(w,v)$.
Porém em grafos direcionados, sendo conhecidos também por **Digrafos** $D(V,E)$, as arestas possuem direção única, sendo $e_i(v,w) \neq e_i(w,v)$. pois agora as arestas são direcionadas.
$$v \rightarrow w$$
![[grafo-direcionado.png]]

Desta forma é justo pensar em graus de saída e graus de entradas, que são denotados como:
### Grau de Saída de entrada
$d^+(v)$ = grau de saída
$d^-(v)$ = grau de entrada
## Fonte
A fonte e um vértice que possui grau de entrada nulo.
## Sumidouro
O sumidouro que o vértice que contem grau de saída nulo.

## Grafo subjacente
Dado um grafo direcionado $D(V,E)$, se retirarmos o direcionamento de suas arestas, teremos o grafo *subjacente* de $D$.
## Fracamente conexo 
Um grafo $D(V,E)$ é dito fracamente conexo ou desconexo, se seu grafo subjacente for também fracamente ou desconexo.

## Fortemente Conexo
Um grafo $D(V,E)$ é fortemente conexo se para todo par de vértices $v,w \in V$ existe um caminho de $v$ para $w$ e de $w$ para $v$. Caso isso seja atendido para todos os vértices de $V$ então $D$ e fortemente conexo e também unilateralmente conexo.

Se um grafo é **Fortemente Conexo** então ele também e unilateralmente e fracamente conexo.

---

# Busca em Profundidade
Uma busca é dita em profundidade quando o critério de escolha do vértice marcado é:
`"Dentre todos os vertices marcados e incidentes a alguma aresta ainda nao explorada, escolher aquele mais recentemente alcancado na busca."`
![[grafos-exemplo.png]]
Considerando o grafo da figura 4.3, e seguindo o critério da busca em profundidade, se selecionarmos o vértice 1 como vértice inicial, e posteriormente explorarmos uma aresta incidente a 1 que não seja explorada, como (1,2), agora teremos o vértice 2 visitado. Assim, seguindo o critério da busca em profundidade, a próxima aresta a ser selecionada deve ser uma aresta não explorada e incidente ao ultimo vértice visitado, no caso o vértice 2. então escolhemos pro exemplo a aresta (2,4) para ser explorada.

Exemplo do algoritm 4.3 do livro de busca em profundidade:
``` Algoritmo 4.3
Dados: G(V,E), conexo
	Procedimento P(v,u)
		marcar v
		para w ∈ A(v) efetuar:
	    if w é não marcado:
		    visitar aresta de árvore (v,w) > arestas visitadas(I)
			P(w,v)
		else:
	      if w ≠ u então visitar aresta de retorno (v,w) > arestas visitadas (II)
	desmarcar todos os vertices
	Escolher uma raiz s
P(s,Ø)
```

Dado um grafo $G(V,E)$ conexo, este algoritmo gera um $T(V,E_t)$ onde $E_t$ é o conjunto de aresta da arvore $T$. O algoritmo divido o conjunto das arestas $E$ em dois grupos, sendo o grupo ($I$) das arestas visitadas no algoritmo _(arestas retas)_, e o grupo ($II$) das arestas de retorno, que são as arestas não visitadas pelo algoritmo mas que estão presentes em $E(G)$ _(As arestas curvas)_. Como vistas na imagem abaixo:
![[grafos-busca-prof.png]]
## Ordem de Vértices
A ordem dos vértices que são inseridos ou retirados de $Q$ pode ser usadas as métricas de Profundidade de entrada $PE(v)$ e profundidade de saída $PS(v)$. sendo:
### Profundidade de Entrada PE(v)
Ordem que o vértice $v \in V$ entrou na pilha $Q$. Ou seja, quando o vértice foi visitado.
### Profundidade de Saída PS(v)
Ordem de saída de um vértice $v \in V$  da pilha $Q$. Um vértice $v$ só e retirado da pilha quando todos os seus vértices $A(v)$ foram visitados. Ou seja, só e retirado quando todos os vértices adjacentes a $v$ estão em $Q$.

Considerando a arvore $T$ gerada em (c) de 4.4, podemos montar a seguinte tabela:

| vértice | v₁  | v₂  | v₃  | v₄  | v₅  | v₆  |
| ------- | --- | --- | --- | --- | --- | --- |
| $PE(v)$ | 1   | 5   | 6   | 4   | 2   | 3   |
| $PS(v)$ | 6   | 3   | 2   | 4   | 5   | 1   |


## Biconectividade
Para a aplicação da busca em profundidade em grafos, será aplicada um algoritmo para a identificação de componentes biconvexas em grafos.

## _lowpt(v)_
Seja o grafo $G(V,E)$ e $T(V,E_t)$ a arvore de profundidade de $G$,  definiremos a função $lowpt(v)$ igual ao vértice mais próximo da raiz de modo que a partir do vértice em questão $v \in V$ somente seja possível descer uma aresta na arvore de profundidade e em seguida retornar para cima, usando no máximo uma aresta de retorno.

do grafo abaixo, definiremos a saída $lowpt(v)$:
![[grafos-lowpt.png]]

| $v_i$        | $v_1$ | $v_2$ | $v_3$ | $v_4$ | $v_5$ | $v_6$ | $v_7$ | $v_8$ | $v_9$ | $v_{10}$ |
| ------------ | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | -------- |
| $lowpt(v_i)$ | $v_8$ | $v_8$ | $v_2$ | $v_2$ | $v_2$ | $v_8$ | $v_8$ | $v_8$ | $v_8$ | $v_1$    |

A função $lowpt(v)$ e utilizada na definição de articulações em arvores de profundidade, como será discorrido a seguir.

## Articulações
Seja um grafo $G(V, E)$ e uma arvore de profundidade $T(V, E)$ de $G$. Uma articulação é um vértice $v \in V$, se e somente se:

1. se $v$ for raiz de $T$ e possuir mais de um filho, ou
2. se $v$ não e raiz de $T$ e possuir um filho $w$, tal que $lowpt(w) = v$ ou $w$.

## $g(v)$
Para o calculo de $lowpt(v)$, definimos a função $g(v)$ onde para um vértice ascendente $w$ de $v$ mais alto em $T$ tal que $(v,w)$ é uma aresta de retorno para aproximação da raiz ou $w$ é a própria raiz. Caso não exista aresta de retorno $g(v)=v$. Utilizando o exemplo da figura acima, temos a tabela de saída de $g(v)$ onde $v \in V$ de uma arvore de profundidade $T$ do grafo $G(V,E)$.

| $v_i$    | $v_1$ | $v_2$ | $v_3$ | $v_4$ | $v_5$ | $v_6$ | $v_7$ | $v_8$ | $v_9$ | $v_{10}$ |
| -------- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | -------- |
| $g(v_i)$ | $v_1$ | $v_8$ | $v_2$ | $v_4$ | $v_2$ | $v_6$ | $v_8$ | $v_8$ | $v_8$ | $v_1$    |

## Demarcadores
sejam $v,w$ vértices de $G$, de modo que $v$ seja articulação, caso $lowpt(w)=v$ ou $w$, então $w$ é um demarcador de $v$. Uma articulação pode ser pai de um ou mais demarcadores.
![[grafos-componentes-biconexaxs.png]]