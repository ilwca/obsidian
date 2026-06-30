# Questão I
prove ou refute a seguinte afirmação: Se $f(n) = O(g(n))$, então $2^{f(n)} = O(2^{g(n)})$ .
forneça um contraexemplo caso a afirmação seja falsa.

Pela definição de Big-O:

$∃c>0,∃n0$  tal que  $f(n)≤cg(n),∀n≥n0$

Como a função exponencial $2^x$ é **monótona crescente**, aplicamos dos dois lados:

$2^{f(n)}≤2^{cg(n)}$

Reescrevendo:

$2^{cg(n)}=(2^{g(n)})^c$

Como c é **constante**:

$(2^{g(n)})^c∈O(2^{g(n)})$

Logo,

$\boxed{ 2^{f(n)} = O(2^{g(n)}) }​$

se assumirmos $f(n)=2n$ e $O(n)$, então teremos:
$$2^{f(n)}\leq(2^{g(n)})\cdot c$$
$$2^{2n}\leq(2^{n})\cdot c$$
se dividirmos ambos os lados da desigualdade por $2^n$, teremos
$$2^n \leq c$$
o que $\nexists c \in \mathbb{R}$ que atenda a igualdade.
Provamos por Contraexemplo:
$$\boxed{f(n)=2n, \text{ }\text{ } g(n)=n}$$

---
## Questão
Sejam $f_1(n), f_2(n), g_1(n) \text{ e } g_2(n)$ funções assintoticamente não negativas definidas para $n$ suficientemente grande. Suponha que:
$$f_1(n) = \Theta(g_1(n)) \text{ }\text{ e }\text{ } f_2(n)=\Theta(g_2(n))$$
A) prove formalmente, a partir da definição de $\Theta$, que:
$$f_1(n) \cdot f_2(n) = \Theta(g_1(n)\cdot g_2(n))$$
B) Analise a seguinte preposição análoga:
$$f_1(n) + f_2(n) = \Theta(g_1(n) + g_2(n))$$
Ela é sempre verdadeira sob as mesma hipóteses? Prove ou refute.

## Questão II

considere o algoritmo abaixo que recebe um array A de inteiros de tamanho $n\geq1$ e devolve o maior elemento.
```algoritmo
Maximo(A,n){ #com n>=1
	m = A[0]
	for(i=1; i++; i=n-1){
		if A[i]>m{
			m = A[i]
		}
	}
	return m;
}
```

contagem de processos:
`m=A[0]` = 1
`for()` = n-1
`if()` = O(n-1)
`return` = 1 
tempo total O(n) = 1 + (n+1) + (n+1) + 1.
2(n+1)+1+1
2n+4

T(n) = 2n+4
Portanto, podemos definir o limite superior como $O(n)$ pois $g(n) = n$.
Demonstrando que  $T(n) = O(n)$.

por definição temos que:
$$O(n) = c\cdot g(n)$$
então $\exists c \in R$ tal que:
$$f(n)\leq c\cdot g(n)$$ $\forall n_0 > n$ onde $n\in R$.
Assim temos:
$$2n+4 \leq c \cdot n$$
ao dividirmos por $n$ a desigualdade teremos:
$$2 + \frac{4}{n} \leq c$$
com $n > 4, \frac{4}{n}$ tende a zero, então, se tomarmos $c = 3$ e $n_0 = 4$ teremos no caso base:
$$2+\frac{4}{4}\leq3$$
$$2+1\leq3$$
Desta forma provamos que $T(n) = O(n)$ para $c =3$ e $n=4$.

---

