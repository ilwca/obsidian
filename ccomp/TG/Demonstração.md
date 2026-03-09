Existem diversos métodos de demonstração (prova), as principais que iremos utilizar são:
- Indução matemática
- Demonstração direta
- Contraposição 
- Contradição / Redução ao Absurdo
- "Se somente se"
- Demonstração por Construção

O processo de prova ou demonstração, sempre parte de uma **conjectura**, que nada mais é do que uma suposição ainda não provada ou concreta.
por exemplo:
$$1 = 1$$
$$1+3 = 4$$
$$1+3+5 = 9$$
$$1+3+5+7 = 16$$
portanto, suspeitamos que a soma do primeiros $n$ números impares é igual a $n²$.
Então essa e a nossa **Conjectura**. 
Em contrapartida, uma conjectura dessa não prova nada, pois, não sabemos se esta conjectura é valida para todos os infinitos casos do conjunto dos números reais.     

## Indução Finita
O principio da indução finita conta com duas etapas principais. A partir da hipótese deve-se formular o caso base e a recorrência. Ex:
$$1 = 1$$$$1+3 = 4$$
$$1+3+5 = 9$$$$1+3+5+...+2n-1 = n²$$
Então devemos provar que a hipótese é valida para os $n$ primeiros números e o próximo, então supondo para um $k$-ésimo número, fazendo $n=k$
**base**:
$$1+3+5+...+2k-1=k²$$
esta base deve ser válida também para o valor sucessor de $k$, ou seja deve ser valida também para $k+1$, portanto:
$$1+3+5+...+(2k-1)+(2k+1)$$
de acordo com nossa hipótese, sabemos que $1+3+5+...+(2k-1)=k²$, assim podemos substituir no proposição, assim, teremos:
$$k²+(2k+1)$$
sabemos que decompondo a expressão $2k+1$ é igual a $(k+1)²$, portanto, prova-se que a hipótese é valida para $k+1$.

## Redução ao Absurdo
Prove que nenhum número inteiro pode ser pimpar e par ao mesmo tempo.

_Na redução ao absurdo iremos supor alguns absurdos como este._

Demonstrando. Suponha por absurdo que:
$$\exists k,l \in N$$
sendo $2k \Rightarrow par$ e $2l+1 \Rightarrow impar$ 
Portanto, $\exists x \in N$ tal que $x=2k$ e $x=2l+1$. Ja que $x$ pode ser impar e par ao mesmo tempo, $2k=2l+1$. Resolvendo a expressao:
$$2k=2l+1$$
$$2k-2l=1$$
$$k-l=\frac{1}{2}$$
**Absurdo!** pois:
$$\nexists k,l \in N | k-l \in N$$
portanto
$$\nexists x \in Z | x=2k \wedge x=2l+1$$
