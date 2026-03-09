
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

**revisando** BigO não é uma igualdade, mas sim uma dominância de desigualdade.
Pela definição do big O temos que sua notação é:

$f(n) = O(g(n))⇔ ∃c > 0, ∃n_0 / f(n)\leq cg(n),\forall n \geq n_0$      

Então para definir a notação do bigO de uma função $f(n)$ se deve encontrar um $c > 0$ e $n > 0$, tal que $O(n) > f(n)$.

**Exemplo 1:**
Prove que f$(n) = 25n+18$ e $g(n) = n$

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

# ==Macete!==
dado uma função $T(n)15n³+n²+4$, então $T(n) \in O(n³)$.
para isso devemos definir um $c>0$ e $n_0>0$, tal que $T(n) \in O(n³)$

Podemos analisar cada fator do polinômio $T(n)$ e do outro lado colocar um valor respectivo de grau $g(n)$ do outro lado. como $g(n) = n³$, então fazemos:
$$T(n)=15n³+n²+4 \in O(n³)$$
Isolando os termos:
$$ 15n³ \leq 15n³$$
$$n² \leq n³$$
$$4 \leq 4n³$$
Assim, do outro lado da igualdade teremos sempre termos de grau 3, deste modo, é possível soma-los...

$$15n³+n³+4n³$$
$$ = 20n³$$
Portanto, achamos assim uma constante $c$ que atende a cota superior para $T(n)$. Então, assumimos $c = 20$ e $n_0=1$. Deste modo $\forall n>n_0 T(n)\leq O(n³)$ 

Por fim, podemos afirmar que
$$T(n) \in O(n³)$$


### Ex. 2
verificar se $2^{2n} \in O(2^n)$.

**afirmação**: $2^{2n} \notin O(2^n)$

Por contradição, se dividirmos ambos os lados por $2^n$ teremos:
$$2^{2n}\leq2nc$$
$$2^n\leq c$$
portanto
$$2^{2n}\notin O(2^n)$$


### Ex. 3
prove que $f=O(n²)$

com $f(n)=3n²+5n+7$

diretamente, temos:
$$3n²+5n+7 \leq c . n²$$
dividindo ambos os lados por $n²$
teremos:

$$\frac{7}{n²}+\frac{5}{n}+3 \leq c$$
com um $n_0>1$ a função $f(n)$ passa a diminuir infinitamente, então teremos este lado da igualdade maior em $n_0=1$. assim podemos definirmos $c=15$ atenderemos a dominância.

$$\therefore 3n²+5n+7 \leq 15n² \ \forall n \geq n_0$$ 

---
## Notação Omega Ω
Seja duas funções não negativas $f(n)$ e $g(n)$ podemos dizer que $f(n)$ está na ordem $Ω$ de $g(n)$ se escrevermos $f(n)$ = $Ω(g(n))$ ou $f(n) ∈ Ω(g(n))$,  se existem constantes _c_ e _n_ tal que $c > 0$  e $n_0 > 0$.
Assim tendo $f(n) > 0$ e $f(n) ≥ c · g(n)$ para todo $n ≥ n_0$.


Ou seja, fazer a prova contraria de **BIG O**  tendo:

$$f(n) ≥ c · g(n)$$

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

	$c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)$

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



---
## Teorema mestre
o teorema mestre e usada para definirmos a complexidade assintótica de um algoritmo a partir do seu custo T(n), ou seja, seu custo recursivo +  custo externo.

### Ideia central do teorema
ele compara:
- O custo total das chamadas recursivas:
## $n^{log_b^a}$

com
- O custo fora da função recursiva
###  $f(n)$

e decide quem **Domina**, a função com  maior custo, tem a complexidade assintótica.


Para isso, existem 3 casos. Definimos

### $d = log_b^a$

agora compare com a função $f(n)$ com  ${n^d}$

---
### Caso I

recursão domina:

$f(n) \in O(n^{d-ε})$

resultado:

$T(n) \in \Theta(n^d)$

Exemplo:
$T(n) = 8T(n/2) + n²$
$d = log_2 8 = 3$

Usaremos $n^d$ = $n³$

como $n² < n³$, então:

$T(n) \in \Theta(n³)$

---

### Caso II

$f(n) \in \Theta(n^d log^{k+1}n)$

Exemplo clássico:
$T(n) = 2T(n/2)+n$
$d=\log_22=1$
$f(n) = n \rightarrow T(n) \in \Theta(n\log n)$ 

aplicado no caso, teremos:
$T(n) \in \Theta(n^d \log¹ n)$ onde k é o grua de $f(n)$
portanto:
$T(n) \in \Theta(n \log n)$


*****

### Caso III 
$f(n) \in \Omega(n^{d-ε})$

com condicao de regularidade:

$af(n/b) ≤ cf(n), c < 1$

resultado:

$T(n) \in \Theta(f(n))$

exemplo:

$T(n) = 2T(n/2)+n² \rightarrow T(n) \in \Theta(n²)$

---
- $T(n)=4T(n/2)+n$
- $T(n)=2T(n/2)+nlogn$
- $T(n)=3T(n/3)+n$

1-
a = 4
b = 2
f(n) =n

$\log_2 4 = 2$
$n^d = n²$

como $n² > n$. Caso 1, predominância da recorrência.

$T(n) \in \Theta(n²)$

2- 
a = 2
b = 2
f(n) = n log n

$d=\log_2​2=1$

caso de empate
$T(n)∈Θ(nlogn)$

3- 
a= 3
b = 3
f(n) = n²

$d=\log_33=1$

custo externo domina
$T(n)∈Θ(n2)$





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

	


---

## Exercicios

## 📝 **Questão de Treino – Análise de Complexidade, Big-O e Θ**

Considere o seguinte algoritmo em pseudocódigo:

```text
Algoritmo Exemplo(n):
1. s ← 0
2. para i = 1 até n:
3.     para j = 1 até i:
4.         s ← s + 1
5. para k = 1 até n:
6.     para m = 1 até n:
7.         s ← s + 1
8. retorne s
```

### (a) Encontre a **função de custo T(n)** que representa o número de operações executadas no pior caso.

---

### (b) Determine a **complexidade assintótica em Big-O**.

---

### (c) Determine a **classe Θ(T(n))**.

---

### (d) Justifique formalmente por que a complexidade encontrada em (b) pertence a Θ da letra (c).

---
## Resposta
### A)
do primeiro bloco for temos O(n²/2)
e no segundo temos: O(n²)

de complexidade total teremos:
$T(n) = \frac{3}{2}n^2 + \frac{1}{2}n$

### B)
Complexidade assintótica bigO
$O(g(n))$
$f(n) = \frac{3}{2}n^2 + \frac{1}{2}n  =  g(n²)$

$O(n) = c \cdot g(n)$

então
$\exists c > 0$ e $\exists n \mid f(n) \leq c \cdot g(n), \forall n > n_0$ 

$= \frac{3}{2}n² + \frac{1}{2}n \leq c\cdot n²$

então, para c = 2 e n =, temos 

$\frac{3}{2}n² + \frac{1}{2}n \leq2n²$

portanto

$f(n) \in O(n²)$ 

### C)
determine o $\theta(T(n))$ 

$c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)$ 

então

$\exists c_1 > 0, \exists c_2 > 0 \text{e} \exists n_0 \mid c_1g(n) \leq f(n) \leq c_2g(n), \forall n>n_0$

Desta forma, tomando $c_1 = 1$ e $c_2 = 2$ para $n_0 = 1$

$n² \leq \frac{3}{2}n² + \frac{1}{2}n \leq2n²$

portanto $f(n) \in \theta(n²)$


d

```

funcao 2 algo(n)

if n = 1 then
	return 1
endif
for i ← 1 to 8 do
	z ← algo(n/2)
enfdor
for i ← 1 to n³ do
	z ← o 
endfor
```

Defina T(n) como o numero total de vezes que a atribuição z ← 0 é executada por algo(n)(contando todas as chamadas recursivas, nao apenas a chamada inicial) Desconsidere qualquer outro custo.

a) Escreva a reconrrencia que define T(n) e indique claramente a condicao de base.
b) Prove diretamente que T(n) $\in \Omega(n³ \log n)$ (Sem usar teorema mestre).   
c) substitua o "8" do primeiro laco por "7", obtenha a nova recorrencia e mostr diretamente que, nesse caso, T(n) $\in$ O(n³).

**A)** $T(n) = 8T(n/2) + O(n³)$ 

**B)** temos que provar agora o limite inferior da funcao.
