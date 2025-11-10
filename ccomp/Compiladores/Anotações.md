Mesmos conceitos de Linguagens formais e automatos.


## Linguagens 
linguagem é um conjunto de palavras formadas por um alfabeto (∑) especifico de simbolos / **L** ⊆ ∑
## AFD
Autômatos finitos determinísticos, são compostos pela 5-tupla:

⅀ = alfabeto de símbolos → ⅀ = {a, b}
**Q** = Conjunto finito de estados → *Q* = {q0, q1, q2, q3}
**𝛿** = função de transição → *𝛿* (q1, b) = q3
**q0** = estado inicial / *q0* ∊ *Q*
**F** = conjunto de estados finais

## AFN
Autômatos finitos não determinísticos, são composto por uma 5-tupla, a diferença é que a função de transição 𝛿 não retorna um único estado, mas sim, um conjunto de estados.

⅀ = alfabeto de símbolos → ⅀ = {a, b}
**Q** = Conjunto finito de estados → *Q* = {q0, q1, q2, q3}
**𝛿** = função de transição que retorna um conjunto → *𝛿* (q1, b) = {q0, q3}
**q0** = estado inicial / *q0* ∊ *Q*
**F** = conjunto de estados finais → F{q3} 

