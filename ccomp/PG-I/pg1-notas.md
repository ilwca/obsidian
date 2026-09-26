 
# Poda e quantização para aceleração de redes neurais profundas: uma revisão
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
A selação do valor de substituição pode ser a media dos valores substituidos, isso é o **Pooling Médio** ou simplismente selecionado o valor máximo entre eles, **Pooling Máximo** ou o menor, **Pooling minimo**. Ou seja, o pooling é um processo de agrupamento de informação.
Em processamento de imagens o pooling pode substituir valores de sua vizinhanca, normalmente sendo uma janela quadrada de 9px, como em [[processamento-de-imagens#Vizinhanca-8 | vizinhanca de 8]] em caso de agrupamento 3x3.
O pooling global, é quando um mapa de caracteristicas inteiro é reduzido a um valor, o GAP _(Global Avarage Pooling)_ pode ser usado como uma forma de poda dinámica.



### Hiperparametro
Parametro pre-definido antes do treinamento da rede ou do ajuste fino (fine-tuning)
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

O resultado para este determinado pixel da nova matriz sera somado ao viés e depois entrará na função de ativação.
exemplo: $ReLU(25+b)$

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
A ativação é dada por uma funcao de ativação do resultado de uma combinação lienar. Vamos propor duas camadas FCL, assim como um grafo [[Grafos#Grafo Bipartido|bipartido]] completo $K_{3,2}$. 
![[cnn-ativacao]]
Considerando estas camadas onde a primeira possui 3 neuronios $a$ e a segunda apenas dois neuronios, vamos analisar a ativação do primeiro neuronio (1) da segunda camada, que sera dividaida em 3 passos, sendo o primeiro definido por definido por:
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

---

# Transfom QUantization for CNN Compression
[arxiv](https://arxiv.org/abs/2009.01174) 

**Primeiro**, propomos a **quantização por transformação** para a compressão de pesos de CNNs — somos os primeiros a considerar a quantização dos **pesos transformados e da base**, além de otimizar ambos após o treinamento.
**Segundo**, apresentamos uma teoria de **taxa e distorção para a quantização de CNNs**, com base na qual os **ganhos da codificação por transformação** podem ser calculados. Em seguida, derivamos uma transformação aprendida **de ponta a ponta (end-to-end)** que maximiza esses ganhos.
**Terceiro**, avançamos o estado da arte na compressão de CNNs, tanto em cenários **com retreinamento** quanto **sem retreinamento**, para tarefas de classificação de imagens — **AlexNet** [1], **ResNets** [60] e **DenseNets** [61] — e para tarefas de visão de baixo nível, **DRUNet** (remoção de ruído) [62] e **EDSR** (super-resolução) [63].

### Qantização por Transformação
Na transformação por quantização os pesos não são diretamente quantizados como na quantização convencional $PF32 \rightarrow INT8$; Antes é feito um processo de transformação destes pesos $FP32 \rightarrow Transform \rightarrow W' \rightarrow INT8$.
A transformação ela "salienta" algumas propriedades que ajudam a definir a importancia do peso, assim pesos menos importantes são mais proximos de 0.

É nesta hora que entra a [[#Poda|poda]]. Pesos mais proximos de zero, em caso de quantização com uma menor taxa de bits, acabam se tornando nulos.

No artigo é trabalhado com duas camadas convulacionais, a camada base (basis-layer) e a camada transformada (transform domain layer), pois a partir delas é possivel reconstruir a camaada original.
Portanto camadas transformadas pode ser representadas como:
$$\Theta'=ST$$
onde:
$T \rightarrow$ camada transformada (transform domain layer)
$S \rightarrow$ camada base (basis-layer)
$\Theta' \rightarrow$ camada de pesos quantizado

## Quantização Pos-Transformação
A aplicação de uma transformação a uma camada convulacional ou a unma camada totalmente conectada permite uma redução de dimensionalidade. 
"A quantização por transformação busca primeiro obter uma representação dos pesos com menor correlação e, então, quantizar essa representação de forma otimizada, permitindo explorar simultaneamente redução de dimensionalidade e redução da precisão numérica."

E destacado no artigo que o foco da compressão da rede são os pesos dos neuronios, pois os vieses tem pouca importancia e as ativações não são o foco da compressão.

## Quantização de CNNs
A representação de uma rede pode ser feita de forma matemática,  principalmente para a representação de pesos de uma camada. No artigo as camadas são representadas por $\Theta_l$ onde:
- $\Theta \rightarrow$ parametros da rede
- $L \rightarrow$ Numeors de camada da rede
- $x \rightarrow$ entrada
- $y \rightarrow$ saída

assim
$$\boxed{Entrada\ x \rightarrow \Theta_1 \rightarrow \Theta_2 \rightarrow \ldots \rightarrow \Theta_L \rightarrow\ Saida\ y}$$
E como ja mencionado anteriormente, o foco da quantização é $\Theta$ pois viéses e ativações nao tem impacto significativo na compressão.

**Mas qual a estrutura de $\Theta$?**
O formato de $\Theta$ depende do tipo da camada, podendo ser uma cada de convulacional, uma FLC.
No caso de uma camada convulacional, $\Theta$ é um tensor de pesos. Seguindo notação do artigo: $$\Theta \in \mathbb{R}^{a\times b}_{n\times m}$$ sendo:
-  $a\times b \rightarrow$ tamanho espacial do kernel
- $n \rightarrow$ numero de canais de entrada
- $m \rightarrow$ numero de canais de saida

Considerando o caso de uma AlexNet com kernels $a\times b = 11\times11$ e uma entrada de uma imagem RGB, ou seja, uma entrada para cada cor R,G,B, assim $n=3$ e 64 saidas, $m=64$. 
```
                 3 canais de entrada
                       ↓
              ┌─────────────────┐
              │ Kernel 1        │ → canal de saída 1
              │ 11 × 11         │
              ├─────────────────┤
              │ Kernel 2        │ → canal de saída 2
              │ 11 × 11         │
              ├─────────────────┤
              │       ...       │
              └─────────────────┘
                       ↓
                 64 saídas
```

Isto para uma unica camada inicial com $n=3$. Assim teremos:
$$\Theta_1\in \mathbb{R}^{11\times11\times64\times3}$$
por tanto a quantidade total de pesos para esta camda é:
$$64×3×11×11=23232$$

Em uma FLC assim, é mais parecido com uma matriz convencional, pois teremos a multiplicação de $n\times m$ formando uma matriz bidimensional.
$$\Theta_L\in \mathbb{R}^{1\times1}_{1000\times4096}$$
pesos:$$1000×4096=4096000$$

### Quantização por camada (Layer-Wise Quantization)
Este é um metodo que busca encontrar como ddistribuir os bits entre as diferentes camadas. Ou seja, a quantização sera aplicada em cada camada de forma independente e dinamica com a determinada precisão. Exemplo: $$R_l=2$$
Determina que na camada $L$ a precisao dos pesos sera de 2 bits. Desta forma, $R_l$ pode ser derminado de maneira dinamica para cada camada $\Theta_l$, assim como tambem pode ser feita a poda integral da camdad com $R_l=0$.
## Alocação Não Uniforme de Bits
Esta distribuição pode ser feita para as camadas como neste exemplo. Suponha as camadas:
$$\Theta_1, \Theta_2, \Theta_3$$
Pode ser definido:
$$R_1=8, R_2=4,R_3=2$$
Mas pode acontecer, que determinadas camadas sejam mais senciveis a quantização que outras.
### Distorição
A distorção da rede é calculada pela função $$D(R_1,\ldots,R_L)=\mathbb{E}||\hat{y}-y||_2^2$$
onde $y$ é a saida da rede original e $\hat{y}$ da rede quantizada. portanto $\mathbb{E}||\hat{y}-y||_2^2$ mede quanto a saida foi afetada pela quantização.

## Transform Quantization
Na transform quantization, temos o seguinte processo
$$\Theta \rightarrow T \rightarrow quantization$$
Assim os pesos sao transformados antes de serem quantizadas. Este processo de transformação salienta caracteristicas dos pesos de mais importancia e reduz o valor de pesos pouco significantes para evitar a redundancia de informações de alguns pesos. por exemplo:$$\Theta=[0.80,0.82,0.79,0.81,0.83]$$
$$T=[4.05,0.03,−0.01,0.02,0.00]$$
Percebemos que o valor agora esta concentrado no primeiro peso, assim os posteriores podem receber poucos bits ou ate 0.
```
Coeficientes transformados
 │
 ├── informação principal █████████
 ├── informação pequena   ██
 ├── informação pequena   ▏
 ├── quase nada           ▏
 └── quase nada           ▏
```

No artigo, é feito um calculo para a medição de eficiencia da trasnformação e comparação com a quantização direta. Então é calculado um $G$ que define a taxa de distorção da rede denotado por:
$$G = \frac{D_{pcm}}{R_{tc}}$$
que de grosso modo significa:
$$G = \frac{distorção\ sem\ transformacao}{distorcao\ com\ transformacao}$$
- caso $G\approx 1$ a transformação nao teve impacto significativo.
- Caso $G>1$ a transformação teve impacto significativo. Quando maior o $G$, melhor a transformação.

## Fine-Tunning
Embora o fine-tunning nao devolva precisao de redes comprimidas devido a perca de dados no momento da compressao, o artigo mostra que a realizacao do fine-tunning em redes  quantizadas por quantização devolve a precisao proxima as das redes originais.

### Redes comparadas
- ResNet-18
- ResNet-34
- ResNet-50
- AlexNet
- DenseNet-121

==O problema enfrentado é que redes quantizadas diminuem a acurácio e no momento do re-treinamento a rede tem que calcular o gradiente de erro no backpropagation. porem com pesos quantizados isso fica mais dificil.== Para isso, são utilizados métodos no artigo, como o _Striaght-Through Estimator (STE)_ para que o treinamento consiga continuar mesmo com a quantização.
### Um resultado importante
O artigo observa que, com retreinamento:
- **2 bits:** a acurácia pode voltar para valores próximos aos da rede original;
- **3 bits:** a perda de acurácia é praticamente eliminada.
Isso mostra que a quantização, por si só, não determina necessariamente a perda final de desempenho. O **retreinamento pode recuperar parte do desempenho perdido**.

O artigo levanta um ponto ja abordado no artigo passado. 
"Portanto, podemos ser capazes de obter uma aceleração adicional caso seja possível desenvolver **hardware especializado** para facilitar operações aritméticas com baixa profundidade de bits." 
Ou seja, o uso de hardware especializado para operações de baixa precisão ajuda a aceleração da rede.

## Comparacao visual
pela figura 11. do artigo que faz uma comparação visual entre as redes DRUNet que tem objetivo de remoção de ruido e reconstruição, envolvendo imagens e a capacidade da rede dereconstrui-las por meio de diferentes **taxas** de bits, como 32, 2, 1 e 0.5.
Lembrando que a taxa de bits é dada pela relação quantos bits os pesos estão sendo representados e a quantidade de pesos. Exemplo:
$$\frac{4\ bits}{8\ pesos}=0.5\ bit\ peso$$
Na figura, são analisados dois parametros, o **PSNR** (Peak Signal-to-Noise Ratio)  e o **SSIM** (Structural Similarity Index Measure).
### PSNR
O PSNR mede quanto a imagem distorcida, se parece com a imagem reconstruida numericamente, então, quanto menor o erro, maior o PSNR. este parametro e medido em dB, pois a unidade de medida decibel, é uma escala logaritmica para representar razões.
### SSIM
O SSIM tenta avaliar se a estrutura da imagem original foi preservada, como fatores como liminescencia, contraste e estrutura. Ou seja, a diferenca visual da imagem reconstruída para a imagem original.

## Discussão
Na discussão o artigo apresenta direções que podem ser estudadas, como:
- Extensão para Transformação 2D.
- Exetensão para Transformação Intre-Kernel

## Limitações e Trabalhos Futuros
problema de ordenação de linhas e colunas, onde deve-se propor um $U$ ideal para cada camada, pois o resultado otmio para a camada $\Theta_1$ nao necessariamente otimo para a camada $\Theta_2$, onde $U^t_1\Theta_1$ produza uma matriz boa e esparsa. o mesmo nao e valho para $U^t_1\Theta_2$.
É ai que os autores propoem uma especie de QAT.

|Estratégia|Treinamento depois/durante|
|---|---|
|PTQ|Não necessariamente|
|QAT|Sim, durante treinamento|
|PTQ + fine-tuning|Sim, depois da quantização|
Ou seja,  PQT sem fine-tunning pode gerar significativa perca de acuracia.

## Conclusão
O citado trabalho propoe a compressão de redes neurais CNN usando de metodos de quantização por transformação no cenário pos-treinamento.
Com o principal criterio de analise sendo a [[#Distorição|taxa de distorção]], foram aperfeicoadas as tecnicas de compressão e quantização, com relação a profunidade de bits atribuidas aos pesos.
A estrutura estudada avanca o estado da arte em compressão de CNNs em diversos modelos de CNN.
Então o principal ponto deste artigo que os autores demonstraram é que:

**transformar os pesos antes da quantização melhora a compressão**.

E o ponto importante é que eles não escolhem simplesmente um número de bits igual para tudo.A quantidade de bits é determinada considerando o impacto na saída da rede.

Portanto um resumo geral deste artigo seria:

**Como a transformação antes da quantização de pesos de uma rede pode melhorar o processo de compressão baseado em uma alocação nao uniforme de pesos considerando a taxa de distorção da rede.**

---

# Energy-Efficient CNNs on FPGA via Convolutional Weight Quantization
[IEEE](https://doi.org/10.1109/EngiTek68245.2025.11567639)
