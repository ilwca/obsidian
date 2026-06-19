## Estatísticas
A estatística é uma parte da matemática aplicada que coleta, organiza, analisa e interpreta dados para a tomada de decisões baseadas em informações.
A definição de estatística pode ser divida em tópicos, como:
- Coleta 
- Organização
- Resumo 
- Análise 

### Dashboard 
É um painel que permite ter uma visão geral em uma única pagina de dados críticos, formados por tabelas, gráficos e métricas.

## Gráfico
Um gráfico deve conter elementos básicos para apresentação dos dados como o titulo, o gráfico(propriamente dito) e a fonte.
Existem diversos tipos de gráficos, como:
- Diagramas
- Cartogramas
- Estéreogramas
- Isogramas
- Organogramas
- Fluxogramas
- Pictogramas
- Compostos
Dentro dos Tipos de **Diagramas temos**:
- Coluna
- Barras
- Linhas
- Pizza
- Pontos
entre outros.

---
07/05

# Probabilidade
## Espaço Amostral
o lançamento de uma moeda tem o seguinte espaço amostral:
$$S=\{Ca, Co\}$$

O lançamento de um dado tem o seguinte espaço amostral:
$$S=\{1,2,3,4,5,6\}$$
Ou seja, o espaço amostra é o conjunto de resultados possíveis dentro de experimento aleatório.
Dois lançamentos sucessivos de uma moeda pode-se obter o seguinte espaço amostral:
$$S=\{(Ca, Co), (Ca, Co), (Ca, Co), (Ca, Co)\}$$
## Evento
Qualquer subconjunto do espaço amostral de um experimento aleatório. por exemplo, considerando o caso acima, $(Ca,Co)$ em S no experimento aleatório do lançamento das moedas, deste modo, podemos dizer que $A\subset S$.
Exemplos:
Considerando o experimento aleatorio do lancamento de um dado.
1. obter um numero par na face superior.
$$A = \{2,4,6\}$$
2. Obter um numero menor ou igual a 6.
$$A=\{1,2,3,4,5,6\}, A=S$$
3. Obter o número 4 na face superior.
$$A = \{4\}$$
## Probabilidade
Chama-se probabilidade de um evento $A(A\subset S)$ o número real $P(A)$, tal que:
$$P(A)=\frac{n(A)}{n(S)}$$
$n(A)$ = Número total de elementos de A
$n(S)$ = Número total de elementos de S

**Exemplo:**
Considerando o lançamento de um dado.
	Qual a probabilidade do evento A "obter um número par na face superior":
$S = \{1,2,3,4,5,6\}, n(S) = 6$
$A = \{2,4,6\}, n(A)=3$

$$P(A)=\frac{n(A)}{n(S)}$$
$$P(A)=\frac{3}{6}= \frac{1}{2}$$
---
# Regressão 
função definida pelos valores de $X$ e $Y$ onde $Y$ é a variável dependente da variável independente de $X$. Onde os valores da função para $Y$ é dado por:
$$Y = aX+b$$
onde $a$ e $b$ são os parâmetros da função definidos por:
$$a = \frac{n \sum x_i y_i \text{ }-\text{ }\sum x_i \sum y_i}{n \sum x_i^2 -(\sum x_i)²}$$
$$b = \overline{y} + a\overline{x}$$
Assim definimos a equação de regressão linear, denotada por:
$$\widehat{Y}=aX+b$$
que definirá os valores aproximados para a função.

### Exemplo
