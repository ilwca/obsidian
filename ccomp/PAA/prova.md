
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
funcao sceduling(lista[])
	lista[] = Mergesort(f) #O(n log n)
	solucao[] = lista[1]
	fim_atual = lista[1].f_1
	
	for i=2 in lista[] # O(n-1)
		if b_i >= fim atual 
			solucao[].append = lista[i]
			fim_atual = lista[i].f_i
```

