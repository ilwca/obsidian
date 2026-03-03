# 23/02

**informação** : dados que possuem algum valor ( financeiro, )
**exploits**: códigos, dados ou sequencias de comandos criados para tirar vantagens de vulnerabilidades em softwares, hardwares ou sistemas permitindo ações não autorizadas como roubo de dados ou instalação de malwares.

## Três Pilares da Segurança
**integridade**: refere-se a manutenção das condições iniciais das informações de acordo com a forma produzidas e armazenadas.

**disponibilidade**:propriedade de resistência a flash (hardware, software, energia) objetivando manter os serviços disponibilizados o máximo de tempo possível

**confiabilidade**: a informação sera somente acessível para indivíduos entidades ou processos devidamente autorizados. 

`Um agente externo pode oferecer uma AMEAÇA a um sistema que se encontra em estado de vulnerabilidade, podendo efetuar um ataque. por isso é importante haver mecanismos de CONTROLE sobre as vulnerabilidades para minimizar a PROBABILIDADE de chances de falha e IMPACTOS indesejados.

## Vulnerabilidades

- Humanas (Elo mais fraco - engenharia social)

- Físicas (perímetro de segurança fragilizado)

- Naturais (Terremoto, maremoto, inundações, secas)

- Hardware (Exemplo EDL, em chipset qualcomm)

- Software (zero-day vs one-day)

- Mídias (Campos magnéticos podem danificar mídias)

- Comunicação (canal inseguro)

**Zero-Day**: que não é conhecida pelo fabricante
**One-Day**: Falha já catalogada.


## Engenharia Social
Método de ataque onde alguém faz uso da persuasão, muitas vezes abusando da ingenuidade ou confiança do usuário, para obter informacaões que podem ser utilizadas para ter acesso não autorizado aos ativos da informação.

| Nome            | Descrição                                                                                                                                                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Adware          | propaganda que e integrada ao software.                                                                                                                                                                                                                    |
| Cavalo de Troia | Programa de computador que parece ter uma função útil, mas também tem uma função oculta e potencialmente que escapa aos mecanismos de segurança                                                                                                            |
| Exploits        | Códigos específicos para uma unica vulnerabilidade ou conjunto de vulnerabilidades.                                                                                                                                                                        |
| Flooders        | Usados para gerar grande volume de dados para atacar sistemas em rede executando alguma forma de ataque.                                                                                                                                                   |
| Keyloggers      | capturam teclas digitadas no teclado de um sistema comprometido                                                                                                                                                                                            |
| Screenloggers   | capturam telas em um sistema comprometido.                                                                                                                                                                                                                 |
| Spyware         | software que coleta informações de um computador e as transmite a outro sistema. Informações podem ser obtidas via monitoração de teclas digitadas, dados de tela e/ou trafego na rede, ou por escaneamento de arquivos no sistema em busca de informações |
| Vírus           | Malware que, quando executado, tenta se reproduzir na forma de outro código de maquina executável ou código de script                                                                                                                                      |
| Zumbi(bot)      | programa ativado em uma máquina infectada que e usado para lançar ataques contra outras maquinas                                                                                                                                                           |
| Bomba Lógica    | Código inserido em um malware por um intruso. Uma bomba lógica permanece em hibernação até ocorrer uma condição predefinida; então, o código ativa uma ação não autorizada.                                                                                |

---

# 02/03


## Esteganografia
E a pratica de ocultar informacoes secrretas dentro de outrops arquivos (imagnes, textos...), tornando a mensagem oculta invisivel ou indetectavel para quem nao sabe da sua existencia

## Criptografia
- termo de origem graga que significa "escrita secreta"
- Permite dois individuos troquem mensagens confidenciais por um canal inseguro
- A mensagem so podera ser revelada com a presenca de uma chave secreta, conhecida apensa pelo remetente e pelo destinatario (usuarios autorizados)

Diferente da esteganografia, na criptografia as pessoas sabem que ha um conteudo escondido.

- Texto em claro ou dado decifrado
	- informacao inteligivel ou desprotegida
	- informacao antres de ser protegida
	- recuperar o texto em claro e o objetivo do perito

- Chave
	- Sequencia de bits utilizada, em conjunto 


## Propriedades da Criptografia
### Difusão
Dissipação das características do texto claro de tal forma que não apareçam no texto cifrado: uma letra frequente no texto em claro não resulta em estatísticas perceptíveis no texto cifrado.
obs.:_a difusão não leva padrões dos dados para a conteúdo cifrado._
### Confusão
A relação entre o valor da chave e o texto cifrado é tão complexa que não é possível deduzir o valor da chave a partir do texto cifrado.
obs.:_na confusão, a chave não carrega características da criptografia._
### Efeito Avalanche
Pequenas modificações no texto em claro ou na chave devem gerar grandes mudanças no criptograma.

### Aleatoriedade
O criptograma não deve apresentar padrões ou quaisquer sequências inteligíveis: deve-se parecer com uma sequencia aleatória.

### Segurança Computacional
O custo para quebrar é maior que o valor da informação codificada e o tempo de quebra é maior que a vida útil da informação. 
**Segurança Incondicional** - Mesmo com tempo e poder computacional infinitos, o criptograma não pode ser decifrado.
único algoritmo conhecido: *One*-*time* *pad*


# Tipos de Cifras
### Cifras Clássicas
- Transposição
- Substituição
- Rotores eletromecânicos

### Cifras Modernas
- Simétricas
- Assimétricas

# Cifras Simétricas
### Cifras de Fluxo
- O algoritmo é aplicado bit a bit (ou byte a byte)
- Precisam ser rápidas e simples
- Geralmente utilizado quando não há quantidade determinada de bits (ou bytes). _Ex: wi-fi_

**XOR (OU exclusivo)**
 
![[XOR.png]]

Uma pequena palavra sendo cifrada bit por bit:

**Texto**: l e b r e
**Senha:** a s t r o
**Cript:** ? ? ?

![[text-ascii.png]]

## A E S - Advanced Encryption Standard
Padrão atualmente usado em criptografias simétricas, composto por:
- Substituições
- Permutações
- XOR com chave
Contendo chaves de tamanhos variáveis:
- AES-128, AES-192 ou AES-256
- Blocos de 128 bits
Os modos de operação mais adotados são:
- Eletronic CodeBook
- Cipher Blocj Chaining
