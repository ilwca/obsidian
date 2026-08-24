### Questão 
Uma metalúrgica deseja maximizar sua receita bruta. A Tabela abaixo ilustra a proporção de cada material na mistura para a obtenção das ligas passíveis de fabricação. O preço está cotado em Reais por tonelada da liga fabricada. Também em toneladas estão expressas as restrições de disponibilidade de matéria-prima.

|                           | Liga baixa resistencia | Liga alta resistencia | disponibilidade M. prima     |
| ------------------------- | ---------------------- | --------------------- | ---------------------------- |
| Cobre                     | 0,5                    | 0,2                   | 16T                          |
| Zinco                     | 0,25                   | 0,3                   | 11T                          |
| Chumbo                    | 0,25                   | 0,5                   | 15T                          |
| Preco ($R\$$ po tonelada) | $R\$$ 3.000            | $R\$$ 5.000           | $\frac{T. minério}{T. liga}$ |
- como misturar os materiais para fazer liga com menos custo?

- a mistura atende as disponibilidades da materia?

Agora precisamos definir algumas coisas...
- **Variaveis**
- **Função**
- **Restrições**
### Variaveis
O que esta variando na tabela de acordo com o minério? **A liga**. então adotaremos $x$ para as duas variaveis, sendo $i$ o indice da liga. Assim temos, $i=1$ para liga de baixa resistencia e $i=2$ para ligas de alta resistencia. ou seja:
$x_1=l.baixa$ 
$x_2=l.alta$

### Função
A nossa função sera com o intuito de maximizar o lucro, ou seja o preço por tonelada. então devemos encontrar um $x_1 \cdot 3.000$, ou seja o material de baixa resistencia que multiplicado por $3.000$ tenha o maior resultado e um $x_2$ que multiplicado pelo $5.000$ tenha o maior resultado. Assim $x_2 \cdot 5.000$. para definir que o valor encontrado tem que ser o maior usamos o termo `maximizar()` ou `max()`. Desta forma, definimos nossa função:
$$ z = max\{f(x)=3.000x_1 + 5.000x_2\}$$

### Restrição
A restrição esta ja definida para cada minerio, conforme da tabela.
então temos:
**cobre**: $0,5x_1 + 0,2x_2 \leq 16$
**zinco**: $0,25x_1+0,3x_2\leq 11$
**chumbo**: $0,25x_1 + 0,5x_2 \leq 15$

Restrição para **Não Negatividade** $x_1\geq0$  e $x_2\geq0$

Assim formulamos o nosso modelo matemático:
$$ z = 3.000x_1+5.000x_2 $$
sujeito a:
$$0,5x_1 + 0,2x_2 \leq 16$$
$$0,25x_1 + 0,3x_2 \leq 11$$
$$0,25x_1 + 0,5x_2 \leq 15$$
---
## Exercicio
Elabore agora para o problema da Dieta:
Para uma boa alimentação, o corpo necessita de vitaminas e proteínas. A necessidade mínima de vitaminas é de 32 unidades por dia e a de proteínas de 36 unidades por dia. Uma pessoa tem disponível carne e ovos para se alimentar. Cada unidade de carne contém 8 unidades de vitamina e 6 unidades de proteínas. Cada unidade de ovo contém 4 unidades de vitamina e 6 unidades de proteínas. Cada unidade de carne custa 3 unidades monetárias e cada unidade de ovo custo 2, 5 unidades monetárias. Qual a quantidade diária de carne e ovos que deve ser consumida para suprir as necessidades de vitaminas e proteínas com menor custo possível ?

|             | Vitaminas | Proteínas | custo ($\$$)            |
| ----------- | --------- | --------- | ----------------------- |
| Ovo         | 4         | 6         | 2,5                     |
| Carne       | 8         | 6         | 3                       |
| necessidade | 32        | 36        | $\frac{necess.}{custo}$ |

- Suprir necessidades com menor custo.
vamos definir:
- **Variaveis**
- **Funcão**
- **Restrições**

### Variaveis
as variaveis devem ser definidas de acordo aquilo que podemos escolher com foco em minimização do custo. Então podemos escolher a quantidade de ovos e quantidade de carne em relação ao custo:
$x_1= quantidade\ de\ ovos$ 
$x_2=quantidade\ de\ carnes$
### Função
como nossa função é de minimizar, pois estamos procurando o menor custo que atenda as restrições faremos:
$$z = min\{f(x)=2,5x_1+3x_2\}$$
### Restrições
Para cada unidade de ovo temos 4 vitaminas e 6 proteinas e o minmo de vitaminas e 32 e de proteinas e 36, então temos:
$$4x_1+8x_2\geq32$$
e para carne, temos 8 vitaminas e 6 proteinas com minimo respectivo em 32 e 36, assim temos:
$$ 8x_1+6x_2\geq36$$
e com restrição de não negatividade temos:
$$x_1\geq0$$
$$x_2\geq0$$
portanto, nossa restrição é
$$\begin{cases}4x_1+6x_2\leq32 \\  8x_1+6x_2\leq36 \\ x_1\geq0 \\ x_2\geq0
\end{cases}$$
Assim formulamos o nosso modelo matemático:
$$z=32x_1+36x_2$$
sujeito a:
$$\begin{cases}4x_1+8x_2\leq32 \\  8x_1+6x_2\leq36 \\ x_1\geq0 \\ x_2\geq0
\end{cases}$$
---
## Exercicio
**Problema da Ração**:
Uma fazenda precisa alimentar seus animais com uma mistura de **ração A** e **ração B**.
Cada quilograma de ração possui as seguintes características:

|                    | Proteínas | Fibras | Custo (R$/kg) |
| ------------------ | --------- | ------ | ------------- |
| Ração A            | 6         | 4      | 2,00          |
| Ração B            | 3         | 8      | 1,50          |
| Necessidade mínima | 30        | 32     |               |
Para garantir uma alimentação adequada, cada animal deve receber **no mínimo 30 unidades de proteínas** e **no mínimo 32 unidades de fibras** por dia. A fazenda deseja determinar **quantos quilogramas de cada tipo de ração devem ser utilizados diariamente**, de modo a **atender às necessidades nutricionais com o menor custo possível**.

Vamos definir a quantidade que atenda aos requisitos com menor valor:
### Variáveis
como o foco é a redução do custo para um valor minimo de proteinas e fibras, temos $x_i$ igual a quantidade de ração. Denotaremos $i=1$ para Ração A e $i=2$ para Ração B.
Assim teremos: $x_1=racaoA$ e $x_2=racaoB$.
### Função
minimizar o custo, então $z=min\{f(x)=2x_1+1,5x_2\}$
### Restrição
$$\begin{cases}6x_1+3x_2\geq30 \\ 4x_1+8x_2\geq32 \\x_1\geq0 \ e \ x_2\geq0 \end{cases}$$
modelo matemárico:
$$z = 2x_1+1,5x_2$$
sujeito a:
$$\begin{cases}6x_1+3x_2\geq30 \\ 4x_1+8x_2\geq32 \\x_1\geq0 \ e \ x_2\geq0 \end{cases}$$
