# Roteiro de Apresentação: Programação Dinâmica Aplicada ao SSAP

## Informações Gerais da Apresentação

**Título:** Análise e Implementação de Programação Dinâmica para Alocação de Espaço em Prateleiras no Varejo (SSAP)

**Duração Total Estimada:** 25-30 minutos

**Público-Alvo:** Pesquisadores, profissionais de varejo, estudantes de engenharia e ciência da computação

**Objetivo:** Apresentar uma solução exata e eficiente para o problema de alocação de espaço em prateleiras usando programação dinâmica, demonstrando tanto a teoria quanto a implementação prática.

---

## Slide 1: Título (1-2 minutos)

### Conteúdo Visual
- Título principal em tipografia elegante
- Subtítulo destacando a otimização de lucro
- Informações do apresentador e data

### Roteiro do Apresentador

Comece com uma saudação calorosa e apresente-se. Estabeleça o contexto inicial:

"Bom [dia/tarde], meu nome é [seu nome]. Hoje vou apresentar um trabalho sobre um problema clássico do varejo: como alocar produtos em prateleiras de forma a maximizar o lucro. Este é um desafio que varejistas enfrentam diariamente, e vamos explorar como a programação dinâmica oferece uma solução exata e eficiente para este problema."

Pausar por 2-3 segundos para permitir que o público absorva o tema.

---

## Slide 2: Roteiro da Apresentação (1 minuto)

### Conteúdo Visual
- Lista numerada de 8 tópicos principais
- Estrutura em duas colunas para melhor visualização

### Roteiro do Apresentador

"Vamos seguir um roteiro estruturado em oito partes. Começaremos com uma introdução aos conceitos fundamentais de programação dinâmica, depois exploraremos o problema específico de alocação de espaço em prateleiras, avançaremos para a modelagem matemática, implementação do algoritmo, análise de complexidade, comparação com heurísticas convencionais, e finalizaremos com as conclusões e referências. Este roteiro nos permitirá construir uma compreensão sólida do tema, do teórico ao prático."

---

## Slide 3: Programação Dinâmica - A Técnica (3-4 minutos)

### Conteúdo Visual
- Definição de DP com destaque em azul acadêmico
- Imagem ilustrativa mostrando subproblemas sobrepostos (Fibonacci)
- Citação sobre decisão sequencial

### Roteiro do Apresentador

"Programação Dinâmica é uma técnica matemática poderosa para resolver problemas de decisão sequencial. A ideia central é que uma decisão tomada em um ponto do processo influencia as decisões futuras. DP funciona dividindo um problema complexo em subproblemas menores e sobrepostos.

O princípio fundamental é a **memoização**: em vez de recalcular a mesma solução múltiplas vezes, armazenamos os resultados intermediários. Isso evita redundância computacional. Vejam a imagem à direita: ela mostra como o problema de Fibonacci, quando resolvido ingenuamente, recalcula os mesmos valores várias vezes. DP elimina essa redundância.

O objetivo final é encontrar a **solução ótima global**, não apenas uma solução local aceitável. Isso é crucial em problemas de otimização onde queremos garantir o melhor resultado possível."

Pausar para deixar o conceito assentar. Fazer contato visual com a audiência.

---

## Slide 4: Shelf-Space Allocation Problem (SSAP) (3-4 minutos)

### Conteúdo Visual
- Definição formal do SSAP
- Imagem mostrando perspectiva frontal e lateral de uma prateleira com produtos
- Tabela de variáveis chave

### Roteiro do Apresentador

"Agora vamos ao problema específico que nos interessa: o Shelf-Space Allocation Problem, ou SSAP. Este é um problema clássico em otimização de varejo.

Imaginem uma loja de supermercado. Os gerentes precisam decidir quantas unidades de cada produto colocar em uma prateleira específica. Cada produto ocupa espaço (peso em metros lineares), gera lucro, e tem uma quantidade máxima disponível. A prateleira tem uma capacidade total limitada.

O objetivo é simples mas desafiador: **maximizar o lucro total** respeitando a restrição de espaço e a disponibilidade de produtos. Vejam a imagem: ela mostra como produtos diferentes ocupam espaços diferentes em uma prateleira, tanto em perspectiva frontal quanto lateral.

Matematicamente, o SSAP é modelado como um **Problema da Mochila 0-1 Limitada** (Bounded Knapsack Problem). Vamos definir as variáveis:

- **N**: número total de produtos disponíveis
- **C**: capacidade total da prateleira
- **w_i**: peso ou espaço ocupado pelo produto i
- **p_i**: lucro ou valor gerado pelo produto i
- **b_i**: número máximo de cópias disponíveis do produto i

Este é um problema NP-Difícil, o que significa que não existe um algoritmo conhecido que o resolva em tempo polinomial para instâncias grandes. No entanto, para instâncias moderadas, a programação dinâmica oferece uma solução exata."

---

## Slide 5: Modelagem DP - A Recorrência (4-5 minutos)

### Conteúdo Visual
- Definição do estado DP[i][w]
- Fórmula matemática da recorrência em caixa destacada
- Imagem mostrando árvore de decisão do problema da mochila

### Roteiro do Apresentador

"Agora vamos ao coração da solução: a modelagem matemática usando programação dinâmica.

Definimos o **estado DP[i][w]** como o lucro máximo que podemos obter usando apenas os primeiros **i** produtos com uma capacidade exata de **w** unidades de espaço.

A relação de recorrência é apresentada aqui. Vamos entendê-la passo a passo:

DP[i][w] = max(DP[i-1][w], max(DP[i-1][w - k·w_i] + k·p_i))

onde k varia de 0 até min(b_i, ⌊w/w_i⌋).

O que isso significa? Para cada item i e cada capacidade w, temos duas opções principais:

1. **Não incluir o item i**: neste caso, o lucro máximo é DP[i-1][w], ou seja, o lucro máximo usando apenas os primeiros i-1 produtos.

2. **Incluir k cópias do item i**: neste caso, o lucro é DP[i-1][w - k·w_i] + k·p_i. Aqui, k pode variar de 1 até o limite de disponibilidade b_i ou até o máximo que cabe no espaço restante.

Tomamos o máximo entre todas essas opções. A imagem à direita mostra como essa árvore de decisão se estrutura: em cada nó, decidimos se incluímos ou não o item, e se incluímos, quantas cópias.

Este é um exemplo clássico de **otimização local levando à otimização global**: ao fazer a melhor escolha em cada subproblema, garantimos a melhor solução geral."

---

## Slide 6: Algoritmo Implementado - Versão Clássica (3-4 minutos)

### Conteúdo Visual
- Descrição estruturada dos 4 passos principais
- Imagem mostrando visualização de código/dados

### Roteiro do Apresentador

"Vamos agora à implementação prática do algoritmo. Aqui está a versão clássica, implementada em Python.

O algoritmo segue estes passos principais:

**Passo 1: Inicialização.** Criamos uma tabela DP de dimensões (N+1) × (C+1), preenchida com zeros. Isso representa o caso base: com zero produtos ou zero capacidade, o lucro é zero.

**Passo 2: Iteração sobre itens.** Para cada produto i de 1 até N, vamos considerar incluir esse produto na solução.

**Passo 3: Iteração sobre capacidades.** Para cada capacidade possível w de 0 até C, calculamos o lucro máximo.

**Passo 4: Loop interno.** Para cada capacidade w, testamos incluir k cópias do item i, onde k varia de 0 até o mínimo entre a disponibilidade b_i e o número máximo de cópias que cabem no espaço (⌊w/w_i⌋). Aplicamos a relação de recorrência e atualizamos DP[i][w] com o máximo valor encontrado.

Após preencher toda a tabela, o valor ótimo está em DP[N][C]: o lucro máximo usando todos os N produtos com a capacidade total C.

A imagem mostra uma visualização de como essa tabela é construída iterativamente. Cada célula representa uma decisão ótima para um subproblema específico."

---

## Slide 7: Exemplo Numérico e Resultado (4-5 minutos)

### Conteúdo Visual
- Tabela com dados dos 3 itens (peso, lucro, limite)
- Resultado destacado: lucro máximo = 240
- Explicação da alocação ótima

### Roteiro do Apresentador

"Vamos trabalhar com um exemplo concreto para tornar tudo mais tangível.

Suponhamos que temos uma prateleira com capacidade de 50 unidades de espaço. Temos três produtos disponíveis:

- **Item 1**: ocupa 10 unidades de espaço, gera 60 de lucro, com no máximo 2 cópias disponíveis.
- **Item 2**: ocupa 20 unidades de espaço, gera 100 de lucro, com no máximo 1 cópia disponível.
- **Item 3**: ocupa 30 unidades de espaço, gera 120 de lucro, com no máximo 3 cópias disponíveis.

Executando o algoritmo de programação dinâmica, obtemos um **lucro máximo de 240**.

Qual é a alocação ótima? Colocamos **2 cópias do Item 1** (ocupando 20 unidades de espaço e gerando 120 de lucro) e **1 cópia do Item 3** (ocupando 30 unidades de espaço e gerando 120 de lucro). No total, usamos exatamente 50 unidades de espaço e obtemos 240 de lucro.

Note que não incluímos o Item 2, apesar de seu alto lucro unitário. Por quê? Porque se o incluíssemos (20 unidades de espaço), só teríamos 30 unidades restantes, o que nos permitiria apenas 1 cópia do Item 3 (120 de lucro) ou 3 cópias do Item 1 (mas só cabem 2). Isso resultaria em um lucro total menor. O algoritmo encontra essa combinação ótima automaticamente."

Pausar para permitir que o público processe o exemplo.

---

## Slide 8: Ambiente Computacional (2-3 minutos)

### Conteúdo Visual
- Destaque de Python como linguagem escolhida
- Três motivações principais com ícones visuais
- Nota sobre implementação

### Roteiro do Apresentador

"Implementamos este algoritmo em **Python**, e gostaria de explicar por quê.

Primeiro, **facilidade com estruturas de dados**. Python oferece listas e arrays multidimensionais que são perfeitos para a tabela DP. Não precisamos nos preocupar com gerenciamento manual de memória.

Segundo, **interpretabilidade**. O código Python é limpo e legível. Isso facilita não apenas a compreensão do algoritmo, mas também futuras modificações e otimizações.

Terceiro, **bibliotecas nativas**. Python possui bibliotecas poderosas para análise de dados, otimização e visualização. Isso nos permite não apenas implementar o algoritmo, mas também analisar seu desempenho e gerar gráficos.

Implementamos tanto a versão clássica quanto uma versão otimizada usando a técnica de Binary Splitting, que veremos em breve. Ambas as versões estão disponíveis e foram testadas com sucesso."

---

## Slide 9: Análise de Complexidade (4-5 minutos)

### Conteúdo Visual
- Três caixas destacadas: Versão Clássica, Versão Otimizada, Complexidade de Espaço
- Imagem mostrando estrutura recursiva/árvore de subproblemas

### Roteiro do Apresentador

"Agora vamos analisar a complexidade computacional, que é crucial para entender a viabilidade do algoritmo.

**Versão Clássica:**
A complexidade de tempo é O(N · C · max(b_i)). Isso significa que para cada um dos N produtos, para cada uma das C capacidades, testamos até max(b_i) cópias do item. O problema é que se max(b_i) for grande (digamos, 1000), o algoritmo fica muito lento. Isso é uma limitação significativa.

**Versão Otimizada - Binary Splitting:**
Aqui está a inovação chave. Em vez de testar todas as k cópias de um item, usamos uma técnica chamada **Binary Splitting**. Transformamos cada item com limite b_i em um conjunto de itens 0-1 com quantidades 1, 2, 4, 8, ..., 2^k, onde 2^k ≤ b_i. Qualquer número de cópias entre 0 e b_i pode ser representado como uma soma dessas potências de 2.

Isso reduz o loop interno de até b_i iterações para apenas log(b_i) iterações. A complexidade de tempo cai para **O(N · C · log(max(b_i)))**, que é uma melhoria exponencial!

**Complexidade de Espaço:**
Ambas as versões usam O(N · C) de espaço para armazenar a tabela DP. Isso é pseudo-polinomial, o que significa que para valores muito grandes de C, o consumo de memória pode ser proibitivo. No entanto, para instâncias de varejo realistas, isso é aceitável.

A imagem mostra como a estrutura recursiva do problema se organiza. Cada nível da árvore representa uma decisão sobre incluir ou não um item, e a profundidade da árvore é reduzida pelo Binary Splitting."

---

## Slide 10: DP vs. Heurísticas Convencionais (4-5 minutos)

### Conteúdo Visual
- Tabela comparativa com 3 critérios
- Imagem mostrando diagrama técnico de SSAP

### Roteiro do Apresentador

"É importante entender como a Programação Dinâmica se compara a outras abordagens.

**Programação Dinâmica:**
- **Qualidade da Solução**: Ótima global. Garantimos que encontramos o melhor lucro possível.
- **Complexidade**: Pseudo-polinomial, O(N · C · log(max(b_i))) com otimização. Mais lenta que heurísticas, mas viável para instâncias moderadas.
- **Uso Recomendado**: Quando a otimalidade é crítica e as instâncias são de tamanho moderado.

**Heurísticas Gulosas (Greedy):**
- **Qualidade da Solução**: Ótima local. O algoritmo faz a melhor escolha no momento, sem considerar o contexto completo. Frequentemente produz boas soluções, mas não garante otimalidade.
- **Complexidade**: Polinomial, geralmente O(N log N) ou O(N²). Muito mais rápida que DP.
- **Uso Recomendado**: Quando temos instâncias muito grandes ou tempo computacional limitado, e estamos dispostos a aceitar uma solução boa (mas não necessariamente ótima).

**Conclusão:**
A DP otimizada oferece um **equilíbrio** entre otimalidade e eficiência. Para instâncias de varejo realistas (dezenas a centenas de produtos, capacidades de prateleira razoáveis), a DP é viável e oferece soluções garantidamente ótimas.

A imagem mostra um diagrama técnico de SSAP, ilustrando a complexidade do problema real que estamos resolvendo."

---

## Slide 11: Conclusões (3-4 minutos)

### Conteúdo Visual
- Síntese da eficácia da DP
- Caixa destacada sobre Binary Splitting
- Seção de trabalhos futuros
- Imagem técnica de SSAP

### Roteiro do Apresentador

"Vamos sintetizar os pontos principais:

**Síntese:**
Este trabalho demonstrou a eficácia da Programação Dinâmica para resolver o SSAP modelado como um Bounded Knapsack Problem. Implementamos o algoritmo em Python e analisamos seu desempenho.

**Otimização Chave:**
A técnica de **Binary Splitting** foi crucial. Ela reduz a complexidade de tempo de O(N · C · max(b_i)) para O(N · C · log(max(b_i))), tornando a DP uma solução prática e eficiente para instâncias reais de varejo.

**Impacto Prático:**
Varejistas podem usar essa abordagem para maximizar o lucro de forma exata ao alocar produtos em prateleiras. Isso é especialmente valioso em contextos competitivos onde cada unidade de lucro importa.

**Trabalhos Futuros:**
Há várias direções promissoras:
1. **DP multidimensional**: Estender para múltiplas prateleiras simultaneamente.
2. **Meta-heurísticas**: Integrar com algoritmos genéticos ou otimização por colônia de formigas para instâncias muito grandes.
3. **Escalabilidade**: Desenvolver técnicas de decomposição para lidar com milhares de produtos.
4. **Branch-and-bound**: Combinar DP com branch-and-bound para poda mais agressiva e instâncias maiores.

A imagem mostra diagramas técnicos reais de SSAP, reforçando que estamos resolvendo um problema prático e relevante."

---

## Slide 12: Referências (2-3 minutos)

### Conteúdo Visual
- Lista numerada de 4 referências principais
- Formatação acadêmica com DOI

### Roteiro do Apresentador

"Finalizamos com as referências que fundamentam este trabalho.

**Referência [1]** é o artigo principal de Czerniachowska et al. (2021), publicado em Procedia Computer Science. Este artigo apresenta a abordagem DP para SSAP e é a base teórica de nosso trabalho.

**Referências [2] e [3]** são os trabalhos clássicos de Howard (1966) e Bellman (1966) sobre Programação Dinâmica. Bellman é o criador da técnica, e seu trabalho estabeleceu os fundamentos que usamos até hoje.

**Referência [4]** é o artigo anexado de Farias e Gregório (2025), que é o trabalho específico que implementou e analisou a DP para SSAP em Python.

Todas essas referências estão disponíveis e podem ser acessadas para aprofundamento. Agradeço a atenção de todos e fico aberto para perguntas."

---

## Dicas Gerais para o Apresentador

### Gestão do Tempo
- Aloque aproximadamente 2-3 minutos para cada slide de conceito
- Slides com exemplos numéricos podem precisar de 4-5 minutos
- Deixe tempo para perguntas no final de cada seção principal
- Se necessário, você pode pular alguns detalhes técnicos para manter o ritmo

### Técnicas de Apresentação
1. **Contato Visual**: Mantenha contato visual com a audiência, não apenas com os slides
2. **Pausa Estratégica**: Pause após conceitos importantes para deixar o público processar
3. **Exemplos Concretos**: Use o exemplo numérico (Slide 7) para tornar abstrações concretas
4. **Gestos**: Use gestos para enfatizar pontos importantes, especialmente ao explicar a recorrência
5. **Tom de Voz**: Varie o tom para manter a atenção, especialmente em seções técnicas

### Antecipação de Perguntas Comuns
- **"Por que não usar heurísticas?"** Responda que heurísticas são mais rápidas, mas DP garante otimalidade
- **"Qual é o tamanho máximo de instância?"** Depende da capacidade de memória e tempo disponível, mas centenas de produtos com capacidades de milhares são viáveis
- **"Como implementar Binary Splitting?"** Explique que é uma transformação de pré-processamento que converte um bounded knapsack em um 0-1 knapsack
- **"Isso é usado em prática?"** Sim, varejistas usam DP e variações para otimização de prateleiras

### Recursos Adicionais
- Tenha o código Python pronto para demonstração ao vivo se possível
- Prepare gráficos de desempenho (tempo vs. tamanho da instância) para mostrar a melhoria do Binary Splitting
- Considere ter um exemplo interativo onde a audiência pode sugerir um cenário e você executa o algoritmo

---

## Conclusão do Roteiro

Esta apresentação oferece uma jornada completa do conceito teórico de Programação Dinâmica até sua aplicação prática em um problema de varejo real. O equilíbrio entre teoria e prática, combinado com exemplos concretos, deve tornar o conteúdo acessível e envolvente para a audiência.

Boa apresentação!




---

# Dynamic Programin
## Exemplo Numérico
aqui, vamos fazer um exemplificação em um cenário bem reduzido, somente para o entendimento de como funciona.
Então como já dito, estamos buscando o maior lucro com o espaco de 50.

temos 3 itens, que segundo o nosso algoritmo a alocação ótima seria, 2 cópias do item 1 e uma cópia do item 3 

## Analise de complexidade
Agora vamos fazer uma analise da complexidade da função original e de métodos usados para a redução da complexidade.

O(N · C · max(bi))

max(b_i) torna o algoritmo muito custoso qunado se trata de produtos com uma alta quantidade de copias, sendo esse o cenário comum para atacadistas.



==otimização funciona bem porque produtos da mesma categoria têm larguras padronizadas.