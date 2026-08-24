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
### Poda de Rede
A poda de rede envolve a remoção de parâmetros que não impactam a precisão da rede
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
`1 + 0 + 3 + 0 + 5 + 0 + 7 + 0 + 9 = 25`

