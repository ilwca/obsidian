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
### Quantizacao de Rede
A quantização de rede envolve a substituição de tipos de dados por tipos de dados de largura reduzida. Por exemplo, substituir o ponto flutuante de 32 bits (FP32) por inteiros de 8 bits (INT8). Os valores podem frequentemente ser codificados para preservar mais informações do que uma simples conversão.
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

### Pooling
O pooling pega um conjunto de valores e os reduz a um mesmo valor.
A selação do valor de substituição pode ser a media dos valores substituidos, isso é o **Pooling Médio** ou simplismente selecionado o valor máximo entre eles, **Pooling Máximo**.
Em processamento de imagens o pooling pode substituir valores de sua vizinhanca, normalmente sendo uma janela quadrada de 9px, como em [[processamento-de-imagens#Vizinhanca-8 | vizinhanca de 8]] em caso de agrupamento 3x3.
O pooling global, é quando um mapa de caracteristicas inteiro é reduzido a um valor, o GAP _(Global Avarage Pooling)_ pode ser usado como uma forma de poda dinámica.

### Capsulas
Estruturas de capsulas, são uma alternativa ao pooling, que ao inves de substituir o mapa de caracteristicas, o substitui por um produto escalar, ou seja, um vetor armazenando caracteristicas principais, como formato, tramanho e posição de objetos.