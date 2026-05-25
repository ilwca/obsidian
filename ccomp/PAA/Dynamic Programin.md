A programação dinâmica consiste em dividir o problema principal em subproblemas e resolve-los separadamente, armazenando o resultado em uma tabela como uma espécie de memorização. 
A programação dinâmica e normalmente feita em três passos principais:
- **Dividir o Problema**
- **Resolver cada Subproblema apenas um vez**
- **Combinar as Soluções dos Subproblemas**
Umas das características que definem a eficiência da programação dinâmica são as características de 
- **Subproblemas Sobrepostos** - Alguns subproblemas aparecem varias vezes durante a resolução do problema.
- **Optimalidade de Subestrutura** - A solução do problema maior e formada a partir da solucao dos problemas menores.

# Problema SSAP
O problema SSAP significa Shelf-Space Allocation Problem que no português significa problema de alocação de espaço. Este problema é comumente enfrentado por varejistas no posicionamento de produtos em espaços limitados na prateleiras. Estes produtos devem ser alocados seguindo regras de marketing visando uma maior lucratividade, então alem do espaço do produto são considerados outros parâmetros para a alocação.

## NP-Dificil
Este problema é classificado como um NP-Difícil por ser uma versão generalizada do problema da mochila, que é um NP-Completo.

## Simplificação do Problema
Para uma melhor abordagem do problema, o varejista, determina os produtos por categoria para a prateleira em questão(por exemplo, garrafas, potes, caixas). Isso permite a redução do problema para o problema da mochila.

# 💭 Solução: Programação Dinâmica
Com o problema resumido, podemos usar a programação dinâmica que garante uma solução ótima.

## 🔧 Como funciona a PD
-  A programação dinâmica divide um problema em subproblemas aninhados
-  Divide estes em uma Matriz $V$ composta por $N$ e $W$. Sendo $N$ = Numero de itens (produtos) a serem alocados e $W$ = capacidade total da prateleira.
-  Cada célula $V[i,j]$ armazena o lucro relacionado aos primeiros $i$ itens com a capacidade $j$ portanto, **$j$ é a capacidade restante da prateleira**.
-  Solução é $V[N,W]$  
-  A complexidade é de $O(N \cdot W)$, isso é chamado de tempo **pseudopolinomial**, rápido se $W$ for pequeno mais inviável para $W$ grandes.
## 📚 **Nomenclatura Relevante**

O artigo usa as seguintes variáveis para o Problema da Mochila:

- $N$: Número total de itens.
-  $W$ (ou $C$): Capacidade (peso) da mochila.    
-  **$w_i$**: Peso do item $i$.
-  **$v_i$ (ou $p_i$)**: Lucro (valor) do item $i$ .    
-  $V[i, j]$: Solução de valor máximo do subproblema com os primeiros $i$ itens e capacidade $j$.

## Ordem de Recorrência
Temos que estabelecer o caso base para a recorrência.

$V[i, j]=\begin{cases} 0 &\text{se} \quad V[i, 0]\\ 0 & \text{se} \quad V[0, j] \end{cases}$

então:

$V[i,j]=\begin{cases} \max(V[i-1,j], \quad v_{i}+V[i-1,j-w_{i}]), & \text{se } w_{i}\le j \\ V[i-1,j], & \text{se } w_{i}> j\end{cases}$


Então a recursão é composta por duas escolhas:

$v_{i}+V[i-1,j-w_{i}]$ 

que é quando o produto é alocado, onde $v_i$ é o produto mais a alocação dos $i$ produtos anteriores, representados por $V[i-1,j-w_{i}]$. 
$j-w_{i}$ representa o espaço do item $i$ ocupando o espaço total $j$. 

enquanto $V[i-1,j]$ representa a escolha de não alocar o item.

## Método Usando o GCD
O Greatest Comun Divisor, que é o maior divisor comum entre os pesos dos itens a serem alocados:

| **Produto ($i$)** | **Largura (Peso, $w_i$​) em cm** | **Lucro (Valor, $v_i$​) por face** | **Faces Máximas (Limite, $b_i$​)** |
| ----------------- | -------------------------------- | ---------------------------------- | ---------------------------------- |
| **Pó A** (1)      | 30                               | 10                                 | 5                                  |
| **Grão B** (2)    | 45                               | 18                                 | 3                                  |
| **Pó C** (3)      | 60                               | 25                                 | 4                                  |
Então o GDC muda a maneira/medida que o produto vai ser analisado para diminuir a complexidade 

$$V[i, j] = \begin{cases} \max(V[i-1, j], \quad v_{i} + V[i-1, j - \frac{w_{i}}{\text{GCD}(w)}]), & \text{se } w_{i} \le j \cdot \text{GCD}(w) \\ V[i-1, j], & \text{se } w_{i} > j \cdot \text{GCD}(w) \end{cases}$$
## Método usando binary splitting

$V[k, j]=\begin{cases} \max(V[k-1,j], \quad v_{i}+V[k-1, j - w'_k] & \text{se } w'_{k} \le j \\ V[k-1, j], & \text{se} w'_{i} > j \end{cases}$

# Complexidade O(N $\cdot$ W)