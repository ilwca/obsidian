[[h.chomsky.canvas|h.chomsky]]


Uma gramática é formada por uma quadrupla. G = (V T P S )

**V** = Conjunto finito e não vazio de símbolos e variáveis (alfabeto de variáveis)
**T** = Conjunto finito de símbolos terminais 
**P** = Regra de Produção
**S** = Simbolo inicial / S ∊ V


No compilador a ser desenvolvido usaremos  [[Gramatica BNF]] , composto por símbolos terminais e não terminais.

**Não-Terminais** : símbolos abstratos como `<expr>` , `<program>` que na gramatica forma são as variáveis `A`, `B` ...

**Terminais** : são símbolos imutáveis, que não geram outros símbolos, como tokens `if`, `+` e etc. Nas gramaticas formais representadas pelos símbolos `a` , `b` ...

**Produções**: Regras que dizes como os não terminais geram ou não outros símbolos. Exemplo:
`S → Ab
`A → a | S`

S → aB



