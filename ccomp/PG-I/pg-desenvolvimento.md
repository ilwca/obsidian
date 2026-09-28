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

## 2.3 LeNet-5
A primeiro uso do termo "convoluçõa" foi na construição de uma das primeiras redes multicanais de retropropagação. O processo de aprendizado por _back-propagation (BP)_ consiste no reajuste de pesos após obter o erro de uma saída, onde o gradiente de erro apontará quais pesos mais influenciaram o resultado erroneo, e assim sera feito o ajuste do peso. Essa rede foi desenvolvida para o reconhecimento de digitos postais manuscritos proposta por Yann LeCun et al.(1988) e denominada de LeNet [[pg-referencias#Lecun|06]].
### 2.3.1 Arquitetura da LeNet-5
A _figura(2)_ amostra a anatomia de uma LeNet composta por camada de entrada das imagens; $3$ camadas convulacionais; $2$ camadas de agrupamento e $3$ camadas totalmente conctadas, onde a ultima faz a predição do simbolo de entrada.
![[mohd1-21-small.gif]]
Esta simplicidade de arquitetura e otimos resultados de reconhecimento fez com que a LeNet-5 se tornasse a mais famosa rede de retropropagação e classificação [[pg-referencias#Zewen|07]]. 
Além da arquitetura das redes neurais, é importante considerar os dados usados para o treinamento destes modelos e posteriormente utilizados para realizar inferências. Assim, faz-se necessário apresentar as bases de dados empregadas neste trabalho e suas principais características.
### 2.3.2 MNIST
O modified NIST, é um dataset que conta com $60.000$ amostras de $32\times32$ pixels manuscritos de $0$ a $9$ de $500$ escritores diferentes, criada pelo _National Institute of Standars and Technology_ [[pg-referencias#Lecun|06]], especialmente para a rede LeNet-5. 
### 2.3.3 CIFAR-10
Com um nivel de complexidade maior que o MNIST, o CIFAR é um data set que tambem conta com $60.000$ imagens porém coloridas, sendo $50.000$ para treinamento e $10.000$ para testes. O CIFAR-10 conta com $10$ classes de como avião, carro, gato, cachorro e etc. Desta forma cada classe possui $5.000$ imagens para treinamento e $1.000$ para inferência [[pg-referencias#Zewen|07]].

## 2.4 Tecnicas de Aceleração e Compressão de Redes
Tendo em mente, os processos e operações que envolvem redes neurais profundas DNNs, observamos que existe uma grande quantidade de custo computacional envolvido, tanto em camadas convolucionais que compoem 99% das operações MAC [[pg-referencias#Choudhary|08]], quanto da grande quantidade de parametros das camadas densas. Assim, compreendemos dois fatores que acarretam diretamente o aumento de custo computacional e aumento do tamanho da rede. Com isso, um dos propósitos deste artigo é a apresentar e testar metodos de aceleração e compressão de redes, analisando o trade-off entre acurácia, tamanho e custo computacional da LeNet.

### 2.4.1 Redundância
A redundância é causada pela quantidade de dados ou parametros irrelevantes, que nao causam impacto significativo na saida da rede seja ela em parâmetros, conexões, neuronios. Desta forma, a redundância pode ser gerada de diversas forma, por parametros que geram pesos de valores similares, neurónios que aprendem caracteristicas semelhantes e filtros gerando caracteristicas sobrepostas [[pg-referencias#Liang|03]]. Então a redundância de informações  abre margem para técnicas que possibitam a redução significativa da rede as vezes com pouco ou nenhum impacto na precisão desta, tudo isso por meio de métodos de compressão.
### 2.4.2 Compressão
A compressão de redes se da pela adoção de técnicas como poda e quantização, que buscam remover quaisquer tipo de calculos considerados desnecssários para o resultado ou a diminuição da precisão das operações realizadas no treinamento e inferência, afetando diretamente na compressão e aceleração da rede.
### 2.4.3 Poda
A poda de rede envolve a remoção de parâmetros que não impactam consideravelmente a precisão da rede. Essas condições podem ocorrer quando o coeficiente de peso for zero ou são redundantes.
### 2.4.4 Quantização
A quantização de rede envolve a substituição de tipos de dados por tipos de dados de largura reduzida. Por exemplo, substituir o ponto flutuante de $32$ bits ($FP32$) por inteiros de $8$ bits ($INT8$). Os valores podem frequentemente ser codificados para preservar mais informações do que uma simples conversão [[pg-referencias#Liang|03]].
## 2.5 Quantização de Redes
Proposta em 1990, a quantizacao e um famoso processo de transformação de valores continuos em valores discretos por meio da aproximado ou normalizado dos valores. O [[#Pooling |pooling]] e o compartilhamento de parametros tambem se enquadram neste processo [[pg-referencias#Liang|03]].
A maioria das redes atualmente usa uma representação de FP32 _(float point de 32 bits ou seja 8 casas decimais)_ que é mais do que necessaria na maioria das vezes. Desta forma, aproximações com menos bits melhoram a eficiencia com pouca perca de informação com o uso de FP16 ou INT8. 
A quantização de 8 bits é amplamente aplicada na prática com uma boa razão entre a precisão e a compressão, e é amaplamente aplicada  em processadoers atuais e em hardware personalizadao
### 2.5.1 Quantização de pesos e ativações
Inicialmente o processo de quantização envolvia somente os paramêtros da rede; depois de alguns avanços, estudos mostraram que a combinação de técnicas de quantização pode reduzir os pesos armazenados de forma significativa. Na quantização parcial, por exemplo, é usado uma tabelas para o armazenamento dos parametros e a quantização é feita somente nos estados dos pesos. Desta forma, o foco da quantização se mantêm nos parâmetros pois viéses e ativações nao tem impacto significativo na compressão, como monstrado por Liang et al (2021).

### 2.5.4 Quantização Uniforme
Na quantização uniforma a rede tem seus pesos normalizados e quantizados e recebendo todos a mesma precisão numérica. Considerando uma rede fomada por conjuntos de camadas convulacionais ou FCL, e denotando seu parametros como $\Theta$.  definimos $R$ como a representação numérica em bits das camadas $\Theta$. Deste modo, $R=8$ bits significa que os parametros das camadas serão representados com precisão de $8$ bits.

### 2.5.5 Escala e Zero-Point
Agora entramos em um dos pontos mais curiosos da quantização.  O processo de quantização não é somente a redução de precisão de um numero é determinado por meio de uma escala $s$ e um zero-point. O processo é denotado por:
$$\hat{x} = round(\frac{x}{s}+z)$$
onde:
$\hat{x}$ = peso quantizado
$s$ = escala
$x$ = peso sem quantizar
Desta forma a escala determina a relação do valor original e o quantizado, onde o zero-point determina o intervalo de quantização.
### 2.5.5 Quantização Simétrica e Assimetrica
Na quantização simetrica ou sem deslocamento, a ideia é simples. Trabalhamos com pesos de valores em um intervalo simétrico que varia em uma escala $s$.
Exemplo: com um $s = 1$ teremos uma variância nos pesos de vai de $-1$ a $1$. Considerando $x$ como o valor do peso temos:$x\in [-1; 1]$ com o "meio" em $z$, que é $0$.
Porêm pode ser trabalhado com qualquer escala de $s$ a partir do método assimétrico.

Na quantização com deslocamento ou asimétrica, trabalhamos com uma escala $s$ que não possui "meio" em $0$. Considerando o exemplo de um intervalo de $x \in [-0.2; 1]$, então é definido um novo valor para o *zero-point*, já que o intervalo não é simétrico com $z$ em $0$. 

### 2.5.5 Granularidade da Rede
Por definição geral, granularidade é o nivel de detalhe ou grau de divisao de um sistema, modelou ou conjunto de dados em partes menores. Assim a aplicação de ajuste de dimensão e escala de dados define a precisão de referencia de um valor com relacao a sua escala de ajuste. Exemplo: $w=\{0.02,\ 0.003,\ 0.00,\ 5.0\}$. Desta forma, podemos definir a escala de variação destes dados é de $0$ a $5$. Porêm, percebe-se que a precisão de referência para o valor $0.003$ diminui.
Assim, teremos duas formas de abordar isso na quantizacao de redes, que é quantização por canal e por camada.
Na quantização **Por Camada**, o peso da camada inteira é adotada por um unico scale.
$$W=​\begin{bmatrix}0.1 & 0.2 & 0.3 \\
1.0 & 1.2 & 1.5 \\
-0.4 & 0.5 & 0.6 \\
\end{bmatrix}$$
Então sera definido um unico $S$ para aquela camada, não importa se varia de $0$ a $1$ ou de $-1$a $5$. 
Na quantização por canal, cada canal possui seu próprio paramêtro de escala, então teremos $S_1, S_2, S_3, ...$ Ao invés de um unico $S$.

### 2.5.6 Largura de bits
A largura de bits representa a quantidade de bits de precisão serão representados os valores numericos da rede, canal ou camada. A LeNet-5 como maioria utilizar de $FP32$ em toda a rede de forma estática. A precisão numérica pode também ser definida de forma dinâmica entre camadas de uma rede. Considerando $l$ o numéro da camada, podemos definir a largura de bits da camada $\Theta_l$ com $R_l$. Desta forma,  $R_1=4, R_2=8,  R_3=2$ denota que a camada $\Theta_1$ utiliza 4 bits de precisão, a $\Theta_2\ 8$ bits  e $\Theta_3$ $2$. Assim, é possivel ajustar a precisa por camada buscando a menor perca de precisão.

### 2.5.7 Quantização Pós Treino
O PQT *(Pos-Training Quantization)* corresponde a applicação da quantização após o treinamento da rede. Nesta abordagem a rede é treinada normalmente com a precisão padrão. Após o processo de treinamento seus parâmetros sao quantizados. Esta abordagem consequentemente diminui a precisão de maneira significativa exigindo o retreinamento [[pg-referencias#Liang|03]]. 
### 2.5.8 Treinamento com Reconhecimento de Qantização
No método QAT _(Quantization-Aware Training)_, o treinamento é feito pensado na quantização, ou seja, ciente de que irá haver um erro somado após o treinamento devido a quantiazação. Dessa forma, o treinamento pode adaptar os parâmetros do modelo considerando as limitações impostas pela representação de menor precisão.

## 2.6 Poda de Rede
Um dos maiores limitadores para a implementação de DNNs em sistemas com limitações computacionais e de armazenamento sempre foram o tamanho e largura de banda. A poda contribui para a redução de ambos visto que sua função é a remoção de parametros redundantes ou ínfimos, assim, liberando bits de armazenamento e poupando cálculos insignificantes [[pg-referencias#Liang|03]]. Existem diferentes tipos de poda de rede, a poda nao estruturada e estruturada, poda de neurónios e conexões e a poda estática e dinámica.
### 2.6.1 Poda Não Estruturada
Ao seguirmos o principio da poda de remover valores proximos de zero, obteriamos estruturas esparssas ou irregulares [[pg-referencias#Liang|03]], dificultando a exploração ou computação.
### 2.6.2 Poda Estruturada
A poda estruturada remove grupos inteiros de neuronios, filtros, linhas ou colunas de matrizes, removendo até camadas quando viável. 
### 2.6.3 Poda em Magnitude
Após a constatação de que pesos com valores grandes tem maior impacto no resultado, a poda por magnitude implementada em tempo de execução, faz a busca por pesos ou caracterisitcas desnecessárias para e as remove durante a predição, removendo valores tanto no kernel ou nos mapas de características.
### 2.6.3 Retreinamento pós Poda
Segundo Liang et al.(2021), a maioria dos paramêtros removidos em redes podadas são oriúndos das FCLs e que o retreinamento, apesar de computacionalmente oneroso, resulta em ganhos satisfatórios na acurácia, alem de uma compressão de até $13\times$ da rede.


