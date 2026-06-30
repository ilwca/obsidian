
  4 - Considere   o seguinte algoritmo, chamado count, cujo o input é um numero inteiro positivo n:
```pseudocodigo
função count(n)
	count = 0
	for(i=1, i < log(n), i++)
		for(j = i, i + 5, j++)
			for(k = 1, k < i, k ++)
				count = count(+1)
```


3 - A[ i ] + A[ j ] + A[ k ] == value function

```pseudocodigo
function finds(A, S)
	for(i=0, i<len(A)-2, i++)
		for(j=(i+1), j<len(A)-1, j++)
			for(k=j+1, k<(len(A)), k++)
				if(A[i] + A[j] + A[k] == S)
					return A[i], A[j], A[k];
	
	return false;
```



# PROVA-II

## Questao 1
1 - a) Proponha um algoritmo
algoritmo da mochila

```
funcao containerAloc(W, n[])
	razao = v_i/p_i  #me diga se devo adicionar esta divisão a complexidade total
	merge_sort(razao[]) #funcao de ordenação qualquer O(n log n) me indique uma 
	solucao[] = 0
	peso_atual = 0
	
	for i em razao[]:  #complexiadade O(n)
		if peso_atual + p_i ≤ W:
			solucao = razao[i]
			peso_atual += p_i
		
	return solucao[]	
```

complexidade total O(n log n)
O(n log n) → oredenação da razao\[], usando merge sort
O(n) → for para percorer a razao\[]

**b)** Exemplo com 5 caixas

| N      | $p_i$ | $v_i$ | razao |
| ------ | ----- | ----- | ----- |
| item 1 | 100   | 50    | 2     |
| item 2 | 150   | 50    | 3     |
| item 3 | 120   | 20    | 4     |
| item 4 | 80    | 40    | 2     |
| item 5 | 40    | 10    | 4     |

razao = \[
	item 5,
	item 3,
	item 2,
	item 1,
	item 4
]

Para um `W = 300`

```
for i em razao[]:  
		if peso_atual + p_i ≤ W:
			solucao = razao[i]
			peso_atual += p_i

=================================

if 0 + 40 ≤ 300
	solucao[5]
	peso_atual = 40
	
=================================

if 40 + 120 < 300
	solucao[5, 3]
	peso atual = 160

=================================

if 160 + 150 < 300
	skip
	
=================================

if 160 + 100 < 300
	solucao[5,3,1]
	peso atual = 260

=================================

if 260 + 80 < 300
	skip
```

retorno da funcao 
Solucao\[
	item 5,
	item 3,
	item 1
]

peso_atual = 260
valor total = 80

solucao otima = {item 5, item 2, item 1}


## Questão II
Usando divisão e conquista encontre um numero na lista:


pra isso, usei uma funcao de binary search recursiva
```
def heap_find(list, target):

	mid = (len(list) // 2)
	
	rigth = list[mid:]
	
	left = list[:mid]
	
	if target == list[mid]:
		return f"numero na lista"
	else:
		print(left, mid, rigth)
		if target < list[mid]:
		return heap_find(left, target)
	else:
		return heap_find(rigth, target)
```

complexidade O(log n) 


# Prova II - II

## Questão 1
tendo:

$A_i$ = Atividades
$b_i$ = Inicio da atividade
$f_i$ = término da atividade

Algoritmo pensado para o problema da selação de atividades:
```pseudoalgoritmo
funcao scheduling(lista[])
	lista[] = Mergesort(f) #O(n log n)
	solucao[] = lista[1]
	fim_atual = lista[1].f_1
	
	for i=2 in lista[] # O(n-1)
		if b_i >= fim atual 
			solucao[].append = lista[i]
			fim_atual = lista[i].f_i
```


## Questão 2
Contagem de recorrências em uma lista de tamanho $n$ usando programação dinâmica.

```pseudo
funcao countFreq(list)
	mid = len(list)//2
	esquerda = list[:mid]
	direita = list[mid:]
	
	if len(lista) == 1:
		return {list[0]:1}
	else
		countFreq(esquerda)
		countFreq(direita)
	
	return merge(esquerda, direita)
	
function merge(listA, listB)
	
	result[] = listA[]
	
	for i in listB:
		if i in listB
			result[i] += listB[i]
		else
			result[i] = listB[i]
	
	return resultado
```


A **complexidade** é dada por:

função recursiva: $T(n) = 2T(n/2)$
função de merge: $O(n/2) + O(n/2) = O(n)$

portanto complexidade assintótica total: $T(n) = 2T(n/2) + O(n)$

utilizando o teorema mestre, dado por:

$aT(n/b) + f(n)$ 
$2T(n/2) + O(n)$

portanto:
a = 2 
b = 2
$f(n)$ = n

então

$n^{log_b^a} = n^{log_2^2} = n¹$

caso 2 do teorema Mestre. Então

$\theta(n log n)$ é complexidade total.

## Exercício
Período mais lucrativo
a partir de uma lista $L = [2, -3, 4, -1, 2, -5, 6]$. Determinar qual foi o período mais lucrativo usando **divisão e conquista**.
```pseudo
funcao countFreq(list)
	mid = len(list)//2
	esquerda = list[:mid]
	direita = list[mid:]
	
	if len(lista) == 1:
		return list[0]
	else
		countFreq(esquerda)
		countFreq(direita)
	
	return merge(esquerda, direita)
	
merge(mapA, mapB)
	first = 0
	second = 0
	for i in mapA
		first +=mapA[i]
	
	for i in mapB
		second +=mapB[i]
	
	if firt > second
		return "periodo 1 mais lucrativo"
	else
		return "periodo 2 mais lucrativo"
```


## Questão 3

Problema da partição minima.
dado um $S$ de $n$ números positivos, encontrar um $S_1$ e $S_2$  tal que, a diferença entre eles seja a mínima possível.
Para isso, determinamos um $T = \sum S$
portanto, $S_1$ e $S_2$ tem que ser o mais próximo possível de $T/2$.
Então determinamos um $dp[i][j]$ composto por:
$i$ : 0 a $length(S)$
$j$ : 0 a $T/2$ 

### Exemplo
$S=\{1,3,4\}$ 
formar a tabela $dp[i][j]$ onde:
$i$ : 0 a 3
$j$ : 0 a 4

$dp[i][j]$ = é possível formar o valor $j$ usando os primeiros $i$ elementos.

| $i / j$   | 0   | 1   | 2   | 3   | 4   |
| --------- | --- | --- | --- | --- | --- |
| 0 (0)     | 1   | 0   | 0   | 0   | 0   |
| 1 (1)     | 1   | 1   | 0   | 0   | 0   |
| 2 (1,3)   | 1   | 1   | 0   | 1   | 0   |
| 3 (1,3,4) | 1   | 1   | 0   | 1   | 1   |



# Prova II (REAL)

**1- Desenvolva uma algoritmo Guloso** para o ajuste de troco.

entrada $V = \{ 100, 50, 20, 10, 5, 2, 1 \}$

**A)** Apresentar algorimo guloso para este.
**B)** Aplique o algorimo ao  valor V = 289

### Resposta
A) 
```
function CashReturn(V, target)
	mergeSort(V, -1) # ordenar vator de moedas de forma decrescente
	valor_atual = 0
	solucao = 0
	
	for i in V:
		if valor_atual + V[i] <= target   #escolha local, visando maior de V[]
			solucao.append(V[i])  #adiciona valor ao final de Solucao[]
			valor_atual += V[i]
			i = 0
	
	return solucao[]
```


## Questao
``` algorithm
Procedure(V, inicio, fim)
	if inicio == fim
		return V[inicio]
	else 
		meio len(V)//2
		x = Procedure(V, inicio, meio)
		y = Procedure(V, meio+1, fim)
		z = 0
		
		for i = inicio to fim
			z = z + V[i]
			return x + y + z
		
```
