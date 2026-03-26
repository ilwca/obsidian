# 24/03

## Recorrência

## Método da Indução

## Expansão da Arvore de Recorrência

## Teorema Mestre
Aplicado para a resolução de recorrências do tipo = $T(n) = aT(\frac{n}{b}+f(n))$ resolvendo diretamente relacionado a três casos comuns.


### Exercício 1.
![[paa-fatorial.png]]

temos que:

$$T(n)= T(n-1)+c_2$$
decompondo $T(n-1)$, como:
$$T(n-1) = ?$$
$$T(n-1) = T(n-1-1)+c_2$$
$$T(n-1) = T(n-2)+c_2$$

aplicando este $T(n-1)$ na função principal:
$$T(n-1) = T(n-2)+c_2+c_2$$

decompondo $T(n-2)$, da mesma forma que inicialmente:
$$T(n-2) = T(n-2-1)+c_2$$
$$T(n-2) = T(n-3)+c_2$$

aplicando na função principal:
$$T(n) = T(n-3)+c_2+c_2+c_2$$
Desta forma, teremos que a função principal fica desta forma:
$$T(n)= T(n-1)+c_2$$
$$T(n) = T(n-2)+c_2+c_2$$
$$T(n) = T(n-3)+c_2+c_2+c_2$$
Assim, percebemos que:
$$T(n)=T(n-k)+k\cdot c_2$$
percebe-se que $k=n$, pois na 3ª iteração teremos $T(n-3)$. 
Portanto $k=n$.
Desta forma teremos na notação principal que $n-k=0$
$$T(n) = T(n-k)+k\cdot c_2$$
$$T(n) = T(0)+n \cdot c_2$$
$$T(n)=c_1 + n\cdot c_2$$

portanto, temos que:
$$n \cdot c_2 + c_1 = O(n)$$

## Exercício 2.
Relação de recorrência:
$$T(n) = \begin{cases} 1 & \text{se } n=1\\ 2T(n-1)+1 &\text{se }n\geq 2\end{cases}$$
	