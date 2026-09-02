Alguns principios a serem abordados
- Paretto Frontier $\Rightarrow$ Para analise dos resultados.

```roadmap
TCC
│
├── 1. INTRODUÇÃO
│
├── 2. FUNDAMENTAÇÃO TEÓRICA
│   ├── 2.1 Redes neurais artificiais
│   ├── 2.2 MLP
│   ├── 2.3 CNN
│   ├── 2.4 Quantização
│   ├── 2.5 Quantização pós-treinamento
│   ├── 2.6 Poda de redes neurais
│   ├── 2.7 Poda estruturada
│   ├── 2.8 Computação aproximada
│   ├── 2.9 Somadores aproximados
│   ├── 2.10 Multiplicadores aproximados
│   ├── 2.11 MAC
│   └── 2.12 Arrays sistólicos
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

## Consumo energetico
Estabelecer uma base, modelo original contendo informacoes, como:

|Métrica|Modelo original|
|---|--:|
|Acurácia|98.x%|
|Tamanho|X MB|
|Número de parâmetros|X|
|MACs|X|
|Latência|X ms|
|Energia*|opcional|

Para a metrica de energia, podemos acompanhar o treinamento e inferencia por meio de software:
- **NVIDIA Management Library (`nvidia-smi` / `pynvml`):** Reporta o consumo em Watts da placa em tempo real diretamente do driver da GPU.
- **CodeCarbon:** Pacote em Python que monitora o consumo do hardware (GPU/CPU) durante a execução e estima a pegada de carbono do modelo.
