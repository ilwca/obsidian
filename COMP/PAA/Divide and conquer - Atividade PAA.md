Nesta atividade, os grupos deverão selecionar um **artigo científico** que utilize a técnica de [[Divisão e conquista]] e reescrever o artigo, incluindo a implementação do algoritmo descrito. 

O Artigo cientifico escolhido foi: [Improvised Divide and Conquer Approach for the LIS Problem](https://www.sciencedirect.com/science/article/pii/S157086671830042X) (Rani,S; Rajpoot, D.S, 2018)

## Resumo
O Neste artigo é proposto um algoritmo de divisão e conquista que apresenta uma solução ótima para todos os casos  os casos para o problema da maior subsequencia crescente #LIS. 
Este problema pode ser relacionado com o problema #LCS, pois qualquer solução que resolva uma LIS resolve também um LCS, basta aplicar simultaneamente em duas ou mais arrays. Os algoritmos usados para este tipo de problemas podem ter varias aplicações como a identificação de padrões e compressão de dados.

Para o Artigo, foi usado divisão e conquista que consiste na divisão do problema em n subproblemas menores, que por sua vez são resolvidos individualmente, que posteriormente tem a solução destes problemas unidas para resolver o problema original. Para uma sequencia X de tamanho n, teremos x¹ e x² que são subsequencias de X.

### Linhas de Quadros de Young Tableau
Este mecanismo é uma forma de arruma organizar números de uma sequencia a fim de descobrir sua LIS.
! Como funciona o algoritmo:
dada uma sequencia X de tamanho n, gera uma subsequencia Y do algoritmo a seguir:
Ex: 
X = [2, 9, 6, 8, 3, 4, 7, 10]

1 -
	Y → recebe X[0] =2
	Y = [2]
2 -
	Y = X[1]=9  *→ recebe o  próximo índice de X*
	9 > Y[0] = 2 → *verifica se o numero adicionado é maior que algum numero da lista*
	Y = [2, 9] → *como não é, adiciona a lista*
3-
	Y = X[3] = 6 →*próximo item de X*
	6 < Y[1] → *como 6 é menor que 9, substitui*
	Y = [2,6]
4-
	Y = X[4] = 8
	8 > Y[] → *já que é maior que todos de Y adiciona...*
	Y = [2,6,8]
5- 
	Y = X[5] = 3
	3 < Y[1] → *como em y tem um menor, substitui*
	Y = [2,3,8]
6-
	Y = X[6] = 4
	4 < Y[2] → *como é menor que 8, substitui*
	Y = [2,3,4]
7-
	Y = X[7]=7
	7 > Y → *como é maior só adiciona*
	Y=[2,3,4,7]
8-
	Y = X[8]
	10 > Y →*como é maior só adiciona*
	Y[2,3,4,7,10]
9-
	*Percorreu todo X *
	*Y [2,3,4,7,10] FIM*


## Abordagem de Dividir para Conquistar
Neste caso de abordagem para este problema dividiremos o problema em subproblemas de tamanho igual o quando a sequencia for de tamanho par e quando for impar o segundo subproblema tem uma unidade a mais que o primeiro problema.

Para a divisão formaremos conjuntos dentro de X¹ e X² que são subconjuntos de X dados pela divisão deste por 2, onde teremos a permutação equivalente de todos estes indices [1, . . .,  n].
Neste caso, como sabemos que o elemento do meio é n/2, então podemos fazer isso para X¹ e X². Exemplo:
X = < 4, 2, 5, 1, 3 >  → então aqui desde 5/2 = 2
X¹ = <(2, 2), (4, 1)>
X² = <(4,1), (5, 3), (3, 5)>

a sequencia e fornecida de forma <(_value_, _ind_), (_value_, _ind_), ... >

### Predecessor
Predecessores indica qual o índice que veio o valor atual dentro da subsequencia LIS (que se formou ou esta sendo formada)

| Índice (posição) | Valor | Melhor LIS terminando aqui | Predecessor (índice anterior) |
| ---------------- | ----- | -------------------------- | ----------------------------- |
| 1                | 3     | [3]                        | 0 (não tem anterior)          |
| 2                | 1     | [1]                        | 0                             |
| 3                | 2     | [1, 2]                     | 2 (porque 1 vem antes de 2)   |
| 4                | 5     | [1, 2, 5]                  | 3                             |
| 5                | 4     | [1, 2, 4]                  | 3                             |