IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

1

Transform Quantization for CNN Compression

Sean I. Young , Member, IEEE, Wang Zhe , Member, IEEE,
David Taubman , Fellow, IEEE, and Bernd Girod , Fellow, IEEE

Abstract—In this paper, we compress convolutional neural network (CNN) weights post-training via transform quantization. Previous
CNN quantization techniques tend to ignore the joint statistics of weights and activations, producing sub-optimal CNN performance at
a given quantization bit-rate, or consider their joint statistics during training only and do not facilitate efficient compression of already
trained CNN models. We optimally transform (decorrelate) and quantize the weights post-training using a rate–distortion framework
to improve compression at any given quantization bit-rate. Transform quantization unifies quantization and dimensionality reduction
(decorrelation) techniques in a single framework to facilitate low bit-rate compression of CNNs and efficient inference in the transform
domain. We first introduce a theory of rate and distortion for CNN quantization, and pose optimum quantization as a rate–distortion
optimization problem. We then show that this problem can be solved using optimal bit-depth allocation following decorrelation by the
optimal End-to-end Learned Transform (ELT) we derive in this paper. Experiments demonstrate that transform quantization advances
the state of the art in CNN compression in both retrained and non-retrained quantization scenarios. In particular, we find that transform
quantization with retraining is able to compress CNN models such as AlexNet, ResNet and DenseNet to very low bit-rates (1–2 bits).

Index Terms—convolutional neural networks, transform coding, compression, quantization, learned transforms.

1

INTRODUCTION

✦

C

ONVOLUTIONAL neural networks (CNNs) have become a
universal framework for solving a number of problems
in pa:ern analysis and computer vision, from classiﬁcation
[1], segmentation [2] and style transfer [3, 4] of images to the
synthesis of images [5]. While CNNs outperform traditional
non-learning-based methods in many vision problems, they
can involve tens or hundreds of millions of parameters, and
their sheer bulk renders deploying CNNs on mobile devices
diﬃcult. CNN weights no longer ﬁt in the cache at the same
time, and they must be loaded from the oﬀ-chip memory as
required, which can be very energy-consuming [6]. Even the
amount of oﬀ-chip memory can be limited on these devices
so the storage of weights is itself a challenge. Moreover, the
number of computations performed on these CNN weights
may hinder the use of CNNs for certain interactive and real-
time applications. One way to reduce the computational and
the storage burden of CNNs is to compress and simplify the
representation of their numerous weight parameters.
  Recent CNN compression techniques may be categorized
as weight pruning [7–21], weight quantization [20–46], and
dimensionality reduction of weight matrices [47–56]. Out of

•  S.  I.  Young  and  B.  Girod  are  with  the  Information  Systems  Laboratory
(ISL), Department of Electrical Engineering, Stanford University, Stanford
CA 94305, USA. E-mail: sean0@stanford.edu, bgirod@stanford.edu.
•  W. Zhe was with the Information Systems Laboratory (ISL), Department of
Electrical Engineering, Stanford University. He is now with the Institute
for Infocomm Research, A*STAR, Singapore.
Email: wang_zhe@i2r.a-star.edu.sg

•  D. Taubman is with the School of Electrical Engineering and Telecommu-
nications, University of New South Wales, Sydney, NSW, Australia.
E-mail: d.taubman@unsw.edu.au

Manuscript  received  28  August  2020;  revised  12  March  2021;  accepted  25
April  2021.  Date  of  publication  25  April  2021;  date  of  current  version
3 May 2021. (Corresponding author: Sean I. Young.)
Recommended for acceptance by
For  information  on  obtaining  reprints  of  this  article,  please  send  email  to:
reprints@ieee.org, and reference the Digital Object Identifier below.
Digital Object Identifier no. 10.1109/TPAMI.2020.

these, weight quantization has shown particular usefulness
for compressing CNNs to binary or tertiary representations
[28–30], at various rate–accuracy trade-oﬀs [36, 37] and even
post-training [38] without any labeled data. However, while
current quantization methods yield good compression, they
tend to ignore the joint statistics of weights and activations
and produce sub-optimum network performance at a given
quantization bit-rate, or consider their joint statistics during
training only [45], and do not facilitate eﬃcient compression
of already-trained networks.
  For post-training compression, optimum decorrelation of
the weights coupled with optimum bit-depth allocations can
signiﬁcantly improve compression especially at the low bit-
rates similar to vector quantization [22–26], but without the
increase in the encoding complexity from the irregularity of
quantization cells. In practice, scalar quantization following
a decorrelating transform is preferred to vector quantization
as suggested by the success of image compression methods
based on e.g. the Discrete Cosine Transform (DCT) [57] and
the Discrete Wavelet Transform (DWT) [58]. The latest video
coding standard VVC [59] can even select the best transform
from DCT-II, -VIII and DST-VII, Trellis-coding the resulting
transform coeﬃcients to further improve compression.

In this work, we propose to quantize CNN weights post-
training using transform quantization. We analyze the CNN
compression problem from a rate–distortion viewpoint, and
show that a particular decorrelating transform coupled with
optimum bit-depths can solve this problem. Transforming a
convolutional or a fully-connecting layer enables dimension
reduction similar to PCA, while quantizing the insigniﬁcant
transform kernels to zero at low rates emulates the behavior
of pruning methods. Therefore, transform quantization uses
all three ingredients of CNN compression—dimensionality
reduction of weights, quantization, and pruning—and also
enables mixed-precision inference on specialized hardware
if diﬀerent bit-depths are assigned to channels. In Fig. 1, we
illustrate the two components (transform and quantization)

0162-8828 © 2020 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission.
See https://www.ieee.org/publications/rights/index.html for more information.

2

m
r
o
f
s
n
a
r
T
)
a
(

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

θ1  θ2

. . .

θ𝑚

→

s1  s2  . . .   s𝑛

t1  t2

. . .

t𝑚

Θ𝑙 ∈ ℝ2×2

𝑛×𝑚

S𝑙 ∈ ℝ1×1

𝑛×𝑛         T𝑙 ∈ ℝ2×2

𝑛×𝑚

e
z
i
t
n
a
u
Q

)
b
(

𝑅1 = 3bits
𝑅2 = 4bits

.

.

.

𝑅𝑛 = 5bits

→

𝑅1  𝑅2  . . .  𝑅𝑛

𝑅1
𝑅2

.

.

.

𝑅𝑛

4bits avg w/o transform

2bits avg with transform

---

Gao et al. [73] estudam os limites da compressão de CNNs a partir de uma perspectiva de **taxa-distorção**, reinterpretando a compressão como um problema de **alocação de taxa**, de maneira semelhante à abordagem deste trabalho.

Entretanto, o estudo deles não considera o uso de uma **transformação como parte da quantização**. A Seção 4 mostra que aplicar uma **transformação de descorrelação antes da quantização** é fundamental para obter uma boa compressão.

# 3 NOTAÇÃO E OBSERVAÇÕES

Vamos estabelecer nossa notação definindo um **espaço vetorial** sobre as entradas, saídas e pesos de uma CNN, equipado com operações baseadas em **convoluções multi-entrada-multi-saída (MIMO — multi-input-multi-output)** [74].

Denotamos por

$$x∈Rma×bx \in \mathbb{R}^{a \times b}_m$$

um **sinal com mm canais**, cujos elementos são matrizes de tamanho $a \times b$, isto é,

$$xk∈Ra×b,k=1,…,m.x_k \in \mathbb{R}^{a \times b}, \quad k = 1, \ldots, m.$$

Denotamos por

$$Θ∈Rn×ma×b\Theta \in \mathbb{R}^{a \times b}_{n \times m}$$

uma **camada convolucional com mm canais de entrada e nn canais de saída**, cujos kernels de convolução

$$θkj∈Ra×b\theta_{kj} \in \mathbb{R}^{a \times b}$$

são definidos para

$$k=1,…,nk = 1, \ldots, n$$

e

$$j=1,…,m.j = 1, \ldots, m.$$

Agora podemos equipar os dois espaços

$$Rma×b\mathbb{R}^{a \times b}_m$$

e

$$Rn×ma×b\mathbb{R}^{a \times b}_{n \times m}$$

com as seguintes operações de espaço vetorial.

### Definição 1: Produto interno

O produto interno de dois sinais de mm canais dados,

$$x,y∈Rma×b,x,y \in \mathbb{R}^{a \times b}_m,$$

pode ser definido como

$$⟨x,y⟩=⟨x1,y1⟩F+⋯+⟨xm,ym⟩F∈R,(1)\langle x,y\rangle = \langle x_1,y_1\rangle_F +\cdots+ \langle x_m,y_m\rangle_F \in \mathbb{R}, \tag{1}$$

em que

$$⟨x,y⟩F\langle x,y\rangle_F$$

denota o **produto interno de Frobenius** dos elementos matriciais

$x,y∈Ra×b.x,y \in \mathbb{R}^{a \times b}.$

### Definição 2: Norma Euclidiana

A norma Euclidiana de um sinal de mm canais dado,

$x∈Rma×b,x \in \mathbb{R}^{a \times b}_m,$

pode ser definida utilizando (1) como

$∥x∥2=⟨x,x⟩=∥x1∥F2+⋯+∥xm∥F2∈R+,(2)\|x\|_2 = \sqrt{\langle x,x\rangle} = \sqrt{ \|x_1\|_F^2 +\cdots+ \|x_m\|_F^2 } \in \mathbb{R}_+, \tag{2}$

em que

$$∥x∥F\|x\|_F$$

denota a **norma de Frobenius** de

$$x∈Ra×b.x \in \mathbb{R}^{a \times b}.$$

### Definição 3: Produto camada–camada

O **produto camada–camada**

$$Z=XYZ = XY$$

de

$$X∈Ro×na×bX \in \mathbb{R}^{a \times b}_{o \times n}$$

e

$$Y∈Rn×mc×dY \in \mathbb{R}^{c \times d}_{n \times m}$$

é definido como

$$Zkj=(xk1⋆y1j+⋯+xkn⋆ynj)∈R(∣a−c∣+1)×(∣b−d∣+1)(3)Z_{kj} = (x_{k1}\star y_{1j} +\cdots+ x_{kn}\star y_{nj}) \in \mathbb{R}^{(|a-c|+1)\times(|b-d|+1)} \tag{3}$$

para

$$k=1,…,ok = 1,\ldots,o$$

e

$j=1,…,m,j = 1,\ldots,m,$

onde ⋆\star representa a **convolução 2D válida (_valid_)** — em oposição às convoluções _full_ ou _same_.

Observe que

$$x⋆y=⟨x,y⟩Fx\star y = \langle x,y\rangle_F$$

quando xx e yy possuem as mesmas dimensões.

Em contraste com as Definições 1–2, a Definição 3 pode envolver elementos de dois espaços vetoriais (possivelmente diferentes). Analogamente, podemos derivar as definições de **produto camada–sinal** e **produto externo** a partir da Definição 3.

A **transposta**

$$Θt∈Rm×na×b\Theta^t \in \mathbb{R}^{a\times b}_{m\times n}$$

de uma camada

$$Θ∈Rn×ma×b\Theta \in \mathbb{R}^{a\times b}_{n\times m}$$

é definida por

$$(Θt)jk=Θkj,(\Theta^t)_{jk}=\Theta_{kj},$$

de maneira análoga à transposta de uma matriz convencional.

Com as definições acima, podemos expressar de forma compacta o mapeamento de uma imagem de mm canais

$$x∈Rmc×dx\in\mathbb{R}^{c\times d}_m$$

por uma camada convolucional

$$Θ∈Rn×ma×b\Theta\in\mathbb{R}^{a\times b}_{n\times m}$$

com mm entradas e nn saídas como

$$x↦Θx.x\mapsto\Theta x.$$

Observe que, como os filtros formam um **anel** (mas não um **corpo**) em relação à convolução, decomposições matriciais clássicas, como **LU** e **QR**, não podem ser aplicadas à camada convolucional Θ\Theta.

Entretanto, uma transformação linear

$$Θ=ST\Theta=ST$$

continua sendo bem definida.

Neste trabalho, essencialmente transformamos todos os mapeamentos convolucionais da forma

$$x↦Θxx\mapsto\Theta x$$

para

$$x↦STxx\mapsto STx$$

e quantizamos SS e TT.

Veja a Figura 1 (à esquerda), onde

$$Θ,T∈Rn×m2×2\Theta,T\in\mathbb{R}^{2\times2}_{n\times m}$$

representam camadas convolucionais 2×22\times2, e

$$S∈Rn×n1×1S\in\mathbb{R}^{1\times1}_{n\times n}$$

representa uma **camada de base (basis layer)**, que é equivalente a uma camada convolucional $1×11\times1$.

## 4 QUANTIZAÇÃO DE CNNs

Este trabalho aborda o problema de compressão das matrizes de pesos de uma CNN. Podemos expressar o mapeamento de ponta a ponta de uma CNN feed-forward de L camadas como

$$y = f(x|\Theta_1,\ldots,\Theta_L) = f_L(\cdots f_2(\Theta_2 f_1(\Theta_1x))), \tag{4}$$

em que $x \in \mathbb{R}^{a\times b}_M$ e $y \in \mathbb{R}^{c\times d}_N$ são, respectivamente, a entrada e a saída da rede, e $Θl=1,…,L\Theta_{l=1,\ldots,L}$ são as L matrizes de pesos convolucionais e totalmente conectadas que parametrizam f.

As não linearidades entre as convoluções, como _pooling_, ativação (ReLU ou tanh) e normalização, foram incorporadas às funções $f_l$, juntamente com os _biases_.

Embora os parâmetros de _bias_ também sejam aprendíveis e, portanto, também precisem ser quantizados e armazenados, eles são suficientemente poucos em relação aos pesos, de modo que seu impacto no tamanho quantizado das CNNs é desprezível.

Quando uma CNN de classificação está sendo quantizada, assume-se que a saída y corresponde aos _logits_, isto é, ao resultado obtido antes da ativação _softmax_.

Para fornecer um exemplo concreto, o AlexNet [1] parametriza f utilizando L=8 conjuntos de pesos convolucionais e totalmente conectados. A entrada $x \in \mathbb{R}^{224\times224}_3$ representa uma imagem colorida com $224\times224$ pixels, enquanto a saída $y \in \mathbb{R}^{1\times1}_{1000}$ representa as 1000 log-probabilidades não normalizadas de pertencimento da entrada x às 1000 classes predefinidas (_tench_, ..., _toilet paper_).

A primeira camada convolucional

$$\Theta_1 \in \mathbb{R}^{11\times11}_{64\times3}$$

possui $64\times3$ kernels convolucionais de tamanho $11\times11$, enquanto a última camada totalmente conectada pode ser representada por

$$\Theta_8 \in \mathbb{R}^{1\times1}_{1000\times4096}.$$

---


Fig. 1. Transform quantization of CNN layers. Given weight matrices Θ1, Θ2, . . . , ΘL of an L-layer CNN, we represent each one as Θl = SlTl (a) and
quantize both the kernel matrix Tl and the basis Sl optimally (b). In (b), the bar lengths illustrate the bit-depths needed to quantize Θl directly (gray
bars), or SlTl in the transform domain (blue and orange bars) for the same performance. Elements corresponding to zero bit-depth assignments
(Rk = 0) are indicated as white blocks in (a).

of transform quantization. A ℎ × 𝑤 convolution layer (gray)
is transformed to a pair of basis (blue) and transform domain
(orange) convolutional layers (a), then the pair quantized to
rate–distortion  optimum  bit-depths  (b).  In  the  absence  of
quantization, composing the mappings of this pair of layers
recovers (or synthesizes) the original one. Signal processing
literature uses the term “transform coding” more commonly
than “transform quantization”. However, we adopt the la:er
term in this work to stress our focus on quantization rather
than (entropy) coding, which we address in our sequel.
  Our main contributions are as follows. First, we propose
transform quantization for compressing CNN weights—we
are the ﬁrst to consider quantization of transformed weights
and basis, and optimize both post-training. Second, we give
a theory of rate and distortion for CNN quantization, based
on which transform coding gains can be computed. We then
derive an end-to-end-learned transform that maximizes the
gains. Third, we advance the state of the art in compression
of CNNs, in both retrained and non-retrained scenarios, for
image classiﬁcation—AlexNet [1], ResNets [60], DenseNets
[61], and for low-level vision tasks, DRUNet (denoising) [62]
and EDSR (super-resolution) [63].

2  RELATED WORK

CNN compression methods based on pruning [7–20] nullify
kernels [7–13], channels [14–17], or even individual weights
[18–20] that are insigniﬁcant according to such criteria as a
norm [7–9] or some objective function [18]. However, while
a few methods [20] compress the pruned weights further via
quantization and variable-length (Huﬀman) coding, optimal
quantization of pruned networks generally remains an open
problem. Moreover, the pruning criteria are often chosen in
a heuristic manner agnostic to the actual accuracy losses. By
contrast,  our  transform-quantization  framework  quantizes
to zero (i.e. prunes) kernels which are deemed insigniﬁcant
according to bit-depth–accuracy optimality criteria.
  Contemporaneous with the pruning-based techniques for
CNN compression, some researchers proposed to compress
CNNs ﬁrst by spatially decorrelating their weights with the
DCT, followed by vector quantization [24] or hashing [26] of
the decorrelated weights to further reduce the redundancies
across the transformed kernels. These transform approaches
are, however, applicable to the compression of convolution
kernels only, computationally complex due to the clustering
involved [24], or cache-ineﬃcient due to using hashtables as
the main data structure [26]. Moreover, some CNN models
contain large numbers of 1 × 1 convolutional kernels, where
the beneﬁt of spatial decorrelation of kernels via the DCT is

less signiﬁcant. In contrast with the spatial-transform-based
approaches, our quantization framework transforms across
(rather than within) kernels to provide the compression and
eﬃciency gains even for smaller convolution kernels.

In parallel with the DCT techniques above, other authors
sought to reduce the dimensionality of CNN layers via PCA
and related techniques [47–56]. Denton et al. [47] apply the
SVD across kernels in convolution layers, or across the rows
and columns of weight matrices for fully-connecting layers
to project input or output to low-rank subspaces, providing
computational savings during the inference stage. Zhang et
al. [51] extend this method by using the generalized SVD to
take into account the presence of ReLU activations between
successive layers. This work was extended in turn by Kim et
al. [52], who apply the SVD on all four axes of convolutional
tensors. Li et al. [49] extend the work of [51] by partitioning
the kernels into subsets, then using the SVD on each subset
of kernels separately. However, PCA-based compression is
not concerned with quantization, so optimal quantization of
the projected network remains an open problem. Also, PCA
methods determine the projection dimensions heuristically
using decorrelated weight variances [51, 52], by minimizing
a least-squares criterion [50] or using dimension assignment
rules [54], none of which reﬂect the actual loss of prediction
accuracy due to the projections. By contrast, our framework
determines the quantization bit-depths and their associated
projection dimensions to minimize the performance loss at a
given quantization bit-rate (average bit-depth).
  Quantization methods (both vector and scalar) for CNNs
[20–46] have developed alongside pruning methods. Vector
quantization of weights [22–26] involves 𝑘-means [22–24] or
a “hashing trick” [25, 26] and may additionally involve the
DCT [24, 26] and residual quantization [22]. Uniform scalar
quantization of weights to one bit (binary representation) is
proposed by Hubara et al. [31, 41], and to two bits (ternary)
by Zhu et al. [30]. LQ-Nets [37] learn the optimal quantizers
during training at a speciﬁed bit-depth. Non-uniform scalar
quantization was proposed by Tung and Mori [21], whereas
Zhou et al. [36] demonstrate that we can quantize networks
post-training, provided that weights can be reﬁned by some
additional training after quantizing (we refer to this process
as re-training). Recent methods [38, 43] propose to quantize
networks in a training-free manner, based on a per-channel
bit-depth allocation paradigm [38], or by equalizing weights
and correcting biases [43]. We extend per-channel bit-depth
allocation and re-training to the transform domain.
  Designing lightweight CNNs such as MobileNet [64] and
SqueezeNet [65] is another form of model compression. One
can relate the depthwise convolution layers of [64] to perfect

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

3

)
B
d
(

n
i
a
g

g
n

i

d
o
C

KLT

ELT

KLT

ELT

Layer number (𝑙)

Layer number (𝑙)

Row number (𝑘)

Row number (𝑘)

𝑙 = 3

𝑙 = 3

Fig. 3. Coding gains due to the KLT and the ELT applied onto the rows of weight matrices Θl. Convolution and fully-connected layers of ResNet-18
exhibit KLT coding gains of 1–7 dB and ELT ones of 1–12 dB (left plots), where the blue and the orange bars indicate the gain components due to
the decorrelation of weights and gradients, respectively. A coding gain of G produces a rate-saving of 1
G. The per-matrix coding gains can be
broken down further into per-column coding-gains shown in the right sub-plots for layers 3 of ResNet-18 (right).

2 log

2

𝜆 = 1

𝜆 = 3

3  NOTATION AND REMARKS

)

𝐷
1
−
𝜇
(

n
o
i
t
r
o
t
s
i
D

Layer bit-depth (𝑅𝑙)

Layer bit-depth (𝑅𝑙)

Fig. 2. Rate–distortion optimal layer bit-depth assignment. For a given
rate–distortion  trade-off λ,  we  sweep  the  bit-depth–distortion  curve  of
each layer (blue and orange lines) to find the bit-depth values Rl where
the slope is equal to −λ (black dots).

diagonalization of weight matrices using the SVD, while the
reduced-input-channel 3 × 3 convolution [65] relates closely
to the projection of input spaces to their lower-dimensional
sub-spaces, both during training. However, discovering the
optimum lightweight CNN models can be challenging since
architecture design decisions must be made prior to training
the network. Optimal quantization of the resulting network
also remains a problem. Transform quantization is based on
the same decorrelating (diagonalizing) principles, inducing
a low-dimensional projection of weights at low quantization
bit-rates. However, our framework has the advantage that it
jointly addresses optimal quantization, post-training.
  Oktay et al. [45] and Huang et al. [66] propose to impose
kernel decorrelation at training time, rather than decorrelate
them post hoc. Although such strategies can be beneﬁcial for
reducing model redundancy, they increase training time if a
high degree of orthogonality is needed [66], do not facilitate
compression of already-trained models, and leaves open the
optimal choice of decorrelating transform [45] as well as the
problem of optimally quantizing the decorrelated kernels. A
related class of methods known as natural gradient descent
[67–72] propose to accelerate the training of CNNs via local
normalization of the loss landscape before taking descent. In
contrast with natural gradient descent where transforms are
used to whiten weight gradient, our framework decorrelates
(but not whiten) the weights themselves prior to quantizing
to improve the quantizer’s “packing”.
  Gao et al. [73] study the limits of CNN compression from
a rate–distortion perspective, reinterpreting compression as
a rate-allocation problem similarly to this work. Their study
however does not consider the use of a transform as part of
quantization. Section 4 shows that applying a decorrelating
transform before quantizing is key to good compression.

Let us set our notation by deﬁning a vector space over CNN
input, output and weights, equipped with operations based
on multi-input-multi-output (MIMO) convolutions [74]. We
𝑚  an 𝑚-channel signal whose elements are
denote by x ∈ ℝ𝑎×𝑏
matrices of size 𝑎 × 𝑏, that is, 𝑥𝑘 ∈ ℝ𝑎×𝑏 for 𝑘 = 1, . . . , 𝑚. We
𝑛×𝑚 a convolutional layer with 𝑚 input and
denote by Θ ∈ ℝ𝑎×𝑏
𝑛 output channels whose convolution kernels 𝜃𝑘𝑗 ∈ ℝ𝑎×𝑏 for
𝑘 = 1, . . . , 𝑛 and 𝑗 = 1, . . . , 𝑚. One is now ready to equip the
𝑛×𝑚 with  the  following  vector  space
two  spaces ℝ𝑎×𝑏
operations.

𝑚  and ℝ𝑎×𝑏

Deﬁnition 1: Inner product. The inner product of two given
𝑚-channel signals x,  y ∈ ℝ𝑎×𝑏

𝑚  can be deﬁned as

〈x,  y〉 = 〈𝑥1, 𝑦1〉𝐹 + ⋅ ⋅ ⋅ +〈𝑥𝑚, 𝑦𝑚〉𝐹 ∈ ℝ,
in which 〈𝑥, 𝑦〉𝐹  denotes the Frobenius inner product of the
matrix-elements 𝑥, 𝑦 ∈ ℝ𝑎×𝑏.

(1)

Deﬁnition 2: Euclidean norm. The Euclidean norm of given
𝑚-channel signal x ∈ ℝ𝑎×𝑏

𝑚  can be deﬁned using (1) as
2 ∈ ℝ+,
2 + ⋅ ⋅ ⋅ +‖𝑥𝑚‖𝐹

‖x‖2 = √〈x,  x〉 = √‖𝑥1‖𝐹

(2)

 in which ‖𝑥‖𝐹  denotes the Frobenius norm of 𝑥 ∈ ℝ𝑎×𝑏.

Deﬁnition 3: Layer–layer product. The layer-layer product
Z = XY of X ∈ ℝ𝑎×𝑏

𝑜×𝑛 and Y ∈ ℝ𝑐×𝑑

𝑛×𝑚 is deﬁned as

Z𝑘𝑗 = (𝑥𝑘1 ⋆ 𝑦1𝑗 + ⋅ ⋅ ⋅ + 𝑥𝑘𝑛 ⋆ 𝑦𝑛𝑗) ∈ ℝ(|𝑎−𝑐|+1)×(|𝑏−𝑑|+1)  (3)

for 𝑘 = 1, . . . , 𝑜 and 𝑗 = 1, . . . , 𝑚, where ⋆ represent valid (as
opposed to full or same) 2D convolution1. Observe that each
𝑥 ⋆ 𝑦 = 〈𝑥, 𝑦〉𝐹  if 𝑥 and 𝑦 have the same dimensions.

In contrast with Deﬁnitions 1–2, Deﬁnition 3 can involve
elements from two (possibly diﬀerent) vector spaces. We can
analogously derive the deﬁnitions of layer–signal and outer-
products  from  Deﬁnition  3.  The  transpose Θ𝑡 ∈ ℝ𝑎×𝑏
𝑚×𝑛  of  a
𝑛×𝑚 is deﬁned via (Θ𝑡)𝑗𝑘 = Θ𝑘𝑗 in analogy with
layer Θ ∈ ℝ𝑎×𝑏
that of a conventional matrix. With the deﬁnitions above, we
𝑚  by
can express the mapping of an 𝑚-channel image x ∈ ℝ𝑐×𝑑
𝑛×𝑚 with 𝑚 inputs  and 𝑛 outputs
a  convolution  layer Θ ∈ ℝ𝑎×𝑏
compactly as x ↦ Θx. Notice that because ﬁlters form a ring
(but not a ﬁeld) with respect to convolution, classical matrix
decompositions like the LU and the QR cannot be applied to
convolution layer Θ. However, a linear transform Θ = ST is

1.  Valid  convolution 𝑧 = 𝑥 ⋆ 𝑦 ∈ ℝ𝑎−𝑏+1 of 𝑥 ∈ ℝ𝑎 and 𝑦 ∈ ℝ𝑏 (when

𝑎 ≥ 𝑏) is given by  𝑧𝑗 = ∑ 𝑥𝑗+𝑖−1𝑦𝑖

 for 𝑗 = 1, . . . , 𝑎 − 𝑏 + 1.

𝑚
𝑖=1

4

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

𝜃2

υ1

𝐮1

𝛖2

𝐮2

(a)

𝜃2

𝜁2

𝜃2

𝜁2

(b)

(c)

(d)

(e)

𝜃1

𝜃1

𝜁1

𝜃1

𝜁1

Fig. 4. The KLT and the ELT. Elements θ1 and θ2 of columns θ of weight matrix Θ ∈ ℝ2×512, shown as dots in (a), are correlated with an underlying
 of γ = ∂y/∂θ (not shown) are correlated with covariance matrix Cγγ. The KLT
Gaussian distribution depicted by the level sets. Elements γ
1
Ut of θ is an orthogonal projection t = Utθ of θ onto u1 and u2, and induces  quantization cells that are square in the domain of θ (b) but parallel-
1 2⁄ θ (c). On the other hand, the ELT Ut is a biorthogonal projection of θ onto υ1 and υ2, and induces cells that are
ograms in the domain of ζ = Cγγ
parallelograms in the domain of θ (d) but square in the domain of ζ (e), minimizing distortion in the output domain.

 and γ
2

still well-deﬁned. In this work, we essentially transform all
convolutional mappings of the form x ↦ Θx to x ↦ STx and
𝑛×𝑚 depict
quantize S and T. See Fig. 1 (left), where Θ,  T ∈ ℝ2×2
𝑛×𝑛, a basis layer, which
2 × 2 convolution layers and S ∈ ℝ1×1
is equivalent to a 1 × 1 convolution layer.

4  QUANTIZATION OF CNNS

This work addresses the problem of compressing the weight
matrices of a CNN. We can express the end-to-end mapping
of an 𝐿-layer feed-forward CNN as

y = 𝑓(x|Θ1, . . . , Θ𝐿) = 𝑓𝐿( ⋅ ⋅ ⋅ 𝑓2(Θ2 𝑓1(Θ1x))),

(4)

𝑀  and y ∈ ℝ𝑐×𝑑

𝑁  are respectively the network
in which x ∈ ℝ𝑎×𝑏
input and output, and Θ𝑙=1,...,𝐿 are the 𝐿 convolutional and
fully-connecting weight matrices that parameterize 𝑓. Non-
linearities between convolutions, such as pooling, activation
(ReLU or tanh), and normalization have been absorbed into
functions 𝑓𝑙 together with biases. Although bias parameters
are also learnable such that they too must be quantized and
stored, they are suﬃciently few relative to weights, and their
impact on the quantized size of CNNs is negligible. When a
classiﬁcation CNN is being quantized, output y is assumed
to be the logits, that is, result prior to softmax activation.
  To give a concrete example, AlexNet [1] parameterizes 𝑓
using 𝐿 = 8 convolutional and fully-connecting weights, the
 represents a 3-color image with 224 × 224
input x ∈ ℝ224×224
1000 unnormalized log-probabilities
pixels, and output y ∈ ℝ1×1
of membership of input x across the 1000 predeﬁned classes
64×3  has
(tench, . . . , toilet paper). Convolution layer Θ1 ∈ ℝ11×11
64 × 3 convolutional  kernels  of  size 11 × 11,  while  the  last
fully-connected layer can be denoted Θ8 ∈ ℝ1×1

1000×4096.

3

to upper bound 𝑅max on the average quantization bit-depth
(quantization bit-rate) required to represent Θ1

𝑞 :
𝑞, . . . , Θ𝐿
2
minimize   𝐷(𝑅1, . . . , 𝑅𝐿) = 𝔼x∼𝑃 (x)‖ŷ − y‖2
subject to  𝑅(𝑅1, . . . , 𝑅𝐿) = ∑ 𝜇𝑙𝑅𝑙

≤ 𝑅max

(6)

𝐿
𝑙=1

[44], where the expectation is taken over the distribution of a
𝑞
training dataset, and 𝜇𝑙 denote the fraction of weights in Θ𝑙
over the total. We use distortion with mean-squared error as
a proxy for the true accuracy measure of interest such as the
top-1 classiﬁcation error, treating the CNN 𝑓 as a regression
model (in particular, we ﬁnd the top-1 accuracy metric to be
monotonic in mean-squared error). If we relax the inequality
constraint of (6), we obtain

minimize  𝐽 = 𝐷(𝑅1, . . . , 𝑅𝐿) + 𝜆𝑅(𝑅1, . . . , 𝑅𝐿),
in which 𝜆 decides the trade-oﬀ between rate and distortion
optimization criteria. Diﬀerentiating the objective of (7) with
respect to bit-depths 𝑅𝑙, we obtain the bit-depth–distortion
(or rate–distortion) optimality conditions

(7)

𝜆 = −

1
𝜇1

𝜕𝐷
𝜕𝑅1

= −

1
𝜇2

𝜕𝐷
𝜕𝑅2

= ⋅ ⋅ ⋅ = −

1
𝜇𝐿

𝜕𝐷
𝜕𝑅𝐿

(8)

cf. [75] so assuming one is allocating an inﬁnitesimal bit, the
optimal trade-oﬀ is reached when the decrease in the output
distortion from this inﬁnitesimal bit is equal for all layers.
  Optimality conditions (8) suggest a discrete approach for
solving problem (7). We ﬁrst generate a bit-depth–distortion
−1𝐷( . . . , 𝑅𝑙, . . . ) for each layer 𝑙, keeping the others
curve 𝜇𝑙
unquantized. Given some 𝜆, the Lagrangian-optimum value
−1𝐷(𝑅𝑙) + 𝜆𝑅𝑙. We show this
of 𝑅𝑙 is one which minimizes 𝜇𝑙
optimality condition geometrically in Fig. 2. This procedure
is discrete and requires no derivatives of 𝐽 to solve (7).

4.1  Layer-wise Quantization
The elements of weights Θ𝑙 are continuously-valued so that
they necessitate quantization for eﬃcient communication or
storage. In the simplest case, we can use uniform quantizers
on weights directly. Quantizing Θ𝑙 at a bit-depth of 𝑅𝑙 gives
𝑞 = 𝑞(Θ𝑙, 𝑅𝑙, Δ𝑙(𝑅𝑙)), where 𝑞(𝜃, 𝑅, Δ) = 0 if 𝑅 = 0 and
us Θ𝑙
𝑞(𝜃, 𝑅, Δ) = Δ clip(round(Δ−1𝜃) , −2𝑅−1, 2𝑅−1 − 1)

(5)

otherwise, where 𝑅𝑙 is a whole number of bits and Δ𝑙(𝑅𝑙) is
the optimum quantization step-size for a given 𝑅𝑙. Denoting
by ŷ = 𝑓(x|Θ𝑙=1,...,𝐿
) the output produced by the quantized
network, our CNN compression problem can be seen as one
2 across the distribution of y, subject
of minimizing 𝔼‖ŷ − y‖2

𝑞

4.2  Transform Quantization
Certain rows, columns or elements of the convolutional and
fully-connected weight matrices Θ𝑙 can have a larger impact
on output distortion when quantized. Allocating bit-depths
equally to all elements of Θ𝑙 may thus produce sub-optimal
rate-accuracy performance. More signiﬁcantly, there may be
statistical correlation among the elements of Θ𝑙. We can use
𝑡Θ𝑙, and
a decorrelating transform U𝑙
allocate bit-depths to transform elements T𝑙 to maximize the
quantizer’s performance. For simplicity, we assume that our
𝑡Θ𝑙) as opposed to row
transforms are column ones (T𝑙 = U𝑙
ones (T𝑙 = Θ𝑙U𝑙). To treat quantization statistically, it is also
convenient to regard the columns of Θ𝑙 as realizations of an

𝑡 on Θ𝑙 to obtain T𝑙 = U𝑙

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

5

n
o
i
t
r
o
t
s
i
D

0
1
g
o
L

ResNet-18

ResNet-50

)

%

(

y
c
a
r
u
c
c
a

1
-
p
o
T

ResNet-18

ResNet-50

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Fig. 6. Log10 output distortion (left plots) and top-1 accuracy (right plots) of Resnet-18 and 50 quantized with row (solid curves) and column (dotted
curves) variants of the KLT (blue curves) and the ELT (orange curves). All transforms have better rate–accuracy trade-offs than no transform (gray
curves), providing a rate saving of 1 bit across all rates. Bit-rates of the KLT and the ELT include bits spent on the transform matrices.

underlying random source θ𝑙, and columns of T𝑙 as those of
random source t𝑙 and assume each of the random sources is
jointly Gaussian. For brevity, we may omit the subscript 𝑙 of
marices Θ𝑙, T𝑙 and sources θ𝑙, t𝑙, and write Θ, T and θ, t. We
ﬁrst derive theoretical results for minimum distortion when
the random source θ is quantized without a transform, and
bit-depths assigned to the individual elements of θ.

)

%

(

d
a
e
h
r
e
v
O

Theorem 1: Minimum distortion without transform. Given
𝑛 , the minimum distortion
a jointly-Gaussian source θ ∈ ℝ𝑐×𝑑
𝐷 = 1
2 due to the quantization of θ at a suﬃciently
high quantization bit-rate (average bit-depth) 𝑅 is given by

𝑛 𝔼‖y − ŷ‖2

𝐷pcm = (∏ (C𝛾𝛾)𝑘𝑘(C𝜃𝜃)𝑘𝑘

𝑛
𝑘=1

)1 𝑛⁄ 𝜖22−2𝑅,

(9)

𝑛  and Γ = (𝜕y 𝜕θ⁄

in which C𝜃𝜃 and C𝛾𝛾 represent the cross-channel covariance
𝑛×𝑁  respectively, 𝑅
matrix  of θ ∈ ℝ𝑐×𝑑
is the average quantization bit-depth for the 𝑛 elements of θ
and 𝜖2 is a constant which depends on the quantization and
coding scheme used [76]. We give the proof in Appendix A.

) ∈ ℝ𝑐×𝑑

𝑛
𝑘=1

  Theorem 1 essentially states the output distortion due to
quantizing the elements of θ with optimal bit-depths for an
average of 𝑅 bits is identical to distortion due to quantizing
)1 𝑛⁄  at 𝑅
a Gaussian source of variance (∏ (C𝛾𝛾)𝑘𝑘(C𝜃𝜃)𝑘𝑘
bits. The exponential decay 2−2𝑅 comes from the halving of
the quantization step-size with each additional bit, reducing
output distortion by a factor of four. We now improve upon
the rate-distortion function (9) by transforming the elements
of θ prior to quantization. Suppose a transform U𝑡 ∈ ℝ1×1
𝑛×𝑛 is
ﬁrst applied on θ to produce coeﬃcients t = U𝑡θ, and t then
quantized. Quantization bit-depths 𝑅𝑘 are allocated now to
the elements of transform source t. Theorem 2 now derives
the minimum output distortion for transform quantization.

𝑛 𝔼‖y − ŷ‖2

Theorem 2: Minimum distortion with transform. Given the
𝑛 , the minimum output
same jointly Gaussian source θ ∈ ℝ𝑐×𝑑
distortion 𝐷 = 1
2 caused by the quantization of the
transform coeﬃcients t = U𝑡θ at suﬃciently high rates 𝑅 is
  𝐷tc = (∏ (U−1C𝛾𝛾U−𝑡)𝑘𝑘(U𝑡C𝜃𝜃U)𝑘𝑘
)1 𝑛⁄ 𝜖22−2𝑅   (10)
in which 𝐂𝛾𝛾 and 𝐂𝜃𝜃 are deﬁned identically as before, and
𝑅 is now the average quantization bit-depth allocated to the
𝑛 elements of t. We provide the proof in Appendix A.

𝑛
𝑘=1

  The ratio between the two distortions (9) and (10),

  𝐺 =

𝑛
𝑘=1

)1 𝑛⁄
(∏ (C𝛾𝛾)𝑘𝑘
𝑛
(∏ (U−1C𝛾𝛾U−𝑡)𝑘𝑘
𝑘=1

)1 𝑛⁄

𝑛
𝑘=1

)1 𝑛⁄
(∏ (C𝜃𝜃)𝑘𝑘
𝑛
(∏ (U𝑡C𝜃𝜃U)𝑘𝑘
𝑘=1

)1 𝑛⁄   (11)

is known as the coding gain [77] of transform U𝑡 (higher is

Layer number (𝑙)

Layer number (𝑙)

Fig. 5. ResNet-18 transform overheads as percentages of the number
of  elements  in Θl.  Row  (left)  and  column  (right)  transform  overheads
shown. Layers 7, 12, 17, and 20 are fully connected.

be:er). We expect quantization of t = U𝑡θ to produce a bit-
rate saving of 1
2 log2 𝐺 bits over that of the original θ source
for a given output distortion. The classical Karhunen–Loève
Transform (KLT) of θ (i.e. the matrix of eigenvectors of C𝜃𝜃)
is however sub-optimal with respect to 𝐺 since it maximizes
only the second gain term of (11). The optimal transform for
CNN quantization is now derived.

Theorem 3: Optimum transforms for CNNs. The transform
U𝑡 that minimizes output distortion 𝐷 = 1
2 caused
by the quantization of t = U𝑡θ, diagonalizes the matrix pair
(C𝜃𝜃, C𝛾𝛾

−1). That is,

𝑛 𝔼‖y − ŷ‖2

U𝑡C𝜃𝜃U = Λ  and  U𝑡C𝛾𝛾

−1U = I,

(12)

in which C𝜃𝜃 and C𝛾𝛾 represent the cross-channel covariance
matrix of θ and Γ respectively as previously, and Λ denotes
the nonnegative diagonal matrix of generalized eigenvalues
−1). In general, U−1 ≠ U𝑡 since U is not
of matrix pair (C𝜃𝜃, C𝛾𝛾
necessarily orthogonal. The proof is given in Appendix A.
  We refer to the optimal transform U𝑡 from Theorem 3 as
the End-to-end Learned Transform (ELT) of θ. The ELTs are
so-called since they simultaneously decorrelate the weights
θ and the partial derivatives 𝜕y 𝜕θ⁄
, which are derived from
the end-to-end mapping of x to output y = 𝑓(x|Θ1, . . . , Θ𝐿)
across all values of x. In practice, we can compute 𝜕y 𝜕θ⁄
 by
back-propagation using a small validation set. In Fig. 3, we
compare the coding gains of the KLT and the ELT across the
layers of ResNet-18. We see that the ELT produces a further
4 dB gain over the KLT. Both transforms were applied onto
the rows of the weight matrices.
  Fig. 4 (a–e) illustrate the diﬀerence between the KLT and
the ELT. Consider a simple multi-layer perceptron

𝑦 = 𝑓(x|Θ1, Θ2, . . . , Θ𝐿),
(13)
in which x ∈ ℝ𝑁 , and 𝑦 ∈ ℝ. Suppose now that elements 𝜃 of

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

6

)

%

(

s
w
o
r

o
r
e
z
-
n
o
N

ResNet-34 layer (𝑙)

ResNet-50 layer (𝑙)

Fig. 7. Percentages of non-zero rows of transformed weight matrices Tl at bit-rates R = 1.1 and 2.1 bits for ResNet-34 (left), and R = 1.1 and 3.1
bits for ResNet-50 (right). Percentages of non-zero rows at lower and higher bit-rates visualized as blue and blue + orange bars, respectively. See
Fig. 9 for retrained and non-retrained classification accuracies at these bit-rates.

opt, 𝑘 = 1, . . . , 𝑚

for 𝑅 = 0, . . . , 𝑀 do

Algorithm 1. Optimal Bit-depth Allocation
𝑚×𝑛, 𝜆, 𝐷𝑘, Δ𝑘, 𝑘 = 1, . . . , 𝑚
1  Input: Z ∈ ℝ𝑎×𝑏
opt, 𝑅𝑘
2  Output: Δ𝑘
3  for 𝑘 = 1, . . . , 𝑚 do
  𝐽 = ∞, 𝑅𝑘 = 0
4
5
6
7
8
9
10
11
12  end for

if 𝐽 > 𝐷𝑘(𝑅) + 𝜆𝑚𝑛𝑎𝑏𝑅 then
 𝐽 = 𝐷𝑘(𝑅) + 𝜆𝑚𝑛𝑎𝑏𝑅
 𝑅𝑘
 Δ𝑘
end if

opt = 𝑅
opt = Δ𝑘(𝑅)

end for

⁄
= 𝜕𝑦 𝜕θ𝑗

1 2⁄ (θ − θ𝑞)∥2

columns θ𝑗=1,...,512 ∈ ℝ2 of some Θ𝑙 ∈ ℝ2×512, shown as dots
in (a), are correlated, as are the elements 𝛾 of the derivatives
∈ ℝ2 for all 𝑗. We can visualize the mapping by
γ𝑗
the KLT U𝑡 of θ as an orthogonal projection of θ onto its two
principal axes 𝐮1 and 𝐮2. Quantizing the projected elements
t = U𝑡θ maps t to the centers of square cells (b). Noting that
2, the square cells
distortion can be wri:en as ∥C𝛾𝛾
1 2⁄ θ (c)  and
become  parallelograms  in  the  domain  of 𝜻 = C𝛾𝛾
incur larger distortion than square cells of the same area. On
the other hand, the ELT U𝑡 of θ is a biorthogonal projection
of θ onto nonorthogonal vectors 𝛖1 and 𝛖2 (a). Quantization
of t = U𝑡θ now maps t to the centers of parallelogram cells
(d). These parallelogram cells map to squares in the domain
2 as a result.
of 𝜻 (e), and minimizes distortion ∥C𝛾𝛾
  Fig. 6 (left) shows that the ELT (orange curves) produces
lower output distortion than the KLT (blue curves) for row-
(solid) and column- (do:ed) variants of the two transforms
in case where no retraining is performed. The classiﬁcation
accuracy associated with each distortion is graphed in Fig. 6
(right). We see that the KLT still provides good classiﬁcation
performance while being signiﬁcantly easier to construct as
it does not require the derivatives (𝜕y 𝜕θ⁄
). Row transforms
perform be:er than column ones, suggesting weights have a
larger correlation within rows than in columns. We relate the
KLT and the ELT to SVD and GSVD in Appendix B.

1 2⁄ (θ − θ𝑞)∥2

𝑛×𝑚. Again, suppose the former, and 𝑛 < 𝑚𝑎𝑏. In this
Θ ∈ ℝ𝑎×𝑏
case, overheads due to the transform are the 𝑛2 elements of
matrix S. If 𝑛 ≥ 𝑚𝑎𝑏, however, only the ﬁrst  𝑚𝑎𝑏 (non-zero)
rows of T need be stored, together with their corresponding
𝑚𝑎𝑏 columns of S. As a result, the total number of overheads
is min(𝑛2, (𝑚𝑎𝑏)2) relative  to  quantizing Θ directly  without
transform. We can analyze the row-transform case similarly.
  Fig. 5 plots the transform-quantization overheads for the
layers of ResNet-18 as percentages of the number of weights
in each one. We consider the overhead for both the row- and
the column-transformed cases. In both cases, the transforms
add overheads of roughly 10% of the number of weights. To
allocate bit-depths optimally to T and S at some given rate–
distortion trade-oﬀ 𝜆, we must satisfy optimality conditions
(8) on the rows of 𝐓, and columns of S. Bit-depth allocation
procedure for 𝐓 and S is given in Algorithm 1. Input Z can
be transform domain 𝐓, or (the transpose of) the basis S.
𝑛×𝑚 may
  At lower bit-rates, less signiﬁcant rows of T ∈ ℝ𝑎×𝑏
be quantized so heavily that only some ﬁrst 𝑘 < 𝑛 rows of T
are non-zero (column-ELT and column-KLT sort the rows of
T in a non-ascending order of variances). In this case, we can
evaluate the mapping x ↦ Θx eﬃciently in the transformed
𝑛×𝑘 and
domain via x ↦ S1:𝑘(T1:𝑘x), where matrices S1:𝑘 ∈ ℝ1×1
𝑘×𝑚 are the ﬁrst 𝑘 columns and the rows of S and 𝐓
T1:𝑘 ∈ ℝ𝑎×𝑏
respectively. Since the ﬁrst mapping x ↦ T1:𝑘x entails larger
𝑎 × 𝑏 convolutions whereas the second one z ↦ S1:𝑘z, 1 × 1
ones, we achieve a large inference speed-up when 𝑘 is small.
  One can express this inference speed-up as the ratio

𝐴 = (12𝑛𝑘 + 𝑎𝑏𝑚𝑘) (𝑎𝑏𝑚𝑛)
,

⁄

(14)

that is, the ratio of the number of multiplications in the map
x ↦ Θx to that in x ↦ S1:𝑘(T1:𝑘x). Typically, 𝑎𝑏𝑚 ≫ 12𝑛, so
the acceleration 𝐴 ≈ 𝑘/𝑛 may be understood as the fraction
of non-zero rows of Θ. In Fig. 7, we graph the percentage of
non-zero rows of ResNet-18 and ResNet-34 weight matrices
Θ at 1–2 bits, illustrating that signiﬁcant acceleration can be
obtained. Averaging (14) across all 𝐿 layers weighted by the
sizes of the input activations gives us the overall acceleration
in the number of ﬂoating-point operations (FLOPs).

4.3  Quantizing Transform Bases
Although the coding gain expression in (11) provides a good
indication of the expected rate savings due to transform, we
need to additionally count the bits spent on quantizing and
storing the inverse transform S = U−𝑡, required at inference
time, together with layer T to reconstruct the original layer
Θ. The overhead amount depends on whether we transform
the columns (T = U𝑡Θ) or the rows (T = ΘU) of the weights

5  OPTIMIZING QUANTIZATION

We now discuss optimal scalar quantization of the elements
of t = U𝑡θ. While vector [77] and dead-zone [78] quantizers
can further improve upon the rate–accuracy performance of
transform quantization, we opt to use simple uniform scalar
quantization to accelerate inference using integer arithmetic
directly on quantization indices.

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

7

n
o
i
t
r
o
t
s
i
d

0
1
g
o
L

𝐷out

𝐷src

𝑅 = 2

𝑅 = 4

𝑙 = 9

𝑅 = 8

𝑙 = 18

2

4

𝐷(𝑅)

6

Log2 step-size (Δ)

Log2 step-size (Δ)

Log2 step-size (Δ)

Log2 step-size (Δ)

Fig. 8. Weight and output distortions against quantization step-size Δ at bit-depths of R = 2 and 4 (left, shown for the first row-KLT element of layer
9 in ResNet-18). The step-size that minimizes the weight distortion Dsrc (orange lines) does not necessarily minimize the output distortion Dout and
incurs a 1–2-bit-rate loss compared with using the optimal quantization step-size for the output (right, shown for layers 9 and 18 of ResNet-18).

TABLE 1
Quantization times of different CNNs on Intel Xeon 6132
@ 2.60GHz + Nvidia Quadro RTX 8000

Model  Weights  Layers  Blocks  Steps  Maxbits  Perf.  Cost
7.0ms  1.6h
8
7.0ms  4.2h
8
7.1ms  7.5h
8
7.2ms  10.9h
8
7.6ms  13.1h
4

8
21
37
54
7,894k  121

AlexNet
ResNet-18
ResNet-34
ResNet-50
DenseNet-121

62,378k
11,679k
21,780k
25,503k

16
16
16
16
16

8
8
8
8
8

5.1  Finding Optimal Step-sizes
To ﬁnd the optimum quantization step-size Δ for a random
source t at a given bit-depth 𝑅, we can evaluate over a range
2 due  to  quantizing
of Δ,  output  distortion 𝐷out = 𝔼 ‖𝐲 − 𝐲̂‖2
source t𝑞(Δ), and ﬁnd a value of Δ that minimizes 𝐷out (the
number of quantization levels is ﬁxed at 2𝑅). Step-sizes that
minimize the distortion 𝐷src = 𝔼 ‖t − t𝑞‖2
2 of the source itself
deviate signiﬁcantly from the one which minimizes output
distortion 𝐷out. Fig. 8 (left) shows this for the KLT source t of
the ninth layer of ResNet-18. This discrepancy in step-sizes
results in a 1–2 bit-rate-loss (Fig. 8, right). The characteristic
shape-𝑉  curves in the right plots are a:ributed to an initial
decrease in overload distortion as step-size Δ increases, then
an increase in granular distortion past optimum Δ—see [77]
for further discussion on granular and overload distortions.
  Banner et al. [38] derived an expression to relate optimal
quantization step-sizes to the variance of the random source
in the Laplace-distributed case. However, Fig. 8 suggests the
quantization step-size should be optimized over the output
distortion explicitly using a grid search. This explicit search
also obviates the need to ﬁt a parametric distribution on the
underlying source, and is also applicable to quantizers with
dead-zones [78], and non-uniform cells [79, 80]. Algorithm 2
lists the procedure for optimal quantization step-size search
on T. Step-size searches on S is similar, but involves S𝑞 and
T instead of T𝑞 and S (being S𝑘 now the 𝑘th column of S).

5.2  Reducing Quantization Complexity

To maximize compression, one could allocate an individual
bit-depth to each row of T and each column of S. This can be
time-consuming for layers having many channels since one
needs to ﬁrst construct a bit-depth–distortion curve for each
row of T, and column of S. Each bit-depth–distortion curve
requires in turn computing the output distortion for a large
number of (bit-depth, step-size) pairs. To save time required
to construct these curves, we therefore partition T (resp. S)
into 𝐵 blocks of rows (resp. columns), and allocate instead a

for 𝑅 = 1, . . . , 𝑀  do
  𝐷𝑘(𝑅) = ∞, Δ𝑘(𝑅) = 0
for Δ = 20, 21, 22, . . .  do
  T𝑞 = T  /* Initialize with unquantized weights */
/* T𝑘 is the 𝑘th row of T */
  T𝑘
  ŷ = 𝑓(x|Θ1, . . . ,ST𝑞, . . . , Θ𝐿)

𝑞 = 𝑞(T𝑘, 𝑅, Δ)

𝑛×𝑛, T ∈ ℝ𝑐×𝑑

Algorithm 2. Optimal Step-size Search
𝑛×𝑚
1  Input: S ∈ ℝ1×1
2  Output: Δ𝑘, 𝐷𝑘, 𝑘 = 1, . . . , 𝑛
3  for 𝑘 = 1, . . . , 𝑛 do
4
5
6
7
8
9
10
11
12
13
14
15
16  end for

2 then
if 𝐷𝑘(𝑅) > 𝔼‖y − ŷ‖2
2
  𝐷𝑘(𝑅) = 𝔼‖y − ŷ‖2
  Δ𝑘(𝑅) = Δ
end if
end for

end for

single bit-depth to each block. This has very li:le impact on
rate–distortion performance if the number of blocks is large
enough—the  output  variance  of  elements  of 𝐓 (resp. S)  is
monotonic-decreasing across the rows (resp. columns), and
the output variances roughly the same within each block. If
the blocks can be allocated a maximum bit-depth of 𝑀, then
time spent on constructing bit-depth–distortion curves of all
layers is proportional to 𝐵𝑆𝐼𝑀𝑃𝐿, where 𝑆 is the number of
quantization step-sizes searched, 𝐼, number of images used
to generate the bit-depth–distortion curves, 𝑃 , performance
of a given CNN in seconds, and 𝐿 the number of layers. The
typical parameters and associated times for optimizing bit-
depth are shown in Table 1 for several networks.

5.3  Fine-tuning Quantized Weights
Whereas ﬁne-tuning of the quantized networks is not always
possible due to lack of suitable training data at compression
time, we demonstrate that optionally ﬁne-tuning transform-
quantized CNNs can restore accuracies close to the original
ones. To re-train the transform-quantized networks, we use
the straight-through estimator (STE) approach of Hubara et
al. [31, 41] to quantize the weights during the forward-pass
according to the assigned bit-depths, and let their gradients
pass through with no change during the backward pass. We
plot in Fig. 9 the bit-rate–accuracy curves of ResNets on the
ImageNet [81] validation set with and without retraining on
the training set. The classiﬁcation accuracies can be restored
close to the original ones at 2 bits, and almost losslessly at 3
bits. All models were retrained for 3 epochs maximum with

8

)

%

(

y
c
a
r
u
c
c
a

1
-
p
o
T

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

AlexNet

ResNet-18

ResNet-34

ResNet-50

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Fig. 9. Rate–accuracy curves of transform-quantized AlexNet and ResNets on the ImageNet validation set, with retraining (blue lines), and without
retraining (orange lines). Unquantized baselines shown as gray lines. All CNNs retrained on the training set for 3 epochs maximum. Shown for the
row-KLT case. Retrained row-ELT results are similar (no distinction exists between the KLT and the ELT after retraining).

TABLE 2
Classiﬁcation accuracies of CNN models compressed using transform quantization and other methods.

Methods

Train
epochs

Comp
ratio

Wgt/Act  Classiﬁcation accuracy
bit-rate  Top-1 (%)  Top-5 (%)

Methods

Train
epochs

Comp
ratio

Wgt/Act  Classiﬁcation accuracy
bit-rate  Top-1 (%)  Top-5 (%)

Full-precision
BWN [28]
TWN [29]
TTQ [30]
INQ [36]
INQ [36]
INQ [36]
INQ [36]
LQ-Nets [37]
LQ-Nets [37]
LQ-Nets [37]
DSQ [40]
DFQ [43]
Ours (row-ELT)
Ours (row-ELT)
Ours (row-KLT)
Ours (row-KLT)
Ours + retrain
Ours + retrain
Ours + retrain
Ours + retrain

Full-precision
L-DNQ [39]
HAQ [46]
HAQ [46]
Ours (row-ELT)
Ours (row-ELT)
Ours (row-KLT)
Ours (row-KLT)
Ours + retrain
Ours + retrain
Ours + retrain
Ours + retrain

–
16
50
160
8
8
8
8
120
120
120
90
0
0
0
0
0
3
3
3
3

–
–
100
100
0
0
0
0
3
3
3
3

ResNet-18
–
32.0×
16.0×
16.0×
16.0×
10.7×
8.0×
6.4×
16.0×
10.7×
8.0×
32.0×
5.3×
10.7×
8.2×
10.7×
8.2×
32.0×
22.9×
16.8×
10.7×

32/32
1/32
2/32
2/32
2/32
3/32
4/32
5/32
2/32
3/32
4/32
1/32
6/32
3.0/32
3.9/32
3.0/32
3.9/32
1.0/32
1.4/32
1.9/32
3.0/32

ResNet-34
–
10.7×
15.2×
10.7×
11.9×
8.4×
11.4×
8.4×
29.1×
22.9×
15.2×
11.9×

32/32
3/32
2.1/32
3.0/32
2.7/32
3.8/32
2.8/32
4.0/32
1.1/32
1.4/32
2.1/32
2.8/32

69.7 (+0.0)  89.2 (+0.0)
60.8 (–8.9)  83.0 (–6.2)
65.3 (–4.4)  86.2 (–3.0)
66.6 (–3.1)  87.2 (–2.0)
66.0 (–3.7)  87.1 (–2.1)
68.1 (–1.6)  88.4 (–0.8)
68.9 (–0.8)  89.0 (–0.2)
69.0 (–0.7)  89.1 (–0.1)
68.0 (–1.7)  88.0 (–1.2)
69.3 (–0.4)  88.8 (–0.4)
70.0 (+0.3)  89.1 (–0.1)
63.7 (–6.0)
66.3 (–3.4)
67.9 (–1.8)  88.1 (–1.1)
68.6 (–1.1)  88.5 (–0.7)
67.2 (–2.5)  87.8 (–1.4)
68.5 (–1.2)  88.4 (–0.8)
64.5 (–5.2)  86.4 (–2.8)
67.2 (–2.5)  87.8 (–1.4)
68.2 (–1.5)  88.4 (–0.8)
69.8 (+0.1)  89.3 (+0.1)

–
–

73.3 (+0.0)  91.3 (+0.0)
44.0 (–29.)  72.9 (–18.)
71.5 (–1.8)  90.1 (–1.2)
73.2 (–0.1)  91.3 (+0.0)
71.5 (–1.8)  90.3 (–1.0)
72.6 (–0.7)  90.9 (–0.4)
71.0 (–2.3)  90.2 (–1.1)
72.4 (–0.9)  90.9 (–0.4)
69.6 (–3.7)  88.9 (–2.4)
71.4 (–1.9)  89.7 (–1.6)
72.8 (–0.5)  90.6 (–0.7)
73.0 (–0.3)  90.8 (–0.5)

Full-precision
INQ [36]
LQ-Nets [37]
LQ-Nets [37]
ABGD [23]
ABGD [23]
HAQ [46]
HAQ [46]
Ours (row-ELT)
Ours (row-ELT)
Ours (row-KLT)
Ours (row-KLT)
Ours + retrain
Ours + retrain
Ours + retrain
Ours + retrain

Full-precision
BWN [28]
DoReFa [42]
TWN [29]
TTQ [30]
INQ [36]
LQ-Nets [37]
Ours (row-ELT)
Ours (row-ELT)
Ours (row-KLT)
Ours (row-KLT)
Ours + retrain
Ours + retrain

Full-precision
Ours (row-KLT)
Ours (row-KLT)

–
8
120
120
9
9
100
100
0
0
0
0
3
3
3
3

–
58
200
50
160
8
120
0
0
0
0
3
3

–
0
0

ResNet-50
–
6.4×
16.0×
8.0×
32.0×
18.8×
10.6×
8.0×
11.4×
8.4×
10.3×
7.8×
29.1×
21.3×
16.8×
11.4×

32/32
5/32
2/32
4/32
1.0/32
1.7/32
3.0/32
4.0/32
2.8/32
3.8/32
3.1/32
4.1/32
1.1/32
1.5/32
1.9/32
3.1/32

AlexNet
–
32.0×
32.0×
16.0×
16.0×
6.4×
16.0×
32.0×
16.0×
32.0×
16.0×
64.0×
32.0×
DenseNet-121

32/32
1/32
1/32
2/32
2/32
5/32
2/32
1.0/32
2.0/32
1.0/32
2.0/32
0.5/32
1.0/32

–
–

76.0 (+0.0)  93.0 (+0.0)
74.8 (–1.2)  92.4 (–0.6)
75.1 (–0.9)  92.3 (–0.7)
76.4 (+0.4)  93.1 (+0.1)
68.2 (–7.8)
73.8 (–2.2)
75.3 (–0.7)  92.5 (–0.5)
76.1 (+0.1)  92.9 (–0.1)
73.6 (–2.4)  91.7 (–1.3)
74.7 (–1.1)  92.4 (–0.6)
73.6 (–2.4)  91.7 (–1.3)
74.8 (–1.2)  92.3 (–0.7)
72.9 (–3.1)  91.4 (–1.6)
74.2 (–1.8)  92.2 (–0.8)
75.2 (–0.8)  92.6 (–0.4)
76.0 (+0.0)  93.0 (+0.0)

55.7 (+0.0)  78.6 (+0.0)
56.8 (+1.1)  79.4 (+0.8)
53.9 (–1.8)  76.3 (–2.3)
54.5 (–1.2)  76.8 (–1.8)
57.5 (+1.8)  79.7 (+1.1)
57.4 (+1.7)  80.5 (+1.9)
60.5 (+4.8)  82.7 (+4.1)
53.4 (–2.3)  77.1 (–1.5)
55.1 (–0.6)  78.2 (–0.4)
53.1 (–2.6)  77.0 (–1.6)
55.0 (–0.7)  78.2 (–0.4)
53.0 (–2.7)  77.0 (–1.6)
55.3 (–0.4)  78.5 (–0.1)

–
8.0×
6.4×

32/32
4.0/32
5.0/32

75.0 (+0.0)  92.3 (+0.0)
72.6 (–2.4)  91.1 (–1.2)
73.7 (–1.3)  91.7 (–0.6)

SGD, and the actual number of iterations optimized using a
grid search to achieve minimum validation error. Note that
transform bases S are also retrained so there is no diﬀerence
between the KLT and the ELT cases after retraining.

6  EXPERIMENTAL RESULTS

and non-retrained scenarios. We show transform-quantized
CNNs advance the state of the art in both scenarios. For fair
comparisons, we compare with other results that do not use
entropy coding, e.g. Huﬀman [20] or arithmetic [45]. We can
always apply standard entropy (lossless) coding to any of the
quantized CNNs for a further ~30% reduction in bit-rates.

To examine the rate–distortion and rate–accuracy behaviors
of transform-quantized networks, we compress a number of
popular pretrained image classiﬁcation networks—AlexNet
[1], ResNets [60], and DenseNets [61]—as well as pretrained
image superresolution network EDSR [63], in both retrained

Image classiﬁcation accuracy. Table 2 shows the accuracies
of transform-quantized AlexNet, ResNets and DenseNets on
ImageNet [81] (pretrained PyTorch versions) at 1–3 bits. The
accuracies are evaluated using the ImageNet2012 validation
set consisting of 50k images. Our CNNs are quantized using

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

9

)
B
d
(
R
N
S
P
d
e
s
i
o
n
e
D

15

25
35

55
75
95

y
t
i
r
a
l
i

m
S

i

d
e
s
i
o
n
e
D

15

25
35

55
75
95

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Bit-rate (bits per weight)

Fig. 10. Average PSNR and SSIM of denoised Set12 images  for noise  variances  15,  25, 35,  55, 75, and 95,  produced  by transform-quantized
DRUNet [62] at different bit-rates. Denoising performance of DRUNet starts to drop below 2 bits per weight.

TABLE 3
Acceleration of ResNet-50 due to zero-quantization
(row-ELT) or pruning (others) of convolution kernels

TABLE 5
PSNR (dB) of  2–4× upsampled images using
transform-quantized EDSR (row-KLT w/o retraining)

Method

Accuracy (%)
Top-1 (Δ%)  Top-5 (Δ%)

Bit-
rate

FLOP
ratio

Compres-
sion ratio

–

76.1 (–0.0)  92.9 (–0.0)
Full-precision
74.6 (–1.5)  92.1 (–0.8)
SoftFP [8]
75.2 (–0.9)
NISP [19]
74.8 (–1.3)  92.3 (–0.6)
FPGM [9]
75.0 (–1.1)  92.3 (–0.6)
DCP [14]
71.9 (–3.2)  90.7 (–1.6)
GDP [13]
75.2 (–0.7)  92.4 (–0.3)
GBN-50 [12]
76.2 (+0.3)  92.8 (+0.2)
GBN-60 [12]
71.0 (–1.9)  90.0 (–1.1)
ThiNet-50 [10]
ThiNet-70 [10]
72.0 (–0.8)  90.7 (–0.5)
Ours + retraining  72.9 (–3.1)  91.4 (–1.6)
Ours + retraining  76.0 (–0.1)  93.0 (+0.1)

32.0  100.0%
58.2%
32.0
56.0%
32.0
46.5%
32.0
44.2%
32.0
48.7%
32.0
44.9%
32.0
59.5%
32.0
44.2%
32.0
63.3%
32.0
65.3%
1.1
88.6%
2.8

1.0×
1.7×
1.8×
2.2×
2.3×
2.1×
2.2×
1.7×
2.3×
1.6×
29.4×
11.4×

TABLE 4
Acceleration of transform-quantized (row-KLT)
MobileNet-v2 on Google TPU and MIT Eyeriss

Methods

Train
epochs

Comp
ratio

Top-1
Accuracy

Inference rate
TPU

Eyeriss

Set5

B100

Set14

Dataset

Basis
[49]

Basis
[49]

3-bits
(ours)

1-bits
(ours)

2-bits
(ours)

EDSR
[63]

Factor
[55]

4-bits
(ours)
2×  38.19  37.95  38.09  38.12  36.81  38.10  38.25  38.27
3×  34.68  34.33  34.47  34.55  32.19  34.34  34.63  34.74
4×  32.48  32.05  32.29  32.39  30.31  32.28  32.51  32.60
2×  33.95  33.53  33.75  33.72  32.73  33.74  33.93  34.00
3×  30.53  30.31  30.41  30.46  29.09  30.39  30.55  30.63
4×  28.81  28.54  28.63  28.69  27.49  28.74  28.87  28.93
2×  32.35  32.15  32.23  32.27  31.47  32.21  32.35  32.37
3×  29.26  29.08  29.15  29.18  28.19  29.13  29.26  29.32
4×  27.72  27.55  27.62  27.64  26.85  27.66  27.74  27.79
2×  32.97  31.99  32.38  32.46  30.12  32.51  32.96  33.05
Urban100  3×  28.81  28.10  28.39  28.51  26.13  28.34  28.76  28.94
4×  26.65  25.98  26.25  26.36  24.67  26.38  26.65  26.81
2×  34.60  34.60  34.77  34.84  33.43  34.79  35.03  35.08
3×  30.91  30.91  31.06  31.11  29.29  30.97  31.23  31.34
4×  28.92  28.92  29.06  29.13  27.65  29.07  29.27  29.35
 1180k    136k    90k    164k  1180k   1180k   1180k   1180k
 11.5%    7.6%   13.9%   3.1%     6.3%    9.4%    12.5%

Parameters
Compression

DIV2K

–

Full-precision
HAQ
HAQ
Ours + retrain
Ours + retrain
Ours + retrain
Ours + retrain
Ours + retrain

–
30
30
30
30
30
30
30

MobileNet-v2

–
0.6
0.4

71.1 (+0.0)
71.2 (+0.1)
68.9 (–2.2)
7.3 bits  71.3 (+0.2)
7.0 bits  71.0 (–0.1)
6.4 bits  70.9 (–0.2)
6.1 bits  67.8 (–3.3)
5.5 bits  64.8 (–6.3)

1504 (1.00)
  64 (1.00)
2067 (1.37)  124 (1.94)
2197 (1.46)  128 (2.00)
2197 (1.46)  127 (1.98)
2207 (1.47)  128 (2.00)
2256 (1.50)  130 (2.03)
2336 (1.55)  133 (2.08)
2407 (1.60)  136 (2.13)

acceleration at bit-rates 𝑅 = 1.1 and 3.1 bits, along with the
results from other pruning methods. While our FLOP counts
are higher than those of specialized pruning techniques, our
FLOPs require much lower bit-depths. Therefore, we may be
able to achieve further acceleration if specialized hardware
can be designed to facilitate low-bit-depth arithmetic. Fig. 7
provides a per-layer breaks-down of the speedup. Numbers
in bold indicate the best result in each column.

row-ELT and row-KLT. For reference, we include the results
of DFQ [43], LQ-Nets [37], INQ [36], ABGD [23] DoReFaNet
[42] and HAQ [46]. We see that our non-retrained ResNet-18
results are signiﬁcantly be:er than those for the DFQ (data-
free quantization) method [43]. In the case where retraining
is performed, row-KLT ResNets have a considerably higher
accuracy than HAQ at low bits (ResNet-34, 50), and slightly
more accurate overall than LQ-Nets (ResNet-18, 50) but with
3 epochs of refining. LQ-Nets also requires the bit-depths to
be determined prior to training the model while we are able
to quantize and refine the models at arbitrary bit-rates after
training. Note that our pretrained AlexNet model is smaller
and has a lower unquantized baseline than the others. Bold
numbers indicate results on the rate–top-1 frontier.

Pruning eﬀect of quantization. We show acceleration due to
zero quantization (pruning) of less signiﬁcant kernels at low
bit-rates (1–3 bits). Table 3 shows for ResNet-50 the overall

Acceleration on H/W. We measure speed up from transform
quantization on high-performance DNN-targeted hardware
accelerators Google TPU [82] and MIT Eyeriss [83], adopting
SCALE-sim [84] to simulate the time cycles of MobileNet-v2
quantized using our approach or using HAQ [46]. Note that
the convolutional blocks of MobileNet-v2 are already in the
2D transform domain (Section 7) so we optimally assign bit-
depths to weights and quantize them via Algorithms 1–2. In
both HAQ and our approach, we fetch quantized weights to
on-chip memory from oﬀ-chip, where they are dequantized
and fed into processing units. Oﬀ-chip memory is accessed
in tandem while convolutions are being performed. In this
experiment, we also quantize all intermediate activations in
a layer-wise fashion for a fairer comparison with HAQ. Our
bit-rates are average quantization bit-depths across weights
and activations, assuming the batch size of one. We provide
in Table 4, the inference rates (in images per second) of our
quantized MobileNet-v2 at diﬀerent bit-rates, and compare

10

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

7
0
-
2
1
t
e
S

5
0
-
2
1
t
e
S

1
1
-
2
1
t
e
S

9
0
-
2
1
t
e
S

0
1
-
2
1
t
e
S

Ground truth

Noisy (17.24dB / 0.3449)  0.5 bits (27.85dB / 0.8297)  1 bits (28.10dB / 0.8315)

2 bits (28.23dB / 0.8345)

Ground truth

Noisy (17.28 dB / 0.4071)  0.5 bits (28.39dB / 0.8808)  1 bits (28.69dB / 0.8906)

2 bits (28.86dB / 0.8930)

Ground truth

Noisy (17.23 dB / 0.3257)  0.5 bits (28.52 dB / 0.7433)  1 bits (28.71dB / 0.7452)

2 bits (28.79dB / 0.7419)

Ground truth

Noisy (17.23 dB / 0.2489)  0.5 bits (27.48 dB / 0.8076)  1 bits (28.72 dB / 0.8490)  2 bits (29.40 dB / 0.8615)

Ground truth

Noisy (17.25 dB / 0.3540)  0.5 bits (28.52 dB / 0.7605)  1 bits (28.82 dB / 0.7703)  2 bits (28.96 dB / 0.7791)

Fig. 11. Visual comparison of denoised Set12 images (noise variance is 35). Denoised images are from row-KLT quantized DRUNet [62] at 0.5, 1.0
and 2.0 bits. PSNR and SSIM in brackets are with respect to ground truth. Images denoised at 2 bits are indistinguishable to the full-precision ones
(not shown). Images denoised at 0.5 bits surfer from staircase artifacts. Best viewed online.

them with those of HAQ. Performance of the two methods
are comparable with transform quantization obtaining 2197
and 127 inference rate on TPU and Eyeriss, respectively, with
71.3% top-1 accuracy, while for HAQ they are 2067 and 124
respectively, with 71.2% top-1 accuracy (these are shown in
bold). Quantized networks are re-trained on the ImageNet
training dataset for 30 epochs.

Quantizing image denoising network (DRUNet). Variants
of U-Net have recently been applied to image denoising. We
apply row-KLT quantization to the state-of-the-art DRUNet
[62] to study the inﬂuence of quantization on the denoising
performance. We corrupt images by additive Gaussian noise
of variance from 15 to 95, and denoise the corrupted images
using quantized DRUNets. In Fig. 10, we plot the PSNR and

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

11

Ground truth

Factor [55]: 25.86 dB

Basis-S [49]: 25.94 dB

Basis [49]: 25.96 dB

EDSR [63]: 26.45 dB

Nearest: 22.87 dB

Bilinear: 23.26 dB

1-bit (ours): 26.00 dB

2-bits (ours): 26.53 dB

4-bits (ours): 26.53 dB

Ground truth

EDSR [63]: 35.27 dB

Basis [49]: 35.10 dB

2-bits (ours): 35.37 dB

4-bits (ours): 35.83 dB

Ground truth

EDSR [63]: 32.69 dB

Basis [49]: 32.68 dB

2-bits (ours): 32.67 dB

4-bits (ours): 32.77 dB

×
4
a
r
a
b
r
a
B

×
4
n
a
c
i
l
e
P

×
4
a
n
e
L

×
4
2
0
0
2

t
n

i
o
P
r
e
w
o
P

Ground truth

EDSR [63]: 27.17 dB

Basis [49]: 27.01 dB

2-bits (ours): 26.38 dB

4-bits (ours): 27.10 dB

Fig.  12.  Visual  comparison  of  4× upsampled  images  produced  by  transform-quantized  EDSR  [63]  (with  retraining).  We  additionally  show  the
upsampled images from Factor [55], Basis [49], and B-spline interpolations for reference. Upsampled images produced by our row-KLT-quantized
EDSR at 2–3 bits are visually identical to those of unquantized EDSR. Results for Factor and Basis are taken from [49]. Best viewed online.

SSIM of the denoised Set12 images against the ground truth
across quantization bit-rates and noise variance. We see that
PSNR and SSIM of the denoised image start to degrade once
quantization rate drops below 2 bits. Fig. 11 visualizes select
denoised outputs at the network quantization rates of 0.5, 1.0
and 2.0 bits, together with the noisy input for noise variance
35. We see that KLT-quantized DRUNet (without retraining)
has good denoising performance even at a very low bit-rate
(0.5 bits). Full precision results are similar to the 2 bit ones.

Quantizing super-resolution networks. We apply row-KLT
quantization to EDSR [63] to demonstrate the applicability
of our framework to image super-resolution. The pretrained
model from [63] is quantized and tested on DIV2K [85], Set5
[86], Set14 [87], B100 [88] and Urban100 [89] datasets. We list
the PSNR of the upsampled images in Table 5 together with
those from baseline methods, Factor [56], and Basis [49], for
comparison.  Even  without  retraining,  transform-quantized
EDSR outperforms baseline methods (requiring training) in

12

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

. . .

θ11
θ12
θ21 θ22

.

.

.

...

u1  u2  . . .   u𝑛

→

. . .

t11
t12
t21 t22

.

.

.

...

Θ ∈ ℝ2×2

𝑚×𝑛

U ∈ ℝ𝑚×𝑚

T ∈ ℝ2×2

𝑚×𝑛

𝑡
v1
𝑡
v2

.

.

.

𝑡
v𝑚
V𝑡 ∈ ℝ𝑛×𝑛

Fig. 13. 2D Transform of Θ. The kernels Θ are now decorrelated in both
the row and the column spaces to produce a sparser matrix T at lower
quantization rates. White blocks indicate zero-quantized regions.

TABLE 6
Intra-kernel transform coding gains (dB) for AlexNet.
Gradient, weight and total (in bold) gains shown.

𝑙

Intra-kernel transform quantization

DCT-I

DCT-II

KLT

ELT

Inter-
KLT  ELT

AlexNet (CaﬀeNet)
1  14.1  5.6  19.6  14.0  5.0 19.0  11.0  5.9  16.9  14.0  5.8  19.8  4.7  6.0
4.3  2.6  6.9  4.5  1.5  5.9  3.1  3.1  6.2  4.7  2.9  7.6  6.3  7.5
2
2.9  2.1  5.1  3.0  1.6  4.6  2.5  2.1  4.6  3.1  2.1  5.2  3.7  5.1
3
2.3  1.4  3.7  2.3  1.2  3.5  2.0  1.5  3.5  2.4  1.5  3.9  1.6  3.0
4
2.0  2.1  4.1  2.0  1.9  3.9  1.9  2.2  4.1  2.1  2.1  4.2  1.7  3.3
5

PSNR and compression ratio. We note that our unquantized
baseline is li:le higher (0.1 dB) than those of [49, 56]. Fig. 12
provides a visual comparison among images upsampled by
quantized models. Images from transform-quantized EDSR
at low bit-rates are very similar to those of the baseline. The
bolded numbers indicate the best result in each row.

7  DISCUSSION

Transform quantization may be extended in directions that
are not explored in this work. We now discuss each of these
extensions, together with possible limitations of our work.

7.1  Extension to 2D Transform
In this work, we decorrelated weight matrices Θ only across
their rows. One may wonder if a 2D transform T = U𝑡ΘV in
both rows and columns of Θ can provide be:er compression
at lower bit-rates. We illustrate this in Fig. 13. Unfortunately
for compression, we ﬁnd that additional storage overheads
incurred from the column transform basis outweigh the bit-
savings obtained from a sparser T (this is especially the case
since column transforms do not work as well as row ones—
refer to Fig. 6. If the quantized and stored size of the CNNs
is not an issue, 2D transforms can still be useful for pruning
to reduce the number of convolutions performed. In fact, we
can interpret the MobileNet-v2 blocks as having been trained
in the 2D transform domain with diagonal T imposed.

7.2  Extension to Intra-kernel Transform
Correlation may also be observed between weights inside a
kernel, and one can alternatively transform weight matrices
by  decorrelating  weights  within  each  kernel  (intra-kernel)
rather than across kernels (inter-kernel). Often, intra-kernel
transforms can produce larger coding gains than their inter-
kernel counterparts. However, certain CNN models such as
AlexNet and VGG can contain signiﬁcant numbers of 1 × 1
convolutional or fully connected layers, so the overall utility
of intra-kernel transforms is negligible for such CNNs.

In  Table  6,  we  provide  the  intra-kernel  coding  gains  of
diﬀerent transforms on the convolutional layers of AlexNet

(layers 1–5). All convolutional layers contain kernels 3 × 3 in
dimensions, with the exception of the ﬁrst (11 × 11) and the
second (5 × 5) layers. For intra-ELT and intra-KLT, we use a
separate transform for each row of the weight matrices for
improved  decorrelation.  The  coding  gains  of  the  intra-ELT
are up to 5 dB higher than those of DCT-II used by the CNN
quantization methods in [24, 26]. However, the performance
of DCT-I is already very similar to that of weight-dependent
KLT and ELT, which, unlike the DCT-I, do not have eﬃcient
bu:erﬂy algorithms available.

7.3  Limitations and Future Work
Storage overheads incurred by transform basis matrices can
be reduced if the transforms could be shared across multiple
layers, similarly to the shared ﬁlter basis idea [45, 49]. In our
post-training quantization case, however, shared transforms
are not useful since the rows or columns of the learnt weight
matrices are ordered arbitrarily—transforms that work well
on one weight matrix may even yield negative coding gains
if applied on diﬀerent weight matrices. Nevertheless, shared
transforms may provide further coding gains if we can train
models from scratch to enforce the same order of rows and
columns across multiple weight matrices.
  One potential limitation of this work is that quantization
introduces a signiﬁcant loss in classiﬁcation accuracies if we
do not subsequently ﬁne-tune the CNN. However, loss due
to quantization is far from unique to this work—to the best
of our knowledge, CNN quantization methods with smaller
accuracy losses involve some form of training, whether it be
from scratch or post-quantization. An important theoretical
future work may be to investigate the reasons for such a loss
in performance when weights are not retrained. Combining
quantization with network architecture search similar to [90]
may be another fruitful research direction.

8  CONCLUSION

This work proposes a transform-quantization framework to
compress CNN weights, post-training. As suggested by the
name, our framework transforms weights before quantizing
them to signiﬁcantly improve compression in both retrained
and non-retrained quantization scenarios. We optimize both
components of our framework (transform and quantization)
by forming CNN compression as a rate–distortion problem
and optimizing its object with respect to the transform, and
bit-depths assigned to transform weights and bases. Solving
this optimization problem also reveals that the classical KLT
has a similar (but not identical) quantization performance as
the optimum end-to-end learned transform (ELT) we derive
in this paper. For either transform, optimum bit-depths are
obtained by minimizing the distortion in the CNN output as
opposed to that of the weights themselves. Transform basis
layers are quantized similarly to transform domain layers.
  The post-training quantization paradigm adopted by our
framework also provides the ﬂexibility to compress models
at arbitrary bit-rates, obviates the need to train models again
from scratch, and is straight-forward to implement. Despite
the simplicity of our framework, it advances the state of the
art in CNN compression for a number of CNN models. We
believe that our transform-quantization framework will also
be useful for other CNNs not speciﬁcally mentioned here.

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

13

APPENDIX A  PROOFS OF THEOREMS

A.1  Proof of Theorem 1
Proof. If we express Θ𝑞 = Θ + dΘ for the quantized version
of a weight matrix Θ ∈ ℝ𝑎×𝑏

𝑛×𝑚, we have for small dΘ

Inequality (a) is obtained with equality if we set U to the
matrix of eigenvectors of C𝛾𝛾C𝜃𝜃. Writing Λ for the diagonal
matrix of eigenvalues 𝜆𝑘(C𝛾𝛾C𝜃𝜃), we obtain (12) by writing
the eigen-decomposition U−1(C𝛾𝛾C𝜃𝜃)U = Λ as generalized
∎
eigenvalue decomposition of matrix pair (C𝜃𝜃, C𝛾𝛾

−1).

2

 𝐷 = 1
(a) 1

  ≈
  =(b) 1
  =(c) 1
(d)
  ≥

𝑛 𝔼‖𝑓(x| . . . , Θ𝑙−1, Θ𝑞, Θ𝑙+1, . . . ) − y‖2
𝑚
)𝑡dθ𝑗
𝑛 𝔼‖𝑓(x|Θ)   +   ∑ (𝜕𝑓(x|Θ) 𝜕θ𝑗
𝑗=1
2
)𝑡dθ𝑗‖2

⁄

⁄

𝑛 ∑ 𝔼‖(𝜕y 𝜕θ𝑗
𝑛 ∑ (C𝛾𝛾)𝑘𝑘(C𝜃𝜃)𝑘𝑘𝜖22−2𝑅𝑘
(∏ (C𝛾𝛾)𝑘𝑘(C𝜃𝜃)𝑘𝑘

𝑛
𝑘=1
𝑛
𝑘=1

)1 𝑛⁄ 𝜖22−2𝑅

𝑚
𝑗=1

2
− y‖2

(15)

in which (a) follows from ﬁrst-order Taylor’s approximation
of 𝑓(x| . . . ,Θ + dΘ, . . . ) at Θ, (b) follows from the deﬁnition
y = 𝑓(x| . . . ,Θ, . . . ) and the fact that gradients 𝜕𝑓(x|Θ) 𝜕θ𝑗
are orthogonal. Equality (c) follows from the deﬁnitions of
𝑚
)𝑡
⁄
the covariance matrices C𝛾𝛾 = ∑ (𝜕y 𝜕θ𝑗
)(𝜕y 𝜕θ𝑗
, and
𝑗=1
C𝜃𝜃 = 1
22−2𝑅𝑘 and
, and the fact that 𝔼(d𝜃𝑘)2 = 𝔼𝜃𝑘
𝔼d𝜃𝑘′d𝜃𝑘 = 0, 𝑘′ ≠ 𝑘. Finally, inequality (d) is obtained with
equality for 𝑅 = 1
 by choosing 𝑅𝑘 such that all the
individual distortions (C𝛾𝛾)𝑘𝑘(C𝜃𝜃)𝑘𝑘𝜖22−2𝑅𝑘 are equal.
∎

𝑚
𝑡
𝑚 ∑ θ𝑗θ𝑗
𝑗=1

𝑛
𝑛 ∑ 𝑅𝑘
𝑘=1

⁄

⁄

A.2  Proof of Theorem 2
Proof. Writing ST𝑞 = S(T + dT) for the quantized version of
a weight matrix ST ∈ ℝ𝑎×𝑏

𝑛×𝑚, we have for small dT

 𝐷 = 1
(a) 1

  ≈
  =(b) 1
  = 1
  =(c) 1

(d)
  ≥

𝑛 𝔼‖𝑓(x| . . . , Θ𝑙−1,ST𝑞, Θ𝑙+1, . . . ) − y‖2
𝑚
𝑛 𝔼‖𝑓(x|Θ)   +   ∑ (𝜕𝑓(x|Θ) 𝜕θ𝑗
𝑗=1

2
)𝑡U−𝑡dt𝑗

⁄

𝑛 ∑ 𝔼‖(𝜕y 𝜕θ𝑗

⁄

𝑚
𝑗=1

)𝑡U−𝑡dt𝑗‖2

2

⁄

𝑚
𝑗=1

)𝑡U−𝑡(U𝑡dθ𝑗)‖2
2

𝑛 ∑ 𝔼‖(𝜕y 𝜕θ𝑗
𝑛 ∑ (U−1C𝛾𝛾U−𝑡)𝑘𝑘(U𝑡C𝜃𝜃U)𝑘𝑘𝜖22−2𝑅𝑘
(∏ (U−1C𝛾𝛾U−𝑡)𝑘𝑘(U𝑡C𝜃𝜃U)𝑘𝑘

𝑛
𝑘=1
𝑛
𝑘=1

)1 𝑛⁄ 𝜖22−2𝑅

2
− y‖2

(16)

in which (a) follows from ﬁrst-order Taylor’s approximation
of 𝑓(x| . . . ,  S(T + dT), . . . ) about Θ = ST, and the chain rule
of diﬀerentiation

APPENDIX B  KLT, ELT, SVD, GSVD, HOSVD
To see how the KLT U𝑡 of θ ∈ ℝ1×1
𝑛  relates to the SVD of the
𝑛×𝑚, we
corresponding fully-connected weight matrix Θ ∈ ℝ1×1
notice  that  cross-channel  covariances C𝜃𝜃 = (1 𝑚⁄ )ΘΘ𝑡 ,  so
the diagonalization U𝑡C𝜃𝜃U = Λ is equivalent to the SVD
Σ = U𝑡ΘV,  U𝑡U = I,  V𝑡V = I,

(19)
𝑛Λ,  and V𝑡 = Σ−1U𝑡Θ.  Therefore,  the  right
in  which Σ =
singular vectors V of Θ are transform coeﬃcients of weights
(up to scaling by Σ−1) whereas the left ones U, the transform
basis. Similarly, the ELT U𝑡 of θ ∈ ℝ1×1
𝑛  relates to the GSVD
(generalized SVD) relation

√

−1U = I,  V𝑡V = I,

Σ = U−1ΘV−𝑡,  U𝑡C𝛾𝛾

(20)
noting that U−1 ≠ U𝑡, and V−𝑡 ≠ V for the GSVD. While the
connection between the KLT and the SVD is simple, optimal
quantization of Θ is not immediately obvious in the SVD or
GSVD domain, and best understood via the rate–distortion-
theoretic framework we have developed in this work.
  CNN model compression methods based on high-order-
SVD (HOSVD) treat convolution weight matrices as fourth-
order tensors, and decompose them across multiple axes (or
dimensions). Given their relatively small spatial dimensions
(usually no larger than 3 × 3), these tensors are decomposed
typically only in their input and output-channel dimensions
[52]. In this case, one can express the resulting higher-order
SVD of the weight tensors equivalently as the 2D transform

T = U𝑡ΘV,  U𝑡U = I,  V𝑡V = I,

(21)

in which transforms U and V are matrices of eigenvectors of
C𝜃𝜃 = (1 𝑚⁄ )ΘΘ𝑡, and C𝜗𝜗 = (1 𝑛⁄ )Θ𝑡Θ, respectively, and T
is a non-diagonal matrix of transformed kernels.

(𝜕y 𝜕t𝑗⁄

)𝑡 = (𝜕𝑓(x|ST) 𝜕t𝑗⁄

)𝑡 = (𝜕𝑓(Θ) 𝜕θ𝑗

⁄

)𝑡S,

(17)

REFERENCES

(b) follows from 𝑓(x|Θ) = y, and (c), from the deﬁnitions of
2)2−2𝑅𝑘
covariance matrices C𝛾𝛾, C𝜃𝜃, and that 𝔼(d𝜃𝑘)2 = 𝔼(𝜃𝑘
and 𝔼d𝜃𝑘′d𝜃𝑘 = 0 for 𝑘′ ≠ 𝑘. Inequality (d) is obtained with
equality for 𝑅 = 1
 by choosing 𝑅𝑘 such that all the
distortions (U−1C𝛾𝛾U−𝑡)𝑘𝑘(U𝑡C𝜃𝜃U)𝑘𝑘𝜖22−2𝑅𝑘 are equal.  ∎

𝑛
𝑛 ∑ 𝑅𝑘
𝑘=1

A.3  Proof of Theorem 3
Proof. The denominator of (11) further gives us

(𝜎tc

𝑛
𝑘=1

2 )𝑛 =   ∏ (U−1C𝛾𝛾U−𝑡)𝑘𝑘(U𝑡C𝜃𝜃U)𝑘𝑘
(a)
det(U−1C𝛾𝛾U−𝑡) det(U𝑡C𝜃𝜃U)
≥
= det(U−1) det(C𝛾𝛾) det(C𝜃𝜃) det(U),
= det(C𝛾𝛾C𝜃𝜃) = ∏ 𝜆𝑘(C𝛾𝛾C𝜃𝜃)

,

𝑛
𝑘=1

(18)

in which 𝜆𝑘(𝐀) denotes the 𝑘th eigenvalue of 𝐀. Inequality
(a) follows from Hadamard’s inequality, and all subsequent
equalities from the properties of the determinant.

  [1]  A.  Krizhevsky,  I.  Sutskever,  and  G.  E.  Hinton,  “ImageNet
classiﬁcation with deep convolutional neural networks,” in NIPS,
2012, pp. 1097–1105.

  [2]  K. He, G. Gkioxari, P. Dollar, and R. Girshick, “Mask R-CNN,” in

CVPR, 2017, pp. 2961–2969.

  [3]  L. A. Gatys, A. S. Ecker, and M. Bethge, “Image style transfer using
convolutional neural networks,” in CVPR, 2016, pp. 2414–2423.
  [4]  J. Johnson, A. Alahi, and F.-F. Li, “Perceptual losses for real-time

style transfer and super-resolution,” in ECCV, 2016, pp. 694–711.

  [5]  T. Karras, T. Aila, S. Laine, and J. Lehtinen, “Progressive growing
of GANs for improved quality, stability, and variation,” in ICLR,
2018.

  [6]  V. Sze, Y.-H. Chen, T.-J. Yang, and J. S. Emer, “Eﬃcient processing
of  deep  neural  networks:  a  tutorial  and  survey,”  Proc.  IEEE,  vol.
105, no. 12, pp. 2295–2329, Dec. 2017.

  [7]  H. Li, A. Kadav, I. Durdanovic, H. Samet, and H. P. Graf, “Pruning

ﬁlters for eﬃcient convnets,” in ICLR, 2016.

  [8]  Y. Yang, Y. He, G. Kang, X. Dong, and Y. Fu, “Soft ﬁlter pruning for
accelerating deep convolutional neural networks,” in IJCAI, 2018,
pp. 2234–2240.

  [9]  Y.  He,  P.  Liu,  Z.  Wang,  Z.  Hu,  and  Y.  Yang,  “Filter  pruning  via
geometric  median  for  deep  convolutional  neural  networks
acceleration,” in CVPR, 2019, pp. 4340–4349.

14

IEEE TRANSACTIONS ON PATTERN ANALYSIS AND MACHINE INTELLIGENCE,   VOL. 0,   NO. 0,   MAY 2021

 [10]  J.-H. Luo, J. Wu, and W. Lin, “ThiNet: a ﬁlter level pruning method
for  deep  neural  network  compression,”  in  ICCV,  2017,  pp.  5058–
5066.

 [11]  Y.  Zhou,  Y.  Zhang,  Y.  Wang,  and  Q.  Tian,  “Accelerate  CNN  via

recursive Bayesian pruning,” in ICCV, 2019, pp. 3306–3315.

bit quantization of convolution networks for rapid-deployment,”
in NIPS, 2019.

 [39]  S.  Chen,  W.  Wang,  and  S.  J.  Pan,  “Deep  neural  network
quantization  via  layer-wise  optimization  using  limited  training
data,” in AAAI, 2019, vol. 33, pp. 3329–3336.

 [12]  Z. You, K. Yan, J. Ye, M. Ma, and P. Wang, “Gate Decorator: global
ﬁlter  pruning  method  for  accelerating  deep  convolutional  neural
networks,” in NeurIPS, 2019, pp. 2133–2144.

 [40]  R.  Gong  et  al.,  “Diﬀerentiable  soft  quantization:  bridging  full-
precision and low-bit neural networks,” in CVPR, 2019, pp. 4852–
4861.

 [13]  F. Huang, S. Lin, R. Ji, Y. Wu, Y. Li, and B. Zhang, “Accelerating
convolutional  networks  via  global  &  dynamic  ﬁlter  pruning,”  in
IJCAI, 2018, pp. 2425–2432.

 [14]  Z. Zhuang et al., “Discrimination-aware channel pruning for deep

neural networks,” in NIPS, 2018, pp. 875–886.

 [15]  Z. Liu, J. Li, Z. Shen, G. Huang, S. Yan, and C. Zhang, “Learning
eﬃcient  convolutional  networks  through  network  slimming,”  in
ICCV, 2017, pp. 2736–2744.

 [16]  Y. He, X. Zhang, and J. Sun, “Channel pruning for accelerating very

deep neural networks,” in ICCV, 2017, pp. 1389–1397.

 [17]  H.  Peng,  J.  Wu,  S.  Chen,  and  J.  Huang,  “Collaborative  channel
pruning for deep networks,” in ICML, 2019, pp. 5113–5122.
 [18]  T.  Zhang  et  al.,  “A  systematic  DNN  weight  pruning  framework
using alternating direction method of multipliers,” in ECCV, 2018,
pp. 184–199.

 [19]  R.  Yu  et  al.,  “NISP:  pruning  networks  using  neuron  importance

score propagation,” in CVPR, 2018, pp. 9194–9203.

 [20]  S. Han, H. Mao, and W. J. Dally, “Deep compression: compressing
deep  neural  networks  with  pruning,  trained  quantization  and
Huﬀman coding,” in ICLR, 2016.

 [21]  F. Tung and G. Mori, “CLIP-Q: deep network compression learning
by  in-parallel  pruning-quantization,”  in  CVPR,  2018,  pp.  7873–
7882.

 [22]  Y.  Gong,  L.  Liu,  M.  Yang,  and  L.  Bourdev,  “Compressing  deep
convolutional networks using vector quantization,” in ICLR, 2015.
 [23]  P. Stock, A. Joulin, R. Gribonval, B. Graham, and H. Jégou, “And
the bit goes down: revisiting the quantization of neural networks,”
in ICLR, 2020.

 [24]  Y.  Wang,  C.  Xu,  S.  You,  D.  Tao,  and  C.  Xu,  “CNNpack:  packing
convolutional neural networks in the frequency domain,” in NIPS,
2016, pp. 253–261.

 [25]  W.  Chen,  J.  T.  Wilson,  S.  Tyree,  K.  Q.  Weinberger,  and  Y.  Chen,
“Compressing neural networks with the hashing trick,” in ICML,
2015, pp. 2285–2294.

 [26]  W.  Chen,  J.  Wilson,  S.  Tyree,  K.  Q.  Weinberger,  and  Y.  Chen,
“Compressing  convolutional  neural  networks  in  the  frequency
domain,” in SIGKDD, 2016, pp. 1475–1484.

 [27]  J.  Wu,  C.  Leng,  Y.  Wang,  Q.  Hu,  and  J.  Cheng,  “Quantized
convolutional neural networks for mobile devices,” in CVPR, 2016,
pp. 4820–4828.

 [28]  M. Rastegari, V. Ordonez, J. Redmon, and A. Farhadi, “XNOR-Net:
ImageNet  classiﬁcation  using  binary  convolutional  neural
networks,” in ECCV, 2016, pp. 525–542.

 [29]  F. Li, B. Zhang, and B. Liu, “Ternary Weight Networks,” in NIPS
Workshop on Eﬃcient Methods for Deep Neural Networks, 2016.
 [30]  C.  Zhu,  S.  Han,  H.  Mao,  and  W.  J.  Dally,  “Trained  ternary

quantization,” in ICLR, 2017.

 [31]  I. Hubara, M. Courbariaux, D. Soudry, R. El-Yaniv, and Y. Bengio,
“Quantized  neural  networks:  training  neural  networks  with  low
precision weights and activations,” J. Mach. Learn. Res., vol. 18, no.
187, pp. 1–30, 2018.

 [32]  J. Faraone, N. Fraser, M. Blor, and P. H. W. Leong, “SYQ: learning
symmetric  quantization  for  eﬃcient  deep  neural  networks,”  in
CVPR, 2018, pp. 4300–4309.

 [33]  B. Jacob et al., “Quantization and training of neural networks for
eﬃcient  integer-arithmetic-only  inference,”  in  CVPR,  2018,  pp.
2704–2713.

 [34]  S. Son, S. Nah, and K. Mu Lee, “Clustering convolutional kernels

to compress deep neural networks,” in ECCV, 2018, pp. 216–232.

 [35]  Z.  Dong,  Z.  Yao,  A.  Gholami,  M.  W.  Mahoney,  and  K.  Keuser,
“HAWQ:  Hessian  AWare  Quantization  of  neural  networks  with
mixed-precision,” in ICCV, 2019, pp. 293–302.

 [36]  A. Zhou, A. Yao, Y. Guo, L. Xu, and Y. Chen, “Incremental Network
Quantization: towards lossless CNNs with low-precision weights,”
in ICLR, 2017.

 [37]  D.  Zhang,  J.  Yang,  D.  Ye,  and  G.  Hua,  “LQ-Nets:  learned
quantization  for  highly  accurate  and  compact  deep  neural
networks,” in ECCV, 2018, pp. 373–390.

 [38]  R. Banner, Y. Nahshan, E. Hoﬀer, and D. Soudry, “Post-training 4-

 [41]  I. Hubara, M. Courbariaux, D. Soudry, R. El-Yaniv, and Y. Bengio,
“Binarized neural networks,” in NIPS, 2016, pp. 4107–4115.
 [42]  S. Zhou, Y. Wu, Z. Ni, X. Zhou, H. Wen, and Y. Zou, “DoReFa-Net:
training  low  bitwidth  convolutional  neural  networks  with  low
bitwidth gradients,” in arXiv:1606.06160 [cs], 2018.

 [43]  M. Nagel, M. van Baalen, T. Blankevoort, and M. Welling, “Data-
through  weight  equalization  and  bias

free  quantization
correction,” in CVPR, 2019, pp. 1325–1334.

 [44]  W. Zhe, J. Lin, V. Chandrasekhar, and B. Girod, “Optimizing the
bit allocation for compression of weights and activations of deep
neural networks,” in ICIP, 2019, pp. 3826–3830.

 [45]  D.  Oktay,  J.  Ballé,  S.  Singh,  and A.  Shrivastava,  “Scalable  model
compression  by  entropy  penalized  reparameterization,”  in  ICLR,
2020.

 [46]  K. Wang, Z. Liu, Y. Lin, J. Lin, and S. Han, “HAQ: Hardware-aware
automated quantization with mixed precision,” in CVPR, 2019, pp.
8612–8620.

 [47]  E.  L.  Denton,  W.  Zaremba,  J.  Bruna,  Y.  LeCun,  and  R.  Fergus,
“Exploiting  linear  structure  within  convolutional  networks  for
eﬃcient evaluation,” in NIPS, 2014, pp. 1269–1277.

 [48]  B. Liu, M. Wang, H. Foroosh, M. Tappen, and M. Pensky, “Sparse
convolutional neural networks,” in CVPR, 2015, pp. 806–814.
 [49]  Y. Li, S. Gu, L. V. Gool, and R. Timofte, “Learning ﬁlter basis for
convolutional  neural  network  compression,”  in  ICCV,  2019,  pp.
5623–5632.

 [50]  V. Lebedev, Y. Ganin, M. Rakhuba, I. Oseledets, and V. Lempitsky,
“Speeding-up convolutional neural networks using ﬁne-tuned CP-
decomposition,” in ICLR, 2015.

 [51]  X. Zhang, J. Zou, X. Ming, K. He, and J. Sun, “Eﬃcient and accurate
approximations  of  nonlinear  convolutional  networks,”  in  CVPR,
2015, pp. 1984–1992.

 [52]  Y.-D.  Kim,  E.  Park,  S.  Yoo,  T.  Choi,  L.  Yang,  and  D.  Shin,
“Compression of deep convolutional neural networks for fast and
low power mobile applications,” in ICLR, 2016.

 [53]  Y. Cheng, F. X. Yu, R. S. Feris, S. Kumar, A. Choudhary, and S.-F.
Chang,  “An  exploration  of  parameter  redundancy  in  deep
networks with circulant projections,” in ICCV, 2015, pp. 2857–2865.
 [54]  B.  Peng,  W.  Tan,  Z.  Li,  S.  Zhang,  D.  Xie,  and  S.  Pu,  “Extreme
network  compression  via  ﬁlter  group  approximation,”  in  ECCV,
2018, pp. 300–316.

 [55]  A.  Novikov,  D.  Podoprikhin,  A.  Osokin,  and  D.  P.  Vetrov,
“Tensorizing neural networks,” in NIPS, 2015, pp. 442–450.
 [56]  M.  Wang,  B.  Liu,  and  H.  Foroosh,  “Factorized  Convolutional

Neural Networks,” in CVPR Workshops, 2017, pp. 545–553.

 [57]  K.  R.  Rao  and  P.  Yip,  Discrete  Cosine  Transform:  Algorithms,

Advantages, Applications. Academic Press, 2014.

 [58]  D.  Taubman  and  M.  Marcellin,  JPEG2000:  Image  Compression
Fundamentals, Standards and Practice. Norwell, MA, USA: Kluwer,
2001.

 [59]  G. Sullivan, “Versatile Video Coding (VVC) arrives,” in VCIP, 2020,

pp. 1–1.

 [60]  K.  He,  X.  Zhang,  S.  Ren,  and  J.  Sun,  “Deep  residual  learning  for

image recognition,” in CVPR, 2016, pp. 770–778.

 [61]  G.  Huang,  Z.  Liu,  L.  van  der  Maaten,  and  K.  Q.  Weinberger,
“Densely connected convolutional networks,” in CVPR, 2017, pp.
4700–4708.

 [62]  K.  Zhang,  Y.  Li,  W.  Zuo,  L.  Zhang,  L.  Van  Gool,  and  R.  Timofte,
“Plug-and-play  image  restoration  with  deep  denoiser  prior,”
ArXiv200813751 Cs Eess, Aug. 2020.

 [63]  B. Lim, S. Son, H. Kim, S. Nah, and K. Mu Lee, “Enhanced deep
residual  networks  for  single  image  super-resolution,”  in  CVPR
Workshops, 2017, pp. 136–144.

 [64]  M. Sandler, A. Howard, M. Zhu, A. Zhmoginov, and L.-C. Chen,
“MobileNetV2:  inverted  residuals  and  linear  borlenecks,”  in
CVPR, 2018, pp. 4510–4520.

 [65]  F. N. Iandola, S. Han, M. W. Moskewicz, K. Ashraf, W. J. Dally, and
K.  Keuser,  “SqueezeNet: AlexNet-level  accuracy  with  50x  fewer
parameters and <0.5MB model size,” in arXiv:1602.07360 [cs], 2016.
 [66]  L.  Huang  et  al.,  “Controllable  orthogonalization  in  training

YOUNG ET AL.: TRANSFORM QUANTIZATION FOR CNN COMPRESSION

15

DNNs,” in CVPR, 2020.

 [67]  G.  Desjardins,  K.  Simonyan,  R.  Pascanu,  and  K.  Kavukcuoglu,

“Natural Neural Networks,” in NIPS, 2015, pp. 2071–2079.

 [68]  J.  Martens  and  R.  Grosse,  “Optimizing  neural  networks  with
Kronecker-factored  approximate  curvature,”  in  ICML,  2015,  pp.
2408–2417.

 [69]  R.  Grosse  and  J.  Martens,  “A  Kronecker-factored  approximate
Fisher matrix for convolution layers,” in ICML, 2016, pp. 573–582.
 [70]  T.  George,  C.  Laurent,  X.  Bouthillier,  N.  Ballas,  and  P.  Vincent,
“Fast  approximate  natural  gradient  descent  in  a  Kronecker-
factored eigenbasis,” in NIPS, 2018, pp. 9550–9560.

 [71]  A.  Bernacchia,  M.  Lengyel,  and  G.  Hennequin,  “Exact  natural
gradient  in  deep  linear  networks  and  its  application  to  the
nonlinear case,” in NIPS, 2018, pp. 5941–5950.

 [72]  L.  Huang,  D.  Yang,  B.  Lang,  and  J.  Deng,  “Decorrelated  Batch

Normalization,” in CVPR, 2018, pp. 791–800.

 [73]  W. Gao, Y.-H. Liu, C. Wang, and S. Oh, “Rate distortion for model
compression:  from  theory  to  practice,”  in  ICML,  2019,  pp.  2102–
2111.

 [74]  J.  C.  Ye,  Y.  Han,  and  E.  Cha,  “Deep  convolutional  framelets:  a
general deep learning framework for inverse problems,” SIAM J.
Imaging Sci., vol. 11, no. 2, pp. 991–1048, Jan. 2018.

 [75]  M.  Flierl  and  B.  Girod,  Video  Coding  with  Superimposed  Motion-
Compensated Signals: Applications to H.264 and Beyond. Springer US,
2004.

 [76]  V. K. Goyal, “Theoretical foundations of transform coding,” IEEE

Signal Process. Mag., vol. 18, no. 5, pp. 9–21, Sep. 2001.

 [77]  A.  Gersho  and  R.  M.  Gray,  Vector  Quantization  and  Signal

Compression. Norwell, MA, USA: Kluwer, 1991.

 [78]  G.  J.  Sullivan,  “Eﬃcient  scalar  quantization  of  exponential  and
Laplacian random variables,” IEEE Trans. Inf. Theory, vol. 42, no. 5,
pp. 1365–1374, Sep. 1996.

 [79]  S.  Lloyd,  “Least  squares  quantization  in  PCM,”  IEEE  Trans.  Inf.

Theory, vol. 28, no. 2, pp. 129–137, Mar. 1982.

 [80]  J.  Max,  “Quantizing  for  minimum  distortion,”  IRE  Trans.  Inf.

Theory, vol. 6, no. 1, pp. 7–12, Mar. 1960.

 [81]  O.  Russakovsky  et  al.,  “ImageNet  large  scale  visual  recognition
challenge,”  Int.  J.  Comput.  Vis.,  vol.  115,  no.  3,  pp.  211–252,  Dec.
2015.

 [82]  N. P. Jouppi et al., “In-Datacenter Performance Analysis of a Tensor
Processing  Unit,”  in  Proceedings  of  the  44th  Annual  International
Symposium  on  Computer Architecture,  Toronto,  ON,  Canada,  2017,
pp. 1–12.

 [83]  Y. Chen, T. Krishna, J. S. Emer, and V. Sze, “Eyeriss: An Energy-
Eﬃcient  Reconﬁgurable  Accelerator  for  Deep  Convolutional
Neural  Networks,”  IEEE  J.  Solid-State  Circuits,  vol.  52,  no.  1,  pp.
127–138, Jan. 2017.

 [84]  A. Samajdar, J. M. Joseph, Y. Zhu, P. Whatmough, M. Marina, and
T.  Krishna,  “A  Systematic  Methodology  for  Characterizing
Scalability of DNN Accelerators using SCALE-Sim,” in 2020 IEEE
International  Symposium  on  Performance  Analysis  of  Systems  and
Software (ISPASS), 2020, pp. 58–68.

 [85]  E.  Agustsson  and  R.  Timofte,  “NTIRE  2017  challenge  on  single
image  super-resolution:  dataset  and  study,”  in  CVPR  Workshops,
2017, pp. 126–135.

 [86]  M. Bevilacqua, A. Roumy, C. Guillemot, and M. L. Alberi-Morel,
super-resolution  based  on

“Low-complexity
nonnegative neighbor embedding,” in BMVC, 2012, p. 135.1–10.

single-image

 [87]  R. Zeyde, M. Elad, and M. Prorer, “On single image scale-up using
sparse-representations,” in Curves and Surfaces, Berlin, Heidelberg,
2012, pp. 711–730.

 [88]  D. Martin, C. Fowlkes, D. Tal, and J. Malik, “A database of human
segmented  natural  images  and  its  application  to  evaluating
segmentation  algorithms  and  measuring  ecological  statistics,”  in
ICCV, 2001, pp. 416–423.

 [89]  J.-B.  Huang,  A.  Singh,  and  N.  Ahuja,  “Single  image  super-

resolution  from  transformed  self-exemplars,”  in  CVPR,  2015,  pp.
5197–5206.

 [90]  T.  Wang  et  al.,  “APQ:  Joint  Search  for  Network  Architecture,
Pruning and Quantization Policy,” in CVPR, 2020, pp. 2078–2087.

Sean I. Young received B.Com and B.E. degrees in software engineering
from  the  University  of Auckland  in  2008,  and  the  M.EngSc  and  Ph.D.
degrees from the University of New South Wales, Sydney, in 2011 and
2018, respectively. He is currently a postdoctoral researcher at Stanford
University, Stanford, CA, USA. In 2016, he was a visiting researcher at
InterDigital Communications, San Diego, CA. His research interests are
large-scale optimization and inverse problems in image processing. He
received the APRS/IAPR best paper award at DICTA 2018, together with
David Taubman.

Wang Zhe received his B.E. degree from Beijing Jiaotong University in
2012, and the M.S. degree in computer applied technology from Peking
University  in  2015.  He  is  currently  a  senior  research  engineer  at  the
Institute for Infocomm Research, A*STAR, Singapore. In 2018, he was a
visiting scholar at Stanford University, Stanford, CA, USA. His research
interests  include  large-scale  image  and  video  search,  neural  network
compression, and deep learning hardware. He has published more than
20 research papers in computer vision and deep learning, and has ﬁled
5 patents. His work on fast indexing and global descriptor aggregation
has been adopted by the MPEG-CDVS (MPEG Compact Descriptors for
Visual Search) standard.

David Taubman received B.S. and B.E. degrees in electrical engineering
from the University of Sydney, in 1986 and 1988, respectively, and the
M.S. and Ph.D. degrees from the University of California at Berkeley, in
1992 and 1994, respectively. From 1994 to 1998, he was with Hewler–
Packard’s  Research  Laboratories,  Palo Alto,  CA.  He  joined  UNSW  in
1998,  where  he  is  currently  a  Professor  with  the  School  of  Electrical
Engineering  and  Telecommunications.  He  has  authored  the  book
JPEG2000: Image Compression Fundamentals, Standards and Practice,
with M. Marcellin. His research interests include highly scalable image
and  video  compression,  motion  estimation  and  modeling,  inverse
problems
imaging,  perceptual  modeling,  and  multimedia
distribution  systems.  He  received  the  University  Medal  from  the
University of Sydney. He has received two best paper awards from the
IEEE  Circuits  and  Systems  Society  for  the  1996  paper  entitled  A
Common Framework for Rate and Distortion-Based Scaling of Highly
Scalable  Compressed  Video,  and  from  the  IEEE  Signal  Processing
Society  for  the  2000  paper  entitled  High  Performance  Scalable  Image
Compression with EBCOT.

in

Bernd  Girod  received  the  Engineering  Doctorate  degree  from
University of Hannover, Germany, and the M.S. degree from Georgia
Institute of Technology. Until 1999, he was a Professor with the Electrical
Engineering  Department,  University  of  Erlangen–Nuremberg.  He  is
currently the Robert L. and Audrey S. Hancock Professor of Electrical
Engineering, Stanford University, CA, USA. He has authored over 600
conference and journal papers and six books. His research interests are
in the area of image, video and multimedia systems. As an entrepreneur,
he was involved in numerous startup ventures, among them Polycom,
Vivo  Software,  8×8,  and  RealNetworks.  He  is  a  EURASIP  Fellow,  a
member of the National Academy of Engineering, and a member of the
German  National Academy  of  Sciences  (Leopoldina).  He  received  the
EURASIP  Signal  Processing  Best  Paper  Award  in  2002,  the  IEEE
Multimedia  Communication  Best  Paper Award  in  2007,  the  EURASIP
Image Communication Best Paper Award in 2008, the EURASIP Signal
Processing  Most  Cited  Paper Award  in  2008,  the  EURASIP  Technical
Achievement Award in 2004, and the Technical Achievement Award of
the IEEE Signal Processing Society in 2011.


