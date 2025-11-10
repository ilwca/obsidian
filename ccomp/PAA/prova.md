
  4 - Considere   o seguinte algoritmo, chamado count, cujo o input é um numero inteiro positivo n:

```pseudocodigo
função count(n)
	count = 0
	for(i=1, i < log(n), i++)
		for(j = i, i + 5, j++)
			for(k = 1, k < i, k ++)
				count = count(+1)
```


3 - A[ i ] + A[ j ] + A[ k ] == value function

```pseudocodigo
function finds(A, S)
	for(i=0, i<len(A)-2, i++)
		for(j=(i+1), j<len(A)-1, j++)
			for(k=j+1, k<(len(A)), k++)
				if(A[i] + A[j] + A[k] == S)
					return A[i], A[j], A[k];
					
	return false;
```


