 Alguns principios a serem abordados
- Paretto Frontier $\Rightarrow$ Para analise dos resultados.

```roadmap
TCC
│
├── 1. INTRODUÇÃO
│
├── 2. FUNDAMENTAÇÃO TEÓRICA
│   ├── 2.1 Redes neurais artificiais
│   ├── 2.2 CNN
│   ├── 2.3 CIFAR-10
│   ├── 2.4 LeNet
│   ├── 2.5 Quantização
│   ├── 2.6 Quantização pós-treinamento
│   ├── 2.7 Poda de redes neurais
│   ├── 2.8 Poda estruturada
│   ├── 2.9 Computação aproximada
│   ├── 2.10 Somadores aproximados
│   ├── 2.11 Multiplicadores aproximados
│   ├── 2.12 MAC
│   └── 2.13 Arrays sistólicos
│
├── 3. TRABALHOS RELACIONADOS
│
├── 4. METODOLOGIA
│   ├── 4.1 Modelos
│   ├── 4.2 Datasets
│   ├── 4.3 Treinamento
│   ├── 4.4 Quantização
│   ├── 4.5 Poda
│   ├── 4.6 Poda + retreinamento
│   ├── 4.7 Poda + quantização
│   └── 4.8 Métricas
│
├── 5. RESULTADOS
│
├── 6. DISCUSSÃO
│
└── 7. CONCLUSÃO
``` 
## Referencial Teorico
``` 
2.1 Redes Neurais Artificiais
    2.1.1 Neurônio artificial
    2.1.2 Pesos, bias e funções de ativação
    2.1.3 Camadas e arquitetura de uma rede neural
    2.1.4 Treinamento, backpropagation e inferência

2.2 Redes Neurais Convolucionais
    2.2.1 Convolução
    2.2.2 Kernels e filtros
    2.2.3 Mapas de características
    2.2.4 Funções de ativação
    2.2.5 Pooling
    2.2.6 Camadas totalmente conectadas
    2.2.7 Custo computacional das CNNs

2.3 LeNet-5 e classificação de imagens
    2.3.1 Arquitetura da LeNet
    2.3.2 Fluxo de dados na LeNet
    2.3.3 LeNet aplicada ao MNIST
    2.3.4 LeNet aplicada ao CIFAR-10

2.4 Computação e inferência em redes neurais
    2.4.1 Operações MAC
    2.4.2 Parâmetros e memória
    2.4.3 Precisão numérica
    2.4.4 Custo de inferência
    2.4.5 Relação entre precisão, memória e desempenho

2.5 Técnicas de compressão e aceleração de redes neurais
    2.5.1 Redundância em redes neurais
    2.5.2 Compressão de modelos
    2.5.3 Poda
    2.5.4 Quantização
    2.5.5 Combinação de técnicas

2.6 Quantização de redes neurais
    2.6.1 Conceito de quantização
    2.6.2 Quantização de pesos e ativações
    2.6.3 Precisão e representação numérica ****
    2.6.4 Quantização uniforme e Layer-Wise
    2.6.5 Escala e zero-point
    2.6.6 Quantização simétrica e assimétrica
    2.6.7 Granularidade da quantização
        - por tensor/camada
        - por canal
    2.6.8 Largura de bits
        - FP32
        - FP16
        - INT8
        - INT4
        - INT2
    2.6.9 PTQ
    2.6.10 QAT
    2.6.11 Impacto da quantização na acurácia
    2.6.12 Quantização de baixa precisão

2.7 Poda de redes neurais
    2.7.1 Conceito de poda
    2.7.2 Poda não estruturada
    2.7.3 Poda estruturada
    2.7.4 Poda por magnitude
    2.7.5 Poda de canais/filtros
    2.7.6 Retreinamento após poda
    2.7.7 Impacto da poda

2.8 Quantização e poda combinadas
    2.8.1 Motivação
    2.8.2 Efeitos combinados
    2.8.3 Trade-off entre compressão e acurácia

2.9 Métricas para avaliação de modelos comprimidos
    2.9.1 Acurácia
    2.9.2 Tamanho do modelo
    2.9.3 Número de parâmetros
    2.9.4 Latência de inferência
    2.9.5 Relação entre as métricas

2.10 Relação entre otimização de modelos e hardware
    2.10.1 Multiplicação e acumulação
    2.10.2 Operadores de baixa precisão
    2.10.3 Impacto da quantização sobre hardware
    2.10.4 Operadores aproximados
    2.10.5 Relação com somadores e multiplicadores aproximados 
```

- [x] Redes Neurais 
- [x] CNN
- [x] base de Dados - CIFAR 10
- [x] LeNet
- [x] Qauntizacao 
- [x] Poda
## Consumo energetico
Estabelecer uma base, modelo original contendo informacoes, como:

| Métrica              | Modelo original |
| -------------------- | --------------: |
| Acurácia             |           98.x% |
| Tamanho              |            X MB |
| Número de parâmetros |               X |
| MACs                 |               X |
| Latência             |            X ms |
| Energia*             |        opcional |

Para a metrica de energia, podemos acompanhar o treinamento e inferencia por meio de software:
- **NVIDIA Management Library (`nvidia-smi` / `pynvml`):** Reporta o consumo em Watts da placa em tempo real diretamente do driver da GPU.
- **CodeCarbon:** Pacote em Python que monitora o consumo do hardware (GPU/CPU) durante a execução e estima a pegada de carbono do modelo.

# Referencial Teorico
- [ ] CNN
- [ ] base de Dados - CIFAR 10
- [ ] LeNet
- [ ] Qauntizacao 
- [ ] Poda

com base em [[pg-referencias#Young | Transform Quantization for CNN Compression]]
## CNN
Ao falar de CNNs, alem de axplica;'ao tecnica do que é, como funciona, destacar suas limitações, como:
- Calculos
- Parametros
- Implementações

Para o treinamento e inferencia destas sao realizadaos milhares de **calculos** por minuto, onde os pesos ja nao cabem mais na memoria de rapido acesso (cache), necessidade de memoria externa aumentando o consumo energetico

As centenas de milhoes de parametros, sendo ativados simultaneamente e seu volume de armazenamento impossibilita a implementação em dispositivos moveis.

# Metodologia
- planejamento

Dentro do escopo da metodologia iremos abordar:
## Tecnologias
- Ferramentas = pytorch, Scikitlearn
- Técnicasw
- Bibliotecas
## Decisões do Projeto
- Arquiteturas
- Trade-Offs de implementação
## Obter Resultados
- Relação de causa e efeito
- Limitação de uma Tecnologia
- Benchmarks comparativos

No desenvolvimento da metodologia, buscaremos responder:
- Qual tecnologia é mais eficaz?
- Pra quem?
- Realizando qual atividade especifica?
- Em qual tipo de sistema?
- Sob qual conjunto de circunstâncias?

O que estaremos analisando aqui? Quais variáveis?
- Accuracia
- Erro (principal)
- Largura de Bits

## Tipos de Pergunta
Com  isso, dessas variáveis teremos que analisar alguns âmbitos:
### Taxa base
- Como X normalmente se comporta
### Correlação
- Y e X estão relacionados
### Relação Causal
- X causa Y? Causa mais Y do que Z?
Ex:"A estratégia QAT reduz mais o erro do que PTQ".
### Projeto
- Qual a forma mais eficaz de alcançar X?
## Experimento Controlado
Método rigoroso de obter relação de causalidade entre variáveis. O pesquisador manipula deliberadamente variáveis independentes (que são os tratamentos aplicados ao método, como técnica de busca, otimização) e mede o efeito sobre as variáveis dependentes (variável de resposta, variável ao qual tenho interesse, como erro, largura de bit).

Ex: "Avaliar se a técnica de design space exploration input-aware (IHA) reduz mais recursos de hardware (LUT + FF) do que abordagem baseada em modelo DFG, para a mesma aplica;'ao e o mesmo limiar de erro."

## Teoria e Observação 
Ex: Tratamento; Resultado = Consumo de LUT + FF.
A teoria por trás (constructo causal $\Rightarrow$ Efeito) é "Aproximação reduz custo de hardware" - mas só observamos sua operacionalização: tratamento $\rightarrow$ resultado medido.

Desta forma, para a aplicação de operações de estudo deve-se justificar teoricamente seu efeito. 

## Terminologia
### Erro Experimental
Ao avaliarmos, por exemplo, a velocidade de execução de um programa, devemos considerar que este compete hardware com o sistema opercaional. Deste modo, é inerente que a cada nova execução teremos um resultado de tempo diferente, sendo este o erro experimental.
Para tratarmos isso, devemos considerar o erro por meio de uma grande quantidade de execuções deste programa, afim de termo uma amostra de execução para que obtenhamos uma média ponderada ou mediana do tempo de execução. A consideração do erro experimental, agrega credibilidade estatística ao dados apresentados.

### Unidade Experimental
Objeto sobre o qual experimento é executado, Ex: Projetos de software, processo de desenvolvimento, configuração de um circuito, etc.
### Sujeito Experimental
Pessoa que aplica os métodos, como equipes de desenvolvimento.

## Hipóteses Estatísticas
### Hipótese Nula ($H_0$)
Nenhuma diferença entre os dois tramamentos, ou seja, não existe relação causal entre as variáveis.
### Hipótese Alternativa ($H_1$)
Postula uma diferença significativa entre dois tramamentos. Alega-se que existe uma relação aos dois tramamentos diferentes.

Então o objetivo do experimento é **Negar** a $H_0$ através de testes estatísticos dos resultados dentro das respostas do experimento. Porém os resultados para a negação da hipótese nula devem atender a uma taxa de significância.  

## Variável de Resposta
As **Variáveis de Resposta (dependente)** é o resultado medido; Sempre quantitativo.
Ex: LUT+FF, Potencia, SSIM, tempo de execução.
### Trade-off
Dois fatores A e B interagem se o efeito de um depende do valor de outro. E preciso examinar o efeito de cada fator isoladamente **e** a interação entre eles sobre a variável de resposta.
=="Como estas variáveis interagem entre si, e qual o efeito destas atuando isoladamente na variável de resposta ?"==
Ex: O ganho de aceleração depende do equilíbrio entre a redução do tamanho e a perda de acurácia variando também conforme a arquitetura da rede.


## Delineamento experimental
- Quais variáveis serão examinadas?
- Quais dados serão coletados?
- Quantos experimentos elementares precisam ser executados?
- **Quantas vezes o experimento será organizado?** (Arranjo dos tratamentos x Unidades x Sujeitos)

## Ameaças à Validade
Todo experimento controlado exige abordar as ameaças a validade da pesquisa e dos resultados. O que pode invalidar meu experimento? O que pode ter sido feito de errado?
Esta é uma forma de criar ciência irrefutável, agregando não desconfiança, mas valor a sua pesquisa.
### Validade Interna
Fatores não controlados podem explicar o resultado observado. Ex: _Seed de otimização não fixada; diferença da versão de ferramentas entre as execuções e etc_.
### Validade Externa
Limitações na generalização dos resultados para outros contextos. Ex: _Resultados obtidos em sobel valem para CNNs? Para outras familias de FPGA?_.
### Validade Construto
As métricas realmente medem o que se pretende medir? Ex: _O SSIM realmente captura a "qualidade aceitavel" para a aplicação-alvo?_.
### Validade de Conclusões
As analises estatísticas foram aplicadas corretamente?