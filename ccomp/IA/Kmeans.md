
## Do DataSet
O projeto visa a segmentação de clientes de uma distribuidora atacadista, utilizando o Wholesale Customers Data Set. Este dataset é composto por 440 amostras e 6 variáveis contínuas, que representam os gastos anuais em unidades monetárias nas categorias de produtos: Fresh, Milk, Grocery, Frozen, Detergents_Paper e Delicassen. O objetivo é aplicar o Machine Learning Não Supervisionado para descobrir grupos de clientes com padrões de consumo similares.

## Resumo das funções principais


- carregar_dados()
    
    - Entrada: nenhuma
    - Saída: tupla (X, feature_names) — X: ndarray com dados; feature_names: lista de nomes de colunas
    - O que faz: procura pelo arquivo `archive/Wholesale customers data.csv` ou `Wholesale customers data.csv`; se não encontrar, tenta baixar/extraí-lo automaticamente do repositório UCI (ZIP). Remove colunas `Channel` e `Region` quando presentes (manter apenas features numéricas).
    - Efeito colateral: pode baixar um ZIP e extrair um CSV; lança FileNotFoundError com mensagem clara se falhar.

- preprocessar(X)
    
    - Entrada: X (array ou matriz de características)
    - Saída: X_scaled (array padronizado), scaler (objeto StandardScaler)
    - ==O que faz: aplica StandardScaler.fit_transform em X e retorna os dados normalizados e o scaler para possíveis inversões.
    - Observações: mantém a lógica do pipeline de ML; não altera X original.

- avaliar_k(X, k_min=2, k_max=10)
    
    - Entrada: X (dados já escalados), k_min, k_max (inteiros)
    - Saída: resultados (dict k -> silhueta média), modelos (dict k -> KMeans ajustado)
    - ==O que faz: para cada k no intervalo, ajusta KMeans (n_init=15, max_iter=300), calcula silhouette_score e guarda o modelo e a métrica; imprime cada resultado.
    - Efeito colateral: treina vários modelos (potencialmente custoso em tempo/CPU).

- plot_silhueta_curva(resultados, melhor_k, pasta_saida)
    
    - Entrada: resultados (dict), melhor_k (int), pasta_saida (string)
    - Saída: caminho do arquivo salvo (string)
    - ==O que faz: cria e salva um gráfico (PNG) que mostra coeficiente de silhueta vs k, destaca o melhor k e rotula pontos com valores.
    - Efeito colateral: salva `silhueta_vs_k.png` em [pasta_saida](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html).
- plot_clusters(X, modelo, k, feature_names, pasta_saida)
    
    - Entrada: X (escalado), modelo (KMeans treinado), k (int), feature_names (lista), pasta_saida (string)
    - Saída: caminho do arquivo salvo (string)
    - ==O que faz: reduz X a 2D com PCA, projeta centróides, plota pontos coloridos por cluster e centróides, salva PNG (`clusters_visualizacao.png`).
    - Observações: usa PCA para visualização — metadados de variância explicada apresentados nos rótulos dos eixos.
- plot_silhueta_detalhada(X, modelo, k, pasta_saida)
    
    - Entrada: X (escalado), modelo (KMeans), k (int), pasta_saida (string)
    - Saída: caminho do arquivo salvo (string)
    - ==O que faz: calcula silhouette_samples, organiza e desenha a distribuição de silhueta por cluster (gráficos em faixas), desenha linha da média e salva PNG (`silhueta_detalhada.png`).
    - Observações/robustez: a versão atual converte arrays com np.asarray e assegura que valores são numéricos (foi ajustada para evitar erros de tipagem).
- gerar_relatorio(resultados, melhor_k, melhor_silhueta, X, modelo, feature_names, pasta_saida)
    
    - Entrada: resultados (dict), melhor_k (int), melhor_silhueta (float), X (dados), modelo (KMeans), feature_names, pasta_saida
    - Saída: caminho do arquivo de texto salvo (string)
    - ==O que faz: monta um relatório textual com metodologia, estatísticas do dataset, resultados por k, conclusão/interpretação baseada na silhueta, métricas adicionais (inertia e composição dos grupos) e salva [relatorio.txt](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html).
    - Efeito colateral: cria/reescreve arquivo de relatório na pasta de saída e imprime o relatório no stdout.
- main()
    
    - Entrada: nenhuma (ponto de entrada do script)
    - Saída: nenhuma (efeitos: arquivos gerados / impressões no console)
    - O que faz: orquestra o pipeline completo:
        1. cria pasta de saída;
        2. carrega dados (com fallback/download);
        3. pré-processa (padroniza);
        4. avalia K para um intervalo e seleciona o melhor k;
        5. gera e salva gráficos (curva de silhueta, clusters, silhueta detalhada);
        6. gera relatório final.
    - Efeito colateral: vários arquivos salvos em [output](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) e mensagens exibidas no console. Trata FileNotFoundError no carregamento para saída amigável.

## Observações rápidas / pontos de atenção

- O pipeline assume dados numéricos e remove `Channel`/`Region` quando presentes (comportamento apropriado para o dataset UCI).
- Operações que podem falhar por ausência de dados: [carregar_dados()](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) — já contém fallback e mensagens; para execução off-line, coloque o CSV em [archive](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) ou na raiz.
- Treinamento com vários k pode ser custoso em tempo; considere reduzir o range de k ou usar amostras menores durante experimentos rápidos.
- Saídas principais (na pasta [output](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)): `silhueta_vs_k.png`, `clusters_visualizacao.png`, `silhueta_detalhada.png`, [relatorio.txt](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html).

Quer que eu gere também um README curto com instruções para rodar o script (com exemplos de linha de comando e requisitos do [requirements.txt](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html))? Ou que eu adicione um argumento CLI para especificar o caminho do CSV (ex.: `--data path/to/file.csv`)?