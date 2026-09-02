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

## Resultados de Poda em Redes TOP-1


### Normalizacao em Lote (BN)
"Usando parâmetros BN, as distâncias dos canais do mapa de características podem ser calculadas por camada. Usando uma [abordagem de agrupamento](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/clustering-approach) para distância, as características próximas podem ser ajustadas. Uma vantagem do agrupamento é que a redundância não é medida com uma distância absoluta, mas com um [valor relativo](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/relative-value) . Com cerca de 60 épocas de treinamento, eles conseguiram podar a rede, resultando em uma redução de 50% em FLOPs (incluindo operações não convolucionais) com uma redução na precisão de apenas 1% tanto para o top-1 quanto para o top-5 no conjunto de dados ImageNet"

### Metodo de reutilização
"O método de redução e reutilização (também descrito como outbound) elimina filtros inteiros calculando a variância estatística da saída de cada filtro usando um [conjunto de calibração](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/computer-science/calibration-set) . Filtros com baixa variância são eliminados. O método outbound obteve2.37×aceleração com perda de precisão de 1,52% no conjunto de dados Labeled Faces in the Wild (LFW) no campo do [reconhecimento facial](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/biochemistry-genetics-and-molecular-biology/facial-recognition) .

Um método que remove iterativamente neurônios redundantes para FCLs sem exigir dados de validação especiais. Essa abordagem mede a similaridade de grupos de pesos após uma normalização. Ela remove pesos redundantes e mescla os pesos em um único valor. Isso levou a uma redução de 34,89% nos pesos FCL na AlexNet com uma perda de precisão top-1 de 2,24% no ILSVRC-2012."

### Poda por Busca Gulosa
"A ThiNet adota informações estatísticas da camada seguinte para determinar a importância dos filtros. Ela usa uma busca gulosa para podar o canal que tem o menor custo de reconstrução na camada seguinte. A ThiNet poda camada por camada, em vez de globalmente, para minimizar grandes erros na [precisão da classificação](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/engineering/classification-accuracy) . Ela também poda menos durante cada época de treinamento para permitir a [estabilidade dos coeficientes](https://www-sciencedirect-com.ez6.periodicos.capes.gov.br/topics/engineering/stability-coefficient) . A taxa de poda é um hiperparâmetro predefinido e a complexidade de tempo de execução está diretamente relacionada a essa taxa. A ThiNet comprimiu o número de operações de ponto flutuante (FLOPs) da ResNet-50 para 44,17%, com uma redução de 1,87% na precisão top-1."

## Poda combinada com Tuning e Retraining
"_Treinamento do zero:_ Observações mostram que a eficiência e a precisão do treinamento da rede são inversamente proporcionais à esparsidade da estrutura. Quanto mais densa a rede, menor o tempo de treinamento. Esta é uma das razões pelas quais as técnicas de poda atuais tendem a seguir um pipeline de treinamento-poda-ajuste em vez de treinar uma estrutura podada do zero."

## Poda Dinamica
Podas estaticas destroem de forma irreverssivel a estrutura original da rede. Uma vez podada e retreinada, e impossivel de recuperar informacoes apagadas. A poda dinamica, controla em tempo de execucao quais camadas e conexoes serao ativadas o que pode diminuir a computacao, dissipacao energetica e a largura da banda.
### Composicao da rede
Para Isso deve-se existir um sistema que controla em tempo de execucao o que podar durante o treinamento. Este componente de decisao e composto por:
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

## Shrinkbench
O Shrinkbench e um sistema de benchmark unificado para fazer comparacoes de desempenhos de poda disponivel no [github](https://github.com/jjgo/shrinkbench).
