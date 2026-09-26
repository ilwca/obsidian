[[pg-todo]]
# Pesquisa
Qual o impacto que a poda e quantizacao pode trazer a acuracia, latencia e tamanho do modelo, e qual a proporcao ideal entre estes metodos de otimizacao em detrito da eficiencia computacional e desempenho.

## Objetivos Gerais
fazer analise e avaliacao pratica de tipos de podas estruturadas e tecnicas de quantização, com intuito de encontrar o melhor balanço entre a eficiencia energética e perca de desempenho da rede por meio de tecnicas de computação aproximada.

## Objetivos Especificos
1. Implementar e avaliar modelos de pequeno e médio porde de redes neurais CNN e MLP, fazer o levantamento de seus resultados, latência e consumo.
2. Aplicar diferentes niveis de quantização pós treinamento aos modelos desenvolvidos.
3. Aplicar diferentes niveis de poda estruturada por magnitude.
4. Avaliar eficiencia do modelo treinado e significancia do re-treinamento.
5. Aplicar e avaliar resultados obtidos apos a aplicação das tecnicas de poda e quantização em um modelo, em diferentes niveis de quantizacao e diferentes niveis de poda.
6. Analisar em quais situações existem um resultado de eficiencia energética consideravel e ainda um otimo desempenho da rede. Levantamento de metricas:
``` metricas
Accuracy
Model Size
Number of Parameters
MACs
Inference Latency
``` 

# 2. Referencial Teorico
## 2.1 Redes Neurais
Redes neurais ou Redes neurais artificiais são sistemas computacionais expirados biologicamente nos sistema nervoso neural humano. Assim como o cerebro humano, as redes neurais tem a capacidade de aprender padrões e comportamentos a partir de um conjunto de entrada com o intuito de classificar ou otimizar uma saída [[pg-referencias#O'Shea|01]].
Normalmente as redes neurais são compostas de uma camada de entrada, camadas ocultas compostas por neuronios e suas funções de ativação e a camada de saida.

### 2.1.1 Neuronios artificiais
As camadas de uma rede neural e composta por varios neuronios, estes neuronios artificiais são funções de modelos matemáticos que recebem um input de neuronios da camada anterior e os multiplica a um determinado peso daquela conexão. Todos os sinais recebidos e ponderados são somados a um viés que enfim passará por uma funcao de ativação [[pg-referencias#krenker|02]].
### 2.1.2 Pesos, bias e funcoes de ativação
Ao inicializar uma rede, todos os pesos recebem um valor aleatorio dentro da escala de ajuste. Os valores dos pesos sao ajustados a partir do treinamento, que envolve uma grande sequencia de entradas na primeira camada. Posteriormente, na saída é calculado o gradiente de erro da função, isto envolve o calculo da distancia euclidiana do vetor de todos os pesos dos neuronios. Os valores cujo obtiverem menor correspondencia com o vetor de entrada, são ajustados em direção a ele [[pg-referencias#krenker|02]]. Este processo é realizado algumas vezes para cada entrada.

O viés compoem a entrada de cada neurónio sendo somada juntamente com cada entrada da camada anterior. Este parametro serve para a locomoção da funcão de ativação, fazendo com que alguns neurónios sejam menos ativados e outros mais.

A ativação é dada por uma funcao de ativação do resultado de uma combinação lienar dos inputs dos neuronios e o bias. Considerando $z = a_1w_{11}+a_2w_{21}+a_3w_{31} + b$, onde:
- $x$ → entrada da camada;
- $b$ → viés;
- $z$ → resultado da combinação linear;
- $f$ → função de ativação;
- $a$ → **ativação**, ou saída da camada.
Assim obteremos um $a$ oriundo de $a=f(z)$. 
As funções de ativação são transformações aplicadas ao valor recebido da camada anterior para garantir a não linearidade da rede. As principais funçõe de ativação é a ReLU [[pg-referencias#Rastegari|03]].

### 2.1.3 Treinamento
As redes neurais possuem tres tipos de paradigma de aprendizado de máquina; o não supervisionado, supervisionado e por reforço. Para cada um destes metodos de treinamento citados existem varios tipos de algoritmos, como algorimto genético, otimização bayesiana e outras heuristicas de aprendizado [[pg-referencias#krenker|02]].

### 2.1.4 Aprendizado Supervisionado
O aprendizado supervisionados de redes neurais consiste no constante ajuste de pesos dos neurónios por época. O ajuste é definido com base no erro obtido na saída para qualquer tipo de entrada valida para aquele conjunto de treinamento [[pg-referencias#krenker|03]].

## 2.2 CNNs
As redes neurais convolucionais *(Convolutional Neural Network - CNNs)* são redes neurais feed-forwar, ou seja, de propagação direta, que utillizam de uma camada de convulação de da entrada com kernels para obterem caracteristicas e padrões abstratos das entradas [[pg-referencias#Rastegari|04]][[##Song|05]]. As CNNs tem apresentados otimos resultados em tarefas de visão computacional e classificação [[pg-referencias#Song|05]]. Porém o processo de treinamento destas redes envolve uma quantidade massiva de dados de hiperparametros e milhares de operações aritiméticas como no caso da convulação da rede.
### 2.2.1 Convulação
A convolução é um processo iterativo realizado na entrada de uma camada convulacional para obtenção de valores continuos que serão somados ao viés e aplicados na função de ativação. Este processo, ira gerar os mapas de carcteristicas _(feature maps)_ ou ativações que funcionam como os dados de entrada para a camada seguinte. A formula da convolução de um determinado kernel aplicado em uma matriz de entrada é:
$$a_i = \Omega(z_i), z_i = \sum^k_{i=1}w_i\times a_i+b \tag{1}\label{eq.conv}$$
A função de ativação esta sendo está sendo representada por $\Omega$. Note que $w_i\times a_i$ denota a multiplicacao de uma matriz de menor tamanho pelos respectivos valores da matriz de entrada. 
### 2.2.2 Kernels
Os kernel são pequenas matrizes de pesos, que percorrem toda a matriz de entrada, executando a operação da _figura(1)_ em cada posição da matriz. o resultado obtido $a_i$ irá compor a matriz de saída da camada convolucional, ou seja, o mapa de caracteristica da entrada.
### 2.2.3 Função de ativação
A ativação do valor de um peso é dada por uma função de ativação. A entrada da função de ativação é a combinação linear da ativação da camada anterior com o peso da conexão, como visto na figura(2).$$z = a_1w_{11}+a_2w_{21}+a_3w_{31} + b$$
onde: 
- $w$ → peso;
- $b$ → viés;
- $z$ → resultado da combinação linear;
- $f$ → função de ativação;
- $a$ → **ativação**, ou saída da camada.
Desta forma a função de ativaçãoa atua no valor do resultado da combinação linear $f(z)$ para garantir a não linearidade da rede [[pg-referencias#Liang|03]]. Existem diferentes tipos de função de ativação, entre elas, as principais são a Sigmoid, Tanh e ReLU.  ==A *Retified Linear Unity* é uma função de ativação que zera todos os valores inferiores a zero e mantem valores positivos, assim resultando em uma alta taxa de zeros, abrindo margem para maior compressão de pesos.== Em analise
### 2.2.4 Pooling
O pooling é o agrupamento dos mapas de caracterisiticas, reduzindo o tamanho das matrizes de entrada e gerando maior abstração dos dados da rede. O pooling utiliza de matrizes, normalmente $2\times2$ que percorrem a entrada e agrupando os valores respectivos da entrada de três maneiras possiveis; conservando o maior valor, o menor ou a media. 
### 2.2.5 Camadas Totalmente Conectadas
O maior nivel de abstração dos pesos de uma rede origina as FCL *(Fully Connected Layers),* que são as camadas totalmente conectadas. Apos a ultima camada convulacional, as matrizes de entrada são reduzidas de dimensão $\mathbb{R}^2\rightarrow\mathbb{R}^1$. Desta forma, cada indice da matriz de entrada se torna um neurónio com peso de seu índice.
### 2.2.6 Custo Computacional
Como visto, o processo convolucional é composto por uma grande quantidade de multiplicações acumuladas *(MACs)*. Considerando $\ref{eq.conv}$, temos que $w$ é uma matrix de pesos $32\times32$ e $a$ sendo 16 filtros $3\times3$; para obtermos 1 mapa de caracterisitcas seria necessário fazer $27$ operações MAC. Calculando as operações que existe na saída para cada posição do kernel na matriz de entrada teremos $14.400$ operações a serem executadas $27$ vezes, resultanddo em $388.800$ operações de multiplicação e acumulação para geração de $16$ mapas de cacteristicas em uma unica camada. 
Esta simulação é apenas um simples exemplo com uma entrada razoavel. Estes numeros podem crescer exponencialmente de acordo com o tamanho da matriz do mapa de entrada, número de canais, tamanho do kernel e numero de filtros.
Como as CNNs realizam grandes numeros de operações aritmeticas, o tamanho da representação numerica impacta de forma significativa o custo computacional e o armazenamento da rede.

## LeNet-5

![[mohd1-21-small.gif]]
