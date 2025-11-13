
# Algoritmo de Moore-Hodgson
Este algoritmo minimiza o número de tarefas atrasadas de uma máquina. Ou seja ele encontra a programação ótima para o problema clássico.

Segundo Moore Hodgson, o algoritmo usa duas operações de ordenação somente, por isso é viável para $n$ muito grandes.

Para denotarmo uma lista de um inteiro positivo, denotamos  como _\[ l ]_  para uma ${ 1, 2, . . . , l }$   

Uma tarefa é dada por um numero de tarefas $n$ denotado por $1, 2, . . ., n$  (par ser identificada pelo índice). Cada tarefa, dada por $j$ tem um tempo de execução $Pj > 0$ e uma data de vencimento dada por $Dj$ também positiva.   
A programação deste problema consiste na permutação destes $n$ problemas. dada uma programação $S$, seu tempo de conclusão é dado por $Cj$ , que consiste no tempo de execução de $Pj$ mais os tempos de execução dos que antecedem $j$. Uma tarefa $j$ é considerada atrasada se $Cj > Dj$. O objetivo é encontrar uma programação $S$ que minimize o numero de tarefas atrasadas. 

$j$ → Tarefa.
$Pj$ → Tempo de execução da tarefa $j$.
$Dj$ → Data de vencimento de uma tarefa $j$.
$Cj$ → Tempo gasto até o resolvimento da tarefa $j$.
$S$ → Programação de resolução de $l$.

Para a ordenação é utilizado a regra EDD que é uma regra de vencimento mais próxima que ordena as tarefas de forma decrescente de suas datas de vencimento. 


Seja _k_ o primeiro trabalho atrasado na sequência EDD. Assim,
$Ck = ⅀ i ∊ [k] Pi > Dk = max i∊[k] Di$
Considere qualquer cronograma _S._ Seja _ℓ_ a última das tarefas emem _S._ Então, o tempo de conclusão de _ℓ_ em _S_ é pelo menosAssim, ℓ _é_ um trabalho tardio de _S._ □