
Dado uma lista com  _n_ elementos, onde o objetivo é: Dado um valor _k_, verifique se ele esta na lista. Caso apareça, indique sua posição; Caso contrário, informe que não esta presente.

O algoritmo propõe que seja percorrido toda a lista comparando cada elemento com a chave _k_ , até encontrar uma correspondência.

Para este problema determine:

- **Melhor caso** 
- **Caso Médio**
- **Pior Caso**

Estes casos podem ser definidos como notações em [[notacoes assintoticas]]

sendo _f(n)_ o numero de comparações feitas ate encontrar o valor _k_

+ teremos o **Melhor caso** com _f(n)_=1 → _k_ no primeiro elemento da lista

+ **Pior Caso** com _f(n)_=n → k não esta na lista ou não esta na lista

- **Caso Médio** é a _f(n)_= p” ). onde P” é a probabilidade de _k_ em _n_ índices. Isto é dado por:
		```Qual a probabilidade de ser sorteado o numero 13 em 100 números de 1 a 100?
		1/100.
		Qual a probabilidade de serem sorteados os numeros 13, 28, 71 em 100 numeros de 1 a 100?
		3/100```
		
	Ou seja, P” = 1/n.  desta forma 1< P” > _n_ 
	
	logo: P”= _n+1/2_


# Limite Inferior e Superior de Complexidade

## Comportamentos Assintóticos

#### Analise Assintótica
A análise assintótica é uma maneira de descrever o comportamento limitante de uma função, que na análise de algoritmos estamos interessados no caso de entradas grandes, quando n → **∞**.

## Notações ( O, Ω, θ)
### Big O 
Análise de pior caso, limite superior

### Omega Ω
Análise de melhor caso, limite inferior

### Theta θ
Análise de caso médio, limite ajustado

###  BIG O
Representa o limite superior de caso de uma função.

formalmente: **_f(n)_ = O(_g(n)_)**

onde **_g(n)_** é a função limitante, ou seja, o grau de crescimento da função, que é o que realmente importa. Exemplo:

 - para a função `3n + 2`
	_f(n)_ = 3n + 2
	_g(n)_ = n

- Para a função `2n² + 4`
	_f(n)_ = 2n² + 4
	_g(n)_ = n²

Este limite superior classifica o grau de complexidade e crescimento da função podendo ser ela constante, linear, quadrática e etc.

| Notação    | Nome         | Exemplo             | Assoc         |
| ---------- | ------------ | ------------------- | ------------- |
| O(1)       | Constante    | Acesso a Array      | A[i]          |
| O(log n)   | Logarítmica  | Busca Binária       | A[n/2]        |
| O(n)       | Linear       | Busca Linear        | A[i++]        |
| O(n log n) | Linearítmica | Merge Sort          | Merge(A¹, A²) |
| O(n²)      | Quadrática   | Bubble Sort         | A[j]←→A[j-1]  |
| O(2”)      | Exponencial  | Fibonacci Recursiva | fbn(fbn(-1))  |
| O(n!)      | Fatorial     | Caixeiro Viajante   | n!            |

![[Complexidade.png]]



## Exemplo Prático 
Analise a complexidade do algoritmo Bubble Short

```bubble Short
```
function bubbleSort(arr):
	  n = tamanho(arr)
	  para i de 0 até n-1:
	    para j de 0 até n-i-1:
	      se arr[j] > arr[j+1]:
	        troca arr[j] e arr[j+1]
```
```

## Análise de Complexidade
- Identificar os Lops: Dois loops Aninhados
- Loop Externo: executa **n** vezes
- Loop interno: executa n-i-1 vezes
- total de comparações: `n + (n + 1) + (n - 2) + ... + 1`
- Soma: `n(n + 1) / 2` = `O(n²)`

pois: n(n + 1) = n² + n

portanto: 
_f(n)_= `n² + n / 2` 
_g(n)_=`n²`

**O(_g(n)_) = n² → O(n²)

Portanto, o algoritmo tem:
==complexidade de tempo = O(n)
complexidade de espaço = O(1) → algoritmo **IN-PLACE**==

! As principais métricas a serem analisadas é a complexidade de tempo e espaço.

### Complexidade de tempo
Quantidade de tempo gasto ou iterações a serem executadas em um algoritmo de acordo com o tamanho da entrada

### Complexidade de espaço
Quantidade de memória usada pelo algoritmo de acordo com o tamanho da entrada.

**IN-PLACE**: Em caso de algoritmos de ordenação, são aqueles que utilizam somente o próprio array para a ordenação.

****
# Notações assintóticas

## Notação Big O (O)

Pela definição do big O temos que sua notação é:

O(g(n)) / O(c.g(n))

Então para definir a notação do big O de uma função _f(n)_ se deve encontrar um c > 0 e n > 0, tal que O(n) > _f(n)_.

**Exemplo 1:**
Prove que f(n) = 25n+18 e g(n) = n

	Então f(n) ≤ O(g(n))

∃ c ∊ IN /  c ∙ n ≥ f(n) ∀n ≥ n°

assumindo c = 26, temos:

	25n + 18 ≤ 26n

Dividindo por n em ambos os lados

	25 + 18/n ≤ 26

Esta afirmação só será verdade quando **n > 18**, pois a medida que _n_ cresce `18/n` se aproxima de 0.
Assim, `25 + 18/n > 26` se n<18.

![[image01.png]]

Ou seja, para estes valore de c e n°, a desigualdade da definição é satisfeita. logo:

**f(n) ∈ O(n)**.

**Exemplo 2:**

verifique se a função _f(n)_=5n³+20n ∈ _g(n)_=n⁴

_f(n)_ ∈ O(g(n)) 
O(n) → c . g(n)

	f(n) ≤ c . g(n)

portanto:

	5n³+20n ≤ n⁴
	
(dividindo as desigualdades por n⁴)

	(5/n)+ 20/n³ ≤ c

tendo c = 26 e n =1

	(5/n)+ 20/n³ ≤ 26

(para todo n>1 f(n) tende a 0)
pois ∀n>1 _f(n)_ ≤ c

**portanto _f(n)_ ∈ O(g(n))**


## Notação Omega Ω
Seja duas funções não negativas _f(n)_ e _g(n)_ podemos dizer que _f(n)_ está na ordem Ω de _g(n)_ se escrevermos _f(n)_ = Ω(_g(n)_) ou _f(n)_ ∈ Ω(_g(n)_),  se existem constantes _c_ e _n_ tal que c > 0  e n° > 0. 
Assim tendo _f(n)_ > 0 e _f(n)_ ≥ c · _g(n)_ para todo n ≥ n°.

Ou seja, fazer a prova contraria de **BIG O**  tendo:

	f(n) ≥ c · g(n)

**Exemplo 1:**
Prove que se T(n) = 15n³ + n² + 4, então T(n) = Ω(n³)

então definimos um c ∈ IN / c · g(n) < f(n) ∀n>n°

c = 15 e n°=1

	f(n)≥ c · g(n) 

	15n³ + n² + 4 ≥ 15n³

**Exemplo 2:**
Mostre que 

	f(n) = 4n⁴ + 10n² ∈ Ω(n⁴)

**Recordando a definição** 
_f(n)_ ∈ Ω( _g(n)_), Significa que existem constantes c > 0 e n° tais que:

	f(n) ≥ c · g(n)  ∀n > n°

∀n ≥ 1, temos 10n² > 0

Isto é:

	4n⁴ + 10n² ≥ 4n⁴

portanto, podemos tomar c = 4 e n⁰ = 1, com essas constantes a igualdade é satisfeita.

Então 

**_f(n)_ ∈ Ω(n⁴)**


**Exemplo 3:**
Mostrar que:

	100n não está em Ω(n²)

Por definição de Ω, temos que _f(n)_ ≥ Ω(g(n)).
que significa que existem constantes c > 0 e n°

tal que  _f(n)_ ≥ c · _g(n)_ ∀n > n°

portanto, manipulando a desigualdade...

	100n ≥ n²
	100 ≥ n

Assim, existe um n, tal que n > 100. Portanto, conclui-se que

****_f(n)_ ∉ Ω(n²)****


## Notação Theta θ
Seja duas funções _f(n)_ e _g(n)_ não negativas, dizemos que _f(n)_ está na ordem de _g(n)_ e escrevemos _f(n)_ = θ(_g(n)_) ou _f(n)_ ∈ θ(_g(n)_). Então existem constantes c¹ e c² > 0 e n° > 0, tal que:

	c¹ · g(n) ≤ f(n) ≥ c² · g(n)      ∀n > n°

![[theta.png]]

portanto afirmamos que:

∃ c¹ > 0, ∃ c² > 0, ∃ n° > 0 | 0 ≤ c¹g(n) ≤ f(n) ≤ c²g(n) ∀n > n° 


**Exemplo 1:**

verifique se _f(n)_ = 5n² + 20n + 100 ∈ θ(n²)

por definição temos que:

	∃ c¹, c² > 0 | c¹g(n) ≤ f(n) ≤ c²g(n) ∀n > n°

então temos:

	c¹g(n) ≤ f(n) ≤ c²g(n)
	c¹n² ≤ 5n² + 20n + 100 ≤ c²n² 

dividindo as desigualdades por n²:

	c¹ ≤ 5 + 20/n + 100/n² ≤ c¹

∀n > 1 20/n e 100/n² se aproxima de 0.
portanto para um `n` suficientemente grande _f(n)_ → 5

assim, podemos assumir `c¹ = 4` e `c² = 6 ∀n > 25` 

Desta forma podemos afirmar que:

	f(n) ∈ θ(n²)


**Exemplo 2:**
prove que: _f(n)_ = 6n³ ∈ θ(n²)

por definição temos que:

	0 > c¹g(n) ≤ f(n) ≤ c²g(n) ∀n > n°
então

	c¹n² ≤ 6n³ ≤ c²n²

dividindo as desigualdades por n²:

	c¹ ≤ 6n ≤ c²

Assim provamos que _f(n)_ ∉ θ(n²) para um limite superior, pois não há um c¹ finito que seja superior a _f(n)_ para um  _n_  suficientemente grande.


*****

# Algoritmos iterativos

para um algoritmo de entrada N deve-se definir um função para o numero máximo de operações possíveis para este algoritmo.

**Exemplo 1:**

```Pseudocodigo

function MaxElement(L[]):
	
	max = L[0]; 
	
	for(i = 1; i < len(L)-1; i ++){  
	
		if(L[i] > max){
			
			max = L[i];
		
		}
	}
	
	return max;
```

Então C é uma  função que define o numero máximo de processos no pior caso para uma entrada n, então para medir o C(n), medimos:


``max = L[0]`` → 1 atribuição: 1 processo.

``for(i = 1; i < len(L)-1; i ++)`` → 1 atribuição, n - 1 verificação, n iterções : 2n processos.

``if(L[i] > max)`` → n - 1 verificações.

``return max `` → 1 retorno: 1 operação

Somando:

	1 + 1 + (n - 1) + n + (n - 1) + 1
	2(n - 1) + n + 3
	2n - 2 + n + 3
	3n - 1

portanto C(n) = 3n - 1


### Demonstração que C(n) ∈ O(n)

por definição, temos que O(n) é:

	O(n) = O(c · g(n))

Então Existe um c > 0 e um n° > 0, tal que:

	C(n) ≤ c · n  ∀n > n°

então

	3n - 1 ≤ cn

se `c = 4` e `n° = 1`, temos:

	3n - 1 ≤ 4n  ∀n > 1

Portanto as constantes satisfazem a condição, podemos concluir que:

C(n) ∈ O(n)


**Exemplo 2:**
```pseudocodigo
Algoritmo exemplo(A[1..n]) 
	soma = 0
    para i ← 1 até n faça
        para j ← 1 até i faça
            soma ← soma + A[j]
```

``soma = 0 `` → 1

``for(i = 1; i <= n; i++)`` →  1 + n

``for(j = 1; j < i; j ++)`` → (n(n+1)/2) + n

``soma ← soma + A[j]`` → (n(n+1)/2) no pior caso.

1 + n + 1  + n(n+1)/2) + n + (n(n+1)/2) 

2n + 2 + 2((n(n+1)/2))

∴ _C(n)_= (n² + n)/2 + 2n + 2

ou seja C(n) ∈ O(n²)


**Exemplo 3:**

``` pseudocodigo
função contar_processos(n):

    contador ← 0

    para i de 1 até n faça:
        contador ← contador + 1   // conta a verificação/execução

    para i de 1 até n faça:
        para j de 1 até i faça:
            contador ← contador + 1

    retorne contador
```


``contador ← 0 `` = 1

``para i de 1 até n faça:`` = n + 1

``para i de 1 até n faça:``= n + 1

``para j de 1 até i faça:`` = (n(n+1))/2

``retorne contador``= 1


portanto: 

	1 + (n + 1) + (n + 1) + (n² + n)/2 + 1

∴ _C(n)_ = (n² + n)/2 + 2n + 4


*****

# Algoritmos Recursivos
A analise de um algoritmo recursivo resolve uma recorrência, onde um algoritmo recursivo é aquele que chama a si mesmo com parâmetros diferentes.

Algoritmo recursivos são compostos por:

-  Caso Base ``if(num = n)``

-  Recursão ``recursão(recursao(n -1))``

para a analise do tempo de execução:

-  Determinar qual o tamanho N do problema
-  verificar se N esta no caso base
-  Determinar o T(n°)
- T(n) é uma soma de varias ocorrências de T(m) mais a soma das outras instruções efetuadas 

	














 