
# Imagens, Visão

## Processo de formação de imagens no Olho humano
A Luz entra no olho pela córnea de acordo com o ajuste da íris e dilatação da pupila que define a quantidade desta luz que entra, assim a córnea recebe o estímulo de frequência visível e o cristalino ajuda com a projeção da imagem no fundo do olho, só que de forma invertida por conta de seu formato convexo. Por sua vez, a retina capta a projeção feita na parte interna do olho e decodifica as informações em sinais neurais para enviá-los ao cérebro.

## Luz
A luz é uma pequena parte do espectro eletromagnético, que é sensível às células fotorreceptoras presentes no olho humano, que são os cones e os bastonetes. Ou seja, é o espectro visível que pertence ao espectro eletromagnético que se propaga por meio de fótons que são percebidos pelo olho.
## Cor
A cor é definida pela frequência da onda recebida pelas cones. Assim, ondas de de 400 a 780 nanômetros de frequência são percebidas, variando do vermelho (menor frequência) ao violeta (maior frequência).

## Luminância
Intensidade de energia luminosa recebida na retina.

## Contraste
Influência da luminância de objetos vizinhos.

## Brilho
Luminância percebida influenciada pelo contraste.

## Bandas de Mach
Em bandas de Mach nosso sistema visual tende a alterar os níveis de intensidade de brilho em áreas de borda ou limites de regiões de intensidades diferentes.
## Inibição Lateral
A inibição lateral ocorre porque quando a informação chega a célula, a mesma comunica para sua proximidade, que a cor enxergada é o contrário, e quando a informação chega a periferia, está também passa a informação inversa, havendo assim um choque de informações, fazendo com que seja percebi o meio termo da informação.
## Contraste Simultaneo
O contraste simultâneo alega que o brilho percebido de uma figura ou superfície é afetado diretamente por sua proximidade, contexto ou background.
## Ilusão de Ótica
As ilusões de ótica são causadas por interpretações precipitadas do cérebro que ao receber a informação tenta preencher as lacunas com informações criadas, assim percebendo propriedades geométricas de objetos de maneira equivocada.

---

# Digitalização
Para ser efetuado o processo de digitalização, o alvo deve estar bem iluminado, entoa mecanismos como espelhos, lentes, filtros e sensores, fazem a cabeça de leitura. Esta é movida por todo o objeto para refletir a imagem deste por um espelho em ângulo para outro espelho. O último reflete a imagem para uma lente que foca a imagem através de um filtro no sensor CCD. O sensor CCD é composto por diodos fotossensíveis, que transformam brilho recebido em carga elétrica, mapeando todo o objeto e transformando o brilho refletido em elétrons

## Amostragem
É o processo de converter uma imagem contínua (do mundo real) em uma matriz discreta de pontos, definindo a resolução espacial por meio da quantização.

## Vizinhanca-4
Dado um pixel $P$ definido por $(x,y)$, sua vizinhança-4 é dada por :$\{(x+1,y), (x,y+1), (x-1,y), (x,y-1)\}$. sendo os pixels adjacentes horizontais e verticais.
## Vizinhanca Diagonal
á Vizinhança diagonal é, considerando o mesmo $P$, sua vizinhança diagonal seria $\{(x+1,y+1),(x+1,y-1),(x-1,y+1) , (x-1,y-1)\}$, ou seja, os pixels adjacentes diagonais.
## Vizinhanca-8
A vizinhança de 8 é a junção de vizinhança-4 e diagonal. Para o mesmo $P$, temos $\{(x+1,y), (x,y+1), (x-1,y) (x+1,y+1),(x+1,y-1),(x-1,y+1),(x-1,y-1)\}$. Assim sendo, todos os pixels adjacentes a $P$.

## Interpolação
Interpolação é o processo de usar dados conhecidos para estimar valores em locais desconhecidos. Interpolação é extensivamente usada em tarefas como ampliação (zoom), redução, rotação e correções geométricas.

---
