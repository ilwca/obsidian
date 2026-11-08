# Apresentação do artigo: Small Object Detection in Drone Captured Images for Maritime Surveillance

O artigo aborda um tema muito interessante dentro do processamento de imagens: Como detectar objetos muito pequenos em imagens capturadas por drones. Com o foco em embarcações e boias em ambientes marítimos.

O artigo traz duas contribuições muito importantes
- A criação de um dataset de imagens marítimas, chamado **Aussys**.
- Um modelos de detecção de objetos que utiliza a técnica SAHI, podendo trabalhar com diferentes modelos de detecção de objetos.

O problema que este artigo busca resolver, é como identificar objetos maritmos por meio de imagens de drones, quando estes objetos muitas vezes possuem alguns aspectos que dificultam a detecção, como
- Pequena representação - O objeto ocupa poucos pixels da imagem
- baixo contraste - O objeto possui a mesma ou similar cor da água.
- Iluminação - Reflexos solares podem dificultar a identificação
- Ondulações - As ondas possuem padrões que podem ser confundidas com as dos objetos.

## Mas existe outro problema.
As entradas dos modelos de detecção de objetos, nao suportam grandes dimensões, assim agravando ainda mais o problema de pequana representação. Um objeto que ocupava poucos pixel em uma imagem 1920x1080 passa a ocupar menos ainda no redimensionamento de 640x640. 

A solução encontrada pelos pesquisadores e combinar duas estratégias:
- dividir a imagem em partes menores.
- Aplicar um algoritmo de detecção de cada parte e utilizar SAHI para organizar e reunir os resultados.
### SAHI - Slice Aided Hyper Inference
O SAHI e uma tecnica de detecção de objetos pequenos em imagens com alta resolução. Ele e uma estrutura que organiza o modelos das imagens para o processamento dos modelos de detecção.
Podem ser configuradas diferentes tamanhos de divisão, com testado no artigo (9,16,20, 42 e 80). O metodo tambem permite a sobreposição (overlap). Isso é importante, pois podem haver objetos posicionados exatamenta nas bordas entre dois recortes.

Cada recorte e enviado individualmente para o modelo de detecção que retorna 3 saidas diferentes:
- cordeada delimitadora (borda)
- Classes previstas
- Confiança da previsão (da classe prevista)

Posteriormente e feito o calculo da posição original do objeto detectado com relação ao recorte que foi detectado o objeto. Assim os recortes processados sao unidos novamente para a comparação e averiguação de redundancia de detecção, ainda mais quando existe sobreposição de recortes, fazendo com que o mesmo objeto seja detectado em mais de um recorte.

No artigo é usado diferentes modelos de detecção:
- YOLOv5
- YOLOv8
- Detectron

### Ambiente de Pesquisa
Pesquisadores criaram a base de dados Aussys, voltada para a detecção de objetos maritimos. As imagens fora capturadas por meio de um drone DJI com uma camera convencional. A base contem 12.154 imagens, porem todas tiradas no mesmo dia, sob os mesmas condições climaticas e geograficas, sendo estas uma das desvantagens do dataset.

### mAP - Mean Avarage Precision
É uma métrica que avalia a qualidade geral das detecções, considerando precisão e renovação em diferentes níveis de confiança.
podem ser divididos em diferentes criterios de rigorosidade, considerando o IoU (Intersection over Union), como o mAP50, para IoU superior a 0,5 e mAP75 para IoU superior a 0,75.

### Resultados sem SAHI
Houve aplicação do método de detecção para os 3 modelos de classificação sem utilizar o método SAHI, porem com resultados insatisfatórios.

### Resultados com SAHI
Posteriormente aplicado os modelos de detecção com o método SAHI com diferentes números de recortes. Percebendo que o mAP não aumenta proporcionalmente com o numero de recortes, havendo melhores resultados entre 26 e 20 recortes no YOLO.
