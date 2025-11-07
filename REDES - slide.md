
## 1 - Como funciona a comunicação na mesma rede?
Já parou pra pensar como funciona quando você envia um e-mail para um colega de trabalho? 
Isso se deve a dois tipos de endereço, o MAC e o IP. Neste apresentação estaremos explicando como funciona o protocolo ARP.

![[osi-tcp-ip.png]]

Para isso devemos foca em duas camada do modelo OSI. A camada 3 que é a **camada de REDE**  e a 2, que é a camada de **ENLACE**. 

## Camada de Rede (IP)
A camada de rede é a de comunicação global, pois a partir dela é possível enviar pacotes para um servidor em São Paulo por exemplo, e atravéz do IP é possível fazer o endereçamento da rota deste pacote, pois o IP atua como o endereço postal de uma casa. Assim, por meio da camada de rede um pacote pode ir para qualquer lugar da internet.

## Camada de Enlace (MAC)
A camada de Enlace é de funcionamento local. Quando dois dispositivos estão na mesma rede local LAN. O endereço MAC é o que determina como o pacote será entregue. O MAC é como se fosse o nome da pessoa. _Assim como quando você chama sua mãe em outro cômodo da casa_.

**Mas por que precisamos destas duas camadas e destes dois tipos de endereçamento?** Simples, por que a internet é dividida e organizada de forma hierárquica, com um pacote podendo passar por varias camadas de rede até ser entregue ao destino.


## Endereço MAC
Cada dispositivo conectado a sua rede _smartphone, tv, impressora, computador_ possui um MAC (Media Access Control). Cada MAC é único, e contêm as caracteristicas:

- **Tamanho** : 48 bits (6 bytes), geralmente representado em notação hexadecimal, como: `AA:BB:CC:DD:EE:FF` 

- **Escopo** : Funciona apenas dentro da mesma rede  local LAN.

- **Permanência** : Atribuido pelo IEEE (Institute of Eletrical and Eletronics Engineers). 

os primeiros 3 bytes são definidos pelo fabricante do dispositivo, os últimos 3 bytes (24 bits) identificam o modelo de dispositivo daquela fabricante.
**Por que o MAC é importante?** Imagine que você envia um pacote para o seu amigo, assim, o reteador precisa saber qual é a porta exata que esse pacote deve ser enviado.


## Protocolo Ethernet
O protocolo ethernet é o padrão da camada 2, que define como os dados sao formatados e compartilhados em uma rede local. Praticamente, todas as redes locais modernas usam o protocolo ethernet, normalmente seguindo estes padrões:

- **Padrão IEEE 802.3** : Que define a estrutura dos quadros (Frames).

- **Velocidade Comuns** : 10Mbps (BASE-T), 100Mbps (BASE-T), 1Gbps(Gigabit ethernet), 10Gbps (10 Gigabit ethernet).

- **Meio Fisico**: cabos de par trançado (CAT6), Fibra ótica ou comunicação sem fio (WIFI).

- **Responsabilidade**: Entrega de quadros na mesma LAN usando endereço MAC.

