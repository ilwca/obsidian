---

---
---
# 04/08
## Introdução
A **Pesquisa Operacional** é um ramo da ciência que lida com a otimização do desempenho de sistemas.
Otimizar:
- Maximizar Lucros
- Maximizar Satisfação
- Minimizar Custos
- Minimizar Riscos

## Modelos de Programação Linear
- Teoria Matemática: Kantorovich, 1939
- 1940: Algoritmo Simplex

### Função objetivo
- **Minimizar** custo, tempo, risco, poluição . . . ou
- **Maximizar** lucro, qualidade, segurança . . . ou 
- **Encontrar** qualquer solução viável
### Restrições
- **Disponibilidade** de recursos, . . .
- **Operacionais** horários de trabalho, tempo de máquina, . . .
- **Limites** venda em escala, . . .

### Problema da Dieta
Quantidades minimas de vitaminas e proteínas ingeridas
- $V_{min}=32$ 
- $P_{min}=36$

carne $x_1$:
- $C_v = 8$
- $C_p= 6$
- $\$=3$
ovo $x_2$:
- $O_v= 4$
- $O_p=6$
- $\$=2.5$

função $z$
$$3x_1+2,5x_2$$
A solução tem que satisfazer os requerimentos nutricionais:

| nutriente | Qtd. Minima |
| --------- | ----------- |
| vitamina  | 32          |
| proteina  | 36          |

---
# 25/08
## Simplex
O algoritmo simplex é denotado por:

Dada uma solução basica para um PPL.
(if) Se $z_j-c_j \geq 0$,  $\forall j \in I_n$ , a solução dada é uma solucao ótima. PARE.
(else) Senão, escolhe-se um $k \in I_n$ para qual $z_k-c_k < 0$;

### solução basica viável (SBV)
Uma solucação basica viavel é denotada por:
$$x(x_0, 0), \ \ x_0\geq0 ,\ x_n=0$$
.
.
.

### Exemplo
maximizar
$$z=3x_1+5x_2$$
sujeito a:
$$\begin{cases}x_1 & \leq4 \\
\ \ \ \ \ \ +x_2 & \leq6 \\
3x_1+2x_2&\leq18 \\
x_1,x_2&\geq0
\end{cases}$$
Associar as restrições nao triviais as variaveis de folga. 3 restrições $\rightarrow$ 3 variveis de folga. 
Lembrando que as variaveis de folga são em relação ao foco do problema, como o problema e de maximizar, vamos **somar** variaveis de folga. Assim temos:

$minimizar$
$$z=3x_1+5x_2+0x_3+0x_4+0x_5$$
$sujeito \ a:$
$$\begin{cases}x_1 \ \ \ \ \ \ \ \ \ \ \ +x_3& \leq4 \\
\ \ \ \ \ \ +x_2 \ \ \ \ \ \ \ \ \ +x_4& \leq6 \\
3x_1+2x_2\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ +x_5&\leq18 \\

\end{cases}$$
$x_j\geq0 \ j=1,2,3,4,5$

A partirn da daterminantes podemos formar a matriz $A$
$$A = (a_1,a_2,a_3,a_4,a_5)=\begin{pmatrix}
1&0&1&0&0\\
0&1&0&1&0\\
3&2&0&0&1
\end{pmatrix} \ \ b=\begin{pmatrix}4\\6\\18\end{pmatrix}$$
e $c=(3,5,0,0,0)$
Onde o $c$ é definido a partir da função a ser minimizada, como: $$z=3x_1+5x_2+0x_3+0x_4+0x_5$$
$$c=(3,5,0,0,0)$$
Agora vamos definir a matriz base($I_B$) e a não base($I_N$), para definir como ja temos uma matriz de indentidade em $A$, esta mais facil decidir quem é $I_B$ e $I_N$.
$$não\ base=\begin{pmatrix}
1&0\\
0&1\\
3&2
\end{pmatrix},\ \
base=\begin{pmatrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{pmatrix}$$
desta forma, temos os indices das colunas da base e nao base como:
$I_N=\{1,2\}$ e $I_B=\{3,4,5\}$

_!Inversa da matriz ou matriz inversa. Dada uma matriz $A$, sua matriz inversa $A^{-1}$ é uma matriz cujo a multiplicação com a matriz original resulta na matriz identidade.!_

Determinamos agora a inversa da matriz base, denotada por $B^{-1}$. Como a nossa matriz base $B$ é uma matriz de identidade, sua inversa é a propria matriz, portanto:
$$B=\{a_3,a_4,a_5\}\ e\ B^{-1}=\begin{pmatrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{pmatrix}$$
Determinando $u$, que é $u=c_BB^{-1}$ , onde $c_B$ é p conjunto $c$ com os indices da matriz $B$, portanti os indices $(3,4,5)$, assim estes indices em $c(0,0,0)$. Então:
$$u=c_BB^{-1}=(0,0,0) \cdot \begin{pmatrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{pmatrix} = (0,0,0)$$
Agora vamos definir o valor da iteração atual $\bar{x}$. Assim:
$$\bar{x}_B = B^{-1}b=\begin{pmatrix}
\bar{x}_3 \\
\bar{x}_4 \\
\bar{x}_5 \\
\end{pmatrix} = \begin{pmatrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{pmatrix} 
\cdot
\begin{pmatrix}
4\\
6\\
18\\
\end{pmatrix} = \begin{pmatrix}
4\\
6\\
18\\
\end{pmatrix}$$
nosso valor de $\bar{z}$ é definido por:
$$\bar{z} = c_BB^{-1}b = ub$$
por $ub$ temos:
$$\bar{z}=ub=(0,0,0)\cdot \begin{pmatrix}
4\\
6\\
18\\
\end{pmatrix} = 0$$
Portando, considerando a condição inicial de $z_j,c_j\geq0,\ \ \forall j\in I_B$  esta solução não é otima, pois $z_j=0$.