"Embora este método seja aplicável ao problema definido aqui, ele é desenvolvido de forma geral neste artigo. No entanto, consiste em apenas duas operações de ordenação realizadas no conjunto total de tarefas e um máximo de $\frac{n+1}{2}$ adições e comparações. Consequentemente, este método será computacionalmente viável para problemas muito grandes e pode ser executado manualmente." JM Moore
# Algoritmo de Moore-Hodgson
Este algoritmo minimiza o número de tarefas atrasadas de uma máquina. Ou seja ele encontra a programação ótima para o problema clássico. Segundo Moore Hodgson, o algoritmo usa duas operações de comparação e ordenação, por isso é viável para $n$ muito grandes.

Para denotarmos uma lista de um inteiro positivo, denotamos  como \[ $l$ ]  para uma ${ 1, 2, . . . , l }$   

Uma tarefa é dada por um numero de tarefas $n$ denotado por $1, 2, . . ., n$  (par ser identificada pelo índice). Cada tarefa, dada por $j$ tem um tempo de execução $Pj > 0$ e uma data de vencimento dada por $Dj$ também positiva.   
A programação deste problema consiste na permutação destes $n$ problemas. dada uma programação $S$, seu tempo de conclusão é dado por $Cj$ , que consiste no tempo de execução de $Pj$ mais os tempos de execução dos que antecedem $j$. Uma tarefa $j$ é considerada atrasada se $Cj > d_j$. 
O objetivo é encontrar uma programação $S$ que minimize o numero de tarefas atrasadas. Isto é um NP-difícil em geral, porem o algoritmo de Moore-Hodgson resolve em tempo polinomial $O(n log n)$ na prática, mas $O(n²)$ na implementação básica.

$j$ → Tarefa.
$p_j$ → Tempo de execução da tarefa $j$.
$d_j$ → Data de vencimento de uma tarefa $j$.
$Cj$ → Tempo gasto até o resolvimento da tarefa $j$.
$S$ → Programação de resolução de $l$.

Para a ordenação é utilizado a regra EDD (Earliest Due Date) que é uma regra de vencimento mais próxima que ordena as tarefas de forma crescente de suas datas de vencimento, assim temos:
$d_1 ≤ d_2 ≤ d_3 ≤ . . . ≤ dj$ . 


## do Algoritmo
Usaremos um exemplo numérico do artigo. 
- jobs : 8 → números de jobs, $j$ = 1, 2, 3, 4, 5, 6, 7, 8.
- $d_j$ : \[6, 8, 9, 11, 20, 25, 28, 35] → vencimento de $d_1$ = 6, $d_4$ = 11...
- $p_j$ : \[4, 1, 6, 3, 6, 8, 7,  10] → tempo de execução de $j$ .

Jobs ordenados por ordem EDD em $d_j$ ordenados crescentemente, assim para o nosso tempos de execução teremos:

$C_j$ = \[4, 5, 11, 14, 20, 28, 35, 45].

Desta forma, temos um atraso em  $d_3$ , pois o $C_3$ > $d_3$ , ou seja, validade da tarefa 3 é de 9 e ele é terminado em 11.

Então é feita uma leitura na lista $p_j$ pois a tarefa com o maior tempo de processamento será removida. Neste caso, $p_3$ é o maior tempo de processamento.  Então esta é a parte **Gulosa** do algoritmo, está em remover o maior $p_j$ quando o $C_j > d_j$  .

---
### Exemplo
Problema do troco. Precisa converter um quantia monetária $V$ em notas e moedas para abastecer um caixa rapido. Objetivo e devolver o menor numero possível de unidades de moedas.
$$V =[100,50,20,10,5,2,1]$$
a) apresente um pseudocódigo do algoritmo guloso para este problema

``` Pseudocodigo
returnCash(V, x)
	\\caso V nao esteja ordenado
	mergeSort(V,-1)
	left = x
	S[] \\resultado
	while left != 0
		i=0
		if left < V[i]
			left= left-V[i]
			S[].append = V[i] \\adiciona V[i] no final de S
			i=0
	return
```

### Escolha local
local onde e feito a escolha de melhor resultado no momento.
