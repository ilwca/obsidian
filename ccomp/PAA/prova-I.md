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

