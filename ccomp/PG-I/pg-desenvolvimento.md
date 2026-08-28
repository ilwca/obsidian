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
