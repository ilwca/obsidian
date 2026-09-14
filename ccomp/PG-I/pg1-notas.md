# Artigos
## Poda e quantização para aceleração de redes neurais profundas: uma revisão
[ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0925231221010894)

**Contribuições deste Artigo:**
- Apresentar revisao das tecnicas de compresssão de rede, que é a poda e a quantizão. e tambem comparação com metodos mais avancados diponiveis;
- Classificar metodos de poda em Offline ou Tempo de Execução;
- Analise de resultados qauntitativos das tecnicas e estruturas de quantização.
### DNN (Deep Neural Network)
Geralmente necessita de ambientes computacionais com maior desempenho, envolvendo aprendizado por transferencia e treinamento adicional.
### Conexoes por camada
normalmente camadas _feedfoward_ tem para cada neuronio $N²$ conexoes ($FCLs$). Porem podem ser reduzidos tambem o numero de conexoes, considerando apenas o neuronio do caminho direto reduzindo para $N$ conexões.
## Poda de Rede
A poda de rede envolve a remoção de parâmetros que não impactam a precisão da rede. Essas condições podem ocorrer quando o coeficiente de peso for zero ou são duplicados.
Existem alguns tipos de poda de rede.
- Poda Estruturada e Não Estruturada
- Poda de Neuronios e Conexões
- Poda Estatica e Dinâmica
### Poda Estática
A poda estatica acontece em neuronios offline após o treinamento e antes da inferencia. Geralmente a poda estatica acontece em três etapas: 1) seleção dos parametros a serem podados; 2) escolha do metodo de poda; 3) re-treinamento ou fine-tuning.

_O retreinamento da rede podada pode melhorar o desenpenho da rede podada para ser comparável com a original, mass isso leva tempo e custo_.
==$\uparrow$ Algo a ser discutido? até que ponto o retreinamento e eficiente em redes podadas? ==

## Poda Não Estruturada
### LASSO
O lasso é uma função de esparcidade nos pesos da rede, pois o LASSO reduz os pessos menos significantes a caracteristicas de menor valor absoluto.
### Critérios da Poda
O processo central de uma rede é a [[#Convulação]], ela envolve três partes:
1. Caracteristicas de entrada produzidas
2. Pesos produzidos na fase de treinamento
3. Valores de bias 
O processo de convulação pode criar pesos de valor zero ou caracteristicas que geram a saída zero. Outro fator são caracteristicas que resultam no mesmo valor.
## Quantizacao de Rede
A quantização de rede envolve a substituição de tipos de dados por tipos de dados de largura reduzida. Por exemplo, substituir o ponto flutuante de 32 bits (FP32) por inteiros de 8 bits (INT8). Os valores podem frequentemente ser codificados para preservar mais informações do que uma simples conversão.

Proposta em 1990, a quantizacao e um famoso processo de substituir valores continuos por um aproximado ou normalizado simbolos ou valores discreto ou inteiros. O [[#Pooling |pooling]] e o compartilhamento de parametros tambem se enquadram neste processo.
A **Quantizacao Parcial** utiliza de algortmos de agrupamento como o [[Kmeans]] para quantizar o estado dos pesos e em seguida armazenar parametros em arquivos compactados.
A maioria das redes atualmente usa uma representacao de FP32 (float point de 32 bits ou seja 8 casas decimais) que e informacaoa mais do que necessaria na amarioria das vezes. Desta forma, aproximacoes com menos bits melhoram a eficiencia com pouca perca de informacao como uso de FP16 ou INT8. 
A quantizacao voltou a ser estudada em 2010, quando a quantizacao de INT8 foi implementada para a aceleracao da inferência sem impacto significativo na precisão de uma rede.

### PTQ (Pos-Training Quantization)
processo convencional de quantizacao em uma rede apos seu periodo de treinamento
```
                 TREINAMENTO
                     ↓
              Rede FP32 treinada
                     ↓
                QUANTIZAÇÃO
                     ↓
              Rede quantizada
``` 

### QAT (Quantization-Aware Training)
Em português significa, treinamento com reconhecimento de quantizacao. Desta forma, diferente da **PTQ**, a rede esta sendo treinada, sabendo que futuramente sera quantizada e tera um _erro_ que irá aparecer na inferencia. Assim, a rede é treinada considerando os impactos da quantizacao, porem envolve um treinamento adicional.

### Granularidade
Por definição geral, granularidade é o nivel de detalhe ou grau de divisao de um sistema, modelou ou conjunto de dados em partes menores. Assim a aplicação de ajuste de dimensão e escala de dados define a precisão de referencia de um valor com relacao a sua escala de ajuste. Exemplo: $w=\{0.02,\ 0.003,\ 0.00,\ 5.0\}$. Desta forma, podemos definir a escala de variação destes dados é de 0 ----- 5. Porêm, concordamos que a precisao de referencia para o valor $0.003$ diminui.
Assim, teremos duas formas de abordar isso na quantizacao de redes, que é quantização por canal e por camada.
#### per-layer / Por Camada
Na quantização **Por Camada**, o peso da camada inteira é adotada por um unico scale.
$$W=​\begin{bmatrix}0.1 & 0.2 & 0.3 \\
1.0 & 1.2 & 1.5 \\
-0.4 & 0.5 & 0.6 \\
\end{bmatrix}$$
Então sera definido um unico $S$ para aquela camada, não importa se varia de `0 --- 1` ou de `-1 --- 5`. 
#### Per-channel / Por Canal
Na quantização por canal, cada canal possui seu próprio paramêtro de escala, então teremos $S_1, S_2, S_3, ...$ Ao inves de um unico $S$.

". . . Pensando de forma holisitica e hierárquica, temos como foco de estudo e abordagem:"
```
Quantização
│
├── Quando?
│   ├── PTQ
│   └── QAT
│
├── Granularidade?
│   ├── Per-layer
│   └── Per-channel
│
└── Precisão?
    ├── INT8
    ├── INT4
    ├── INT2
    └── ...
```

Desta forma podemos estudar e trabalhar configurações diferentes no processo de treinamento e inferencia da rede.

### Pooling
O pooling pega um conjunto de valores e os reduz a um mesmo valor.
A selação do valor de substituição pode ser a media dos valores substituidos, isso é o **Pooling Médio** ou simplismente selecionado o valor máximo entre eles, **Pooling Máximo**.
Em processamento de imagens o pooling pode substituir valores de sua vizinhanca, normalmente sendo uma janela quadrada de 9px, como em [[processamento-de-imagens#Vizinhanca-8 | vizinhanca de 8]] em caso de agrupamento 3x3.
O pooling global, é quando um mapa de caracteristicas inteiro é reduzido a um valor, o GAP _(Global Avarage Pooling)_ pode ser usado como uma forma de poda dinámica.

### Hiperparametro
Parametro pre-definido antres do treinamento da rede ou do ajuste fino (fine-tuning)
### Kernel
Pequena matriz de numeros que percorre uma imagem ou outra matriz de dedaos para extrair caracteristicas.

## Convulação
A convulação e a extração de valores continuos dos inputs. 
`Entrada ⊛ Kernel + Bias = Saída`
onde ⊛ é a convulação. Ou seja, a convulação e a transformação da multiplucação da entrada com o kernel somado com um viés.
Por exemplo:
```
Entrada:          Kernel:

1  2  3           1  0  1
4  5  6     ×     0  1  0
7  8  9           1  0  1
``` 
multiplicando posicao por posição teremos:
```
(1×1) + (2×0) + (3×1)
+ (4×0) + (5×1) + (6×0)
+ (7×1) + (8×0) + (9×1)
``` 
Resultado:
$1 + 0 + 3 + 0 + 5 + 0 + 7 + 0 + 9 = 25$

### Capsulas
Estruturas de capsulas, são uma alternativa ao pooling, que ao inves de substituir o mapa de caracteristicas, o substitui por um produto escalar, ou seja, um vetor armazenando caracteristicas principais, como formato, tramanho e posição de objetos.

## Resultados de Poda em Redes


### Normalizacao em Lote (BN)
"Usando parâmetros BN, as distâncias dos canais do mapa de características podem ser calculadas por camada. Usando uma [abordagem de agrupamento](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/clustering-approach) para distância, as características próximas podem ser ajustadas. Uma vantagem do agrupamento é que a redundância não é medida com uma distância absoluta, mas com um [valor relativo](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/relative-value) . Com cerca de 60 épocas de treinamento, eles conseguiram podar a rede, resultando em uma redução de 50% em FLOPs (incluindo operações não convolucionais) com uma redução na precisão de apenas 1% tanto para o top-1 quanto para o top-5 no conjunto de dados ImageNet"

### Metodo de reutilização
"O método de redução e reutilização (também descrito como outbound) elimina filtros inteiros calculando a variância estatística da saída de cada filtro usando um [conjunto de calibração](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/calibration-set) . Filtros com baixa variância são eliminados. O método outbound obteve 2.37×aceleração com perda de precisão de 1,52% no conjunto de dados Labeled Faces in the Wild (LFW) no campo do [reconhecimento facial](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/biochemistry-genetics-and-molecular-biology/facial-recognition) .

Um método que remove iterativamente neurônios redundantes para FCLs sem exigir dados de validação especiais. Essa abordagem mede a similaridade de grupos de pesos após uma normalização. Ela remove pesos redundantes e mescla os pesos em um único valor. Isso levou a uma redução de 34,89% nos pesos FCL na AlexNet com uma perda de precisão top-1 de 2,24% no ILSVRC-2012."

### Poda por Busca Gulosa
"A ThiNet adota informações estatísticas da camada seguinte para determinar a importância dos filtros. Ela usa uma busca gulosa para podar o canal que tem o menor custo de reconstrução na camada seguinte. A ThiNet poda camada por camada, em vez de globalmente, para minimizar grandes erros na [precisão da classificação](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/engineering/classification-accuracy) . Ela também poda menos durante cada época de treinamento para permitir a [estabilidade dos coeficientes](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/engineering/stability-coefficient) . A taxa de poda é um hiperparâmetro predefinido e a complexidade de tempo de execução está diretamente relacionada a essa taxa. A ThiNet comprimiu o número de operações de ponto flutuante (FLOPs) da ResNet-50 para 44,17%, com uma redução de 1,87% na precisão top-1."

## Poda combinada com Tuning e Retraining
"_Treinamento do zero:_ Observações mostram que a eficiência e a precisão do treinamento da rede são inversamente proporcionais à esparsidade da estrutura. Quanto mais densa a rede, menor o tempo de treinamento. Esta é uma das razões pelas quais as técnicas de poda atuais tendem a seguir um pipeline de treinamento-poda-ajuste em vez de treinar uma estrutura podada do zero."

## Poda Dinamica
Podas estaticas destroem de forma irreverssivel a estrutura original da rede. Uma vez podada e retreinada, e impossivel de recuperar informacoes apagadas. A poda dinamica, controla em tempo de execucao quais camadas e conexoes serao ativadas o que pode diminuir a computacao, dissipacao energetica e a largura da banda.
### Composicao da rede
Para isso, deve-se existir um sistema que controla em tempo de execucao o que podar durante o treinamento. Este componente de decisao e composto por:
- **Conexoes adicionais** criadas na fase de inferencia ou treinamento;
- **Caracteristicas das conexoes** que podem ser aprendidos por algoritmos de retropropagacao;
- **Rede de decisao lateral** de dificil treinamento mas otimo desempenho.
### Tipos/Niveis de poda
O nivel de poda escolhido influencia no projeto de hardware, sendo ele por:
- Por canal;
- Camada;
- bloco;
- Rede.

A desvantagem da poda dinamica e que exige uma camada extra de decisao rodando em tempo real durante o treinamento, exigindo maior computacao, largura de banda e eneergia.
a
## Shrinkbench
O Shrinkbench e um sistema de benchmark unificado para fazer comparacoes de desempenhos de poda disponivel no [github](https://github.com/jjgo/shrinkbench).

### INT8 training
[[pg-referencias#Jacob |Jacob]] Utilizou INT8 tanto para treinamento quanto para inferencia e obteve perca de precisa de 1,5% no ResNet-50.

# Glossary
## DataSets
**MNIST -** Dataset com mais de 60k imagens de numeros de 0 a 9 manuscritos. treinamento basico, apenas para validar o funcionamento da rede.
**CIFAR-10** - Dataset de imagens 32x32 coloridas com 10 classes.
**SVHN -** Dataset com fotos reais de numeros de casas capturadas no Google StreetView.
**ImageNet / ILSVRC-2012 -** mais de 1 milhao de imagens de alta resolucao com mais de 1000 classes diferentes.

## Arquiteturas de Rede
### LeNet-5
Uma das primeiras CNN feita para conhecer digitos manuscritos, a propria MNIST. Pequena e simples.
### AlexNet / GoogleNet
Sao CNNs bem maiores e mais modernas.Desenhadas com foco na ImageNet. Tem muito mais camadas e muito mais parametros.

## Acuracia
**TOP-1** : quando a rede define a resposta correta como maior probabilidade de veracidade entre as outras opcoes.
**TOP-5** : Quando a resposta correta esta entre as 5 opcoes de probabilidade de resposta.

## Processo de treinamento de uma rede
### Feed Foward Propagation
processo de alimentacao de pesos de forma consecutiva a partir de uma entrada ate a saída, sempre alimentando a rede para frente.

Considerando o caso de treinamento em uma MNIST. Caso a precisao da rede seja 85% de chance de ser o numero 7, mas o resultado correto é 3, houve um grande erro. Quando isso acontece, é calculado o gradiente da função de erro para identificar qual camada influenciou mais para a previsão do atual resultado. em seguida seus pesos são reajustados.
### Back Propagation
Este processo de voltar em camada na rede a partir da camada de output no sentido do gradiente de erro, é chamada de back propagation. 

``` 
Input --- FowardP. --- Output/Error ---- BackP. ---- ajusta peso
``` 

## Algebra da Quantizacao
## Quantizacao Simetrica e Assimetrica
### Sem Deslocamento / Simetrica
Na quantização simetrica, a ideia é simples. Trabalhamos com pesos de valores em um intervalo simetrico que varia em uma escala $s$.
Exemplo: com um $s = 1$ teremos uma variancia nos pesos de vai de $-1$ a $1$. Considerando $x$ como o valor do peso temos:
$$x\in [-1; 1]$$
com o "meio" em $z$, que e 0.
Porem pode ser trabalhado com qualquer escala de $s$ nos graus dos pesos.

### Com Deslocamento / Assimetrica
Neste caso, trabalhamos com uma escala $s$ que nao possui "meio" em 0. Por exemplo.
$$x \in [-0.2; 1]$$
Entao e definido para a quantizacao, que sera tratado com outros valores, o zero real. Exemplo:
``` INT8
         43
         ↓
0 ------ 43 ---------------- 255
         ↑
       x = 0
``` 
$z = 43$
$s=255$

Assim, a forma de extração do zero point e do valor de peso quantizadao é dada por:
$$\hat{x} = round(\frac{x}{s})$$
$\hat{x}$ = peso quantizado
$s$ = escala
$x$ = peso sem quantizar

Quando se tratando de deslocamento temos:
$$\hat{x} = round(\frac{x}{s}+z)$$
$z$ = ponto zero.

## Ativção

## Resultados em Quantizacão
Explorando redes de pesos binários [[pg-referencias#Rastegari |Rastegari]].
Aplicaram a binarizacao de pesos em ResNet-18 e GoogleNet resultando 9.5% e 5.8% de perca em comparacao com pesos FP32. Eles tambem extenderam a binarização para a funcao de ativação, a chamada XNOR-Net  e avaliaram ela em larga escala no dataset ILSVRC-1012. A XNOR-Net alcancou 44.2% de acuracia em classificacao top-1 no ILSVRC-2012 com Alex-Net, e teve uma aceleracao no tempo de execução de 58x.



### Kernels Eficientes
```
Imagem
  │
  ▼
┌────────────────────┐
│ Conv Layer         │
│ INT8 × INT8        │
└────────────────────┘
  │
  │ resultado convertido
  ▼
FP32
  │
  ▼
┌────────────────────┐
│ Conv Layer         │
│ INT8 × INT8        │
└────────────────────┘
  │
  ▼
FP32
  │
  ▼
...
``` 

### Quantizacao Reduz Overfitting
segundo [[pg-referencias#Liang|Liang]], além de acelerar as redes neurais, a quantização também demonstrou, em alguns casos, resultar em maior precisão. Como exemplos: 1) VGG-16 com pesos de 3 bits supera sua contraparte de precisão total em 1,1% no top-1 [144](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0720) , 2) AlexNet reduz o erro top-1 de referência em 1,0% com pesos de 2 bits e ativações de 8 bits [66](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0330) , 3) ​​ResNet-34 com pesos e ativações de 4 bits obteve 74,52% de acurácia top-1, enquanto a versão de 32 bits obteve 73,59% [174](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0870) , 4) Zhou mostrou que um modelo quantizado reduziu o erro de classificação em 0,15%, 2,28%, 0,13%, 0,71% e 1,59% em AlexNet, VGG-16, GoogLeNet, ResNet-18 e ResNet-50, respectivamente [269](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1345) , e 5) Xu mostrou que redes quantizadas com redução de bits ajudam a reduzir o overfitting em Redes Totalmente Conectadas (FCNs).

## Ativação
A ativação é dada por uma funcao de ativação do resultade de uma combinação lienar
![[Drawing 2026-09-11 10.54.52.excalidraw]]
Considerand estas camadas onde a primeira possui 3 neuronios $a$ e a segunda apenas dois neuronios, vamos analisar a ativação do primeiro neuronio (1) da segunda camada, que sera dividaida em 3 passos, sendo o primeiro definido por definido por:
1 -$$z = a_1w_{11}+a_2w_{21}+a_3w_{31} + b$$
onde:
- $x$ → entrada da camada;
- $b$ → viés;
- $z$ → resultado da combinação linear;
- $f$ → função de ativação;
- $a$ → **ativação**, ou saída da camada.

  2 - $$f(z)$$ Onde $f$ é a funcao de ativação. Assim:
  3 - $$a=f(z)$$
  ### Funções de ativação
  As funções de ativação são transformações aplicadas ao valor recevido da camada anterior para garantie a não linearidade da rede. Principais: ReLU, Sigmoid, Tanh.
  
  #### ReLU
  A função de ativação ReLU *(Retificated Linear Unity)* aplica a $z$:
  $$ReLU\ =\ max(0,z) \Rightarrow a=ReLU(0,z)$$
  Portanto a função zera vcalores negativos e propaga valores positivos.

# Resumo
## Poda
com base nas tecnicas de poda analisada, o recomendado para uma pode eficaz e:
- Definir tacade de poda para variar por camadas
- ==A poda dinâmica pode resultar em maior precisão== e manter maior capacidade de rede [246](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1230) .
- Treinar um modelo podado do zero às vezes, mas nem sempre (ver [Seção 3.3](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#s0090) ), é mais eficiente do que ajustar a partir dos pesos não podados [160](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0800) .
- A poda baseada em penalidades normalmente reduz a perda de precisão em comparação com a poda baseada em magnitude [255](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1275) . No entanto, esforços recentes estão reduzindo a diferença [72](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0360).
## Quantização
Com relacao a poda foram discutidos resultados de redes binarizadas e de precisão reduzida. Também a eficiencia de frameworks de quantização populares. Apesar da quantização diminuir a precisão da rede, devido a perca de informção algumas redes quantizadas podem superar a rede original (ver: [Seção 4.4](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#s0160) ).
A quantização de 8 bits é amplamente aplicada na pratica com uma boa razao entre a precisão e a compressão, e é amaplamente aplicada  em processadoers atuais e em hardware personalizadao. A perca de precisão é minima quando o [[#QAT (Quantization-Aware Training) |treinamento com reconhecimento de quantização]] esta ativado. Redes binarizadas alcancaram resultados satisfatorios com hardware especializado.

Para obter melhores resultados em quantização é recomendado:
- ==Use quantização assimétrica==. Ela preserva a flexibilidade ao longo do intervalo de quantização, embora tenha sobrecarga computacional [120](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0600) .
- ==Quantize os pesos em vez das ativações==. A ativação é mais sensível à precisão numérica [75](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0375) .
- ==Não quantize os vieses==. Eles não requerem armazenamento significativo. Vieses de alta precisão em todas as camadas [114](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0570) e nas primeiras/últimas camadas [200](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1000) , [272](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1360) mantêm uma precisão de rede mais alta.
- Quantizar kernels por canal em vez de por camada para melhorar significativamente a precisão [131](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0655) .
- Ajustar o modelo quantizado. Isso reduz a lacuna de precisão entre o modelo quantizado e o modelo de valor real [244](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1220) .
- Inicialmente, treine usando um modelo de ponto flutuante de 32 bits. Modelos quantizados de baixa quantidade de bits podem ser difíceis de treinar do zero - especialmente modelos compactos em conjuntos de dados de grande escala [272](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1360) .
- A sensibilidade da quantização é ordenada como gradientes, ativações e, em seguida, pesos [272](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1360) .
- A quantização estocástica de gradientes é necessária ao treinar modelos quantizados [89](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b0445) , [272](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/science/article/pii/S0925231221010894?via%3Dihub#b1360) .


a pesquesa atual sobre compressao esta focada principalmeente em cnns. mais especificamentte a pesquisa e direcionamen principalemnte para taredfas de clasificaçlão em cnns. trabaçlhos futuros deve considerar outros ripos de aplicações como detecç~ao de  objetos, reconhecimento de fala , traducao de idicomas, etc. a relacao entre compressao de rede e proecisao para diferentes aplicações e uma area de pesquisa interessante,
adaptação de hardweaer, as implementações de hardware podem limitar a eficacia dos algoritmos de poda. po ecemplo a poda eleemnto a elemnto praticamente nao refduz os calculos ou largurea de bancda ao usar o imwcolgell,, em processadores de uso geral, da mesm forma a poda por forma normalmente nao pode ser implementada em aceleradores de cnn dedicados. o projeto conjunnto de hardware e fogrware de tecnicas de compressao para aceleradodees de hardware deve ser considerado para alcancar a melhor ewfgiciencia do sistema.
metodos blobais, As otimizações de rede são normalemtne aplicadas separadamento sem que a informação de uma otimizazao influencia qualquer outra,. Redentem,ente foram propostas abordagensque considram a eficação da ortimização em multiplas camadas, fiscute a poda combinada com a fatoração de tensores que resulta em ma melghor compressao geral. Tecnmicas semelhantes podem ser consideradas usadno diferentes tipos e niveis de compressao e fatoração.

# Conclusões
