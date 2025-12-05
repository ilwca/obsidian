
Neste projetos estaremos treinando uma rede neural para a classificação de mensagens de e-mail como spam e não spam.
## Problema
por dia recebemos dezenas de mensagens indesejadas, seja ligacoes ou mensagens.
segundo o against data um cidadao americano recebe em media cerca de 1825 mensagens de spam por ano, que e equivalente a 5 mensagens de SPAM por dia.
## spam
spam são mensagens  classificadas como não desejadas, que são enviadas para uma grande quantidade de pessoas simultâneamente buscando promover algo.

## ham 
O oposto de spam's são as ham's que são mensagens de colegas de trabalhos, amigos entre outros.

## Solucao
com isto, treinamos um modelos de inteligencia artifical para classificar estas mensagens recebidas como desejadas ou nao desejadas(SPAM ou HAM). Para isso teriamos que usar uma grande amostra de dados para que o modelo baseie seu aprendizado

Para isto, usamos uma base de dados chamada "Spam Email Classification Dataset" disponível no [kaggle](https://www.kaggle.com/datasets/purusinghvi/email-spam-classification-dataset). Esta base de dados conta com mais de 75 mil mensagens.
Apesar de grande, o dataset contem apensa duas colunas, a de "text" que contem a mensagem a ser analisada e a do "label", que é um valor binário, indicando **0 para ham** e **1 para spam** da respectiva mensagem.


# Target
O target é uma variável alvo, ou seja, é ela que queremos prever. Neste caso nosso alvo é a variável "label", pois buscamos acertar se a mensagem que está em "text" é spam ou não.
Como estamos lidando com um modelo de classificação, é um dado discreto, enquanto para modelos de regressão o target é contínuo.
- Em **Regressão**: Prever dados contínuos como: 2.45, 5.12, 1.14. Em clima, preços, etc.
- Em **Classificação**: Prever resultados categoricos como dados binarios, em: "doente" e  "saudável", "gato" e "cachorro" ou "spam" e "não Spam".


# TF-IDF
Os modelos de aprendizado não entendem palavras, somente número, então, temos que atribuir um peso para cada palavra para que esta seja calculada.
O TF-IDF (Term Frequency - Inverse Document Frequency) mede quanto uma palavra é importante em uma mensagem e dentro do contexto de todo o dataset.

análisando o trecho de codigo:

```python
tfidf = TfidfVectorizer(
    max_features=5000,  # limita ao vocabulário de 5000 palavras mais relevantes
    max_df=0.8,         # ignora palavras que aparecem em mais de 80% dos textos
    min_df=2,           # ignora palavras que aparecem em menos de 2 textos
    stop_words='english',  # remove palavras comuns irrelevantes (the, is, etc.)
    ngram_range=(1, 2)  # considera unigramas (1 palavra) e bigramas (pares de palavras)
)```

Então ele cria um vocabulário de ate  5000 palavras, ou seja, cada texto vira um vetor de 5000 números onde cada um representa o peso TF-IDF de uma palavra.

```python
X_tfidf = tfidf.fit_transform(X)
```

Com os nossos palavras e bigramas convertidos em matrizes de pesos teremos:
```
⚙️ Configurando TF-IDF Vectorizer... 
🔄 Transformando textos em features TF-IDF... 
✅ Features TF-IDF criadas! 
📊 Dimensões da matriz: (75678, 5000) - 75678 mensagens - 5000 features (palavras/bigramas)
```

Gerado uma matriz de dimensão 75678x5000 com textos_do_datase X sequencia_de_pesos

A partir disso, obviamente teremos palavras como "win", "free", "credit" com muito mais peso que outras, tendo mais chances de serem spams.


# Divisão de Treino/Teste
A divisão dos dados normalizado e importante para o treinamento e validação do aprendizado. Para isso, dividimos o dataset do jeito convencional 80/20, sendo 80% para treinamento e 20% para testes.

```python
X_train, X_test, y_train, y_test = train_test_split(
X_tfidf, y, #matriz de pesos, label (variavel target)
test_size=0.2, #define os 20% de treino
random_state=42, #garante que todas as vezes a divisão seja a mesma
stratify=y # Mantém a proporção das classes

)```

assim, temos agora o dataset dividido em:
- **Treino**: 60542 mensagens (80.0%)
- **Teste**:  15136 mensagens (20.0%)

Todas elas com a mesma proporção de Spams e Hams, devido ao ` stratify = y `.

# Treinamento do Modelo 
Agora iremos ajustar as definições e treinar o modelo usando uma rede neural MLP (MultiLayer Perceptron) que sera alimentado com os dados da nossa matriz de pesos.

## MLP

```python
mlp = MLPClassifier(
    hidden_layer_sizes=(100, 50), #camada oculta com 100 e 50 neuronios
    activation='relu', # função de ativação
    solver='adam', # Metodo para ajuste de pesos durante o treinamento
    max_iter=200, # Máximo de 200 épocas
    random_state=42, # Garante sempre o mesmo resultado
    early_stopping=True, # interrompe o treino se o modelo para de aprender
    validation_fraction=0.1, # Reserva 10% do conjunto para validação.
    verbose=True # Mostra o progresso
)```

Com todas as definições feitas, a linha:
` mlp.fit(X_train, y_train)`
... faz o treinamento do modelo.

## ReLU
Rectified Linear Unit, o ReLU e a nossa funcao de ativiacao, basicamente ela determina o quento do sinal de um neoronio vai passar para o outro.
- se **x < 0** → saida  = o
- se **x ≥ 0** → saida = x

entao, de grosso modo, a funcao relu "mata" valores negativos e repassa valores positivos.
porem isso pode acarretar no problema de morte de neuronios, que se um neuronio se receber muito valores negativos suas funcoes serao zeradas e ele so passara valores negativos, entao o gradiente vira 0 e o neuronio nunca mais aprende, ele "morre".

### Vanishin Gradient
Este e um problema de achatamento do gradiente fazendo com que os neuronios da entrada tenham os valores aproximados de 0, assim repassando o gradinte inteiro a ficar mais "achatado".
