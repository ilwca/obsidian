# 23/02

**informação** : dados que possuem algum valor ( financeiro, )
**exploits**: códigos, dados ou sequencias de comandos criados para tirar vantagens de vulnerabilidades em softwares, hardwares ou sistemas permitindo ações não autorizadas como roubo de dados ou instalação de malwares.

## Três Pilares da Segurança
**integridade**: refere-se a manutenção das condições iniciais das informações de acordo com a forma produzidas e armazenadas.

**disponibilidade**:propriedade de resistência a flash (hardware, software, energia) objetivando manter os serviços disponibilizados o máximo de tempo possível

**confiabilidade**: a informação sera somente acessível para indivíduos entidades ou processos devidamente autorizados. 

`Um agente externo pode oferecer uma AMEAÇA a um sistema que se encontra em estado de vulnerabilidade, podendo efetuar um ataque. por isso é importante haver mecanismos de CONTROLE sobre as vulnerabilidades para minimizar a PROBABILIDADE de chances de falha e IMPACTOS indesejados.`


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

# Hashes Criptográficos
Um algoritmo de hash criptográfico é uma função matemática cujo o resultado é um valor de tamanho fixo, gerado a partir de uma entrada de tamanho arbitrário.
Dado seu atributo de unidirecionalidade, a partir de seu resultado é impraticável produzir o parâmetro de entrada.
_Ou seja, impossível obter o conteúdo que foi utilizado na geração daquele hash._


## Esteganografia
E a pratica de ocultar informações secretas dentro de outros arquivos (imagnes, textos...), tornando a mensagem oculta invisível ou indetectável para quem não sabe da sua existência.

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
![[diagrama-cript.png]]
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

### Cifra de Bloco
A maioria dos métodos de criptografia usa método de cifra de bloco, como: DES, BlowFish, RC5, 3-DES, etc...

As entradas são blocos de texto plano e uma chave **k**. As entradas são divididas no meio em dois blocos, o $L_0$ e o $R_0$. Estas duas metades passam por $N$ rodadas de processamento e são combinadas ao final para produzir um bloco de texto cifrado.  
![[cifra-de-bloco.svg.png]]


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


## Tipos de Cifras Simétricas
- AES
- DES 
- RC4

Comparativo entre elas:

| **Nome**                 | **Classificação**        |
| ------------------------ | ------------------------ |
| DES (com variante 3-DES) | Cifra simétrica de BLOCO |
| AES                      | Cifra simétrica de BLOCO |
| RC-4                     | Cifra simétrica de FLUXO |


## ...Revisando Cifras Simétricas
### Vantagens
- Hardware de baixo custo
- Facilidade de uso e implementação
- Rapidez e uso geral
### Desvantagens
- Distribuição e armazenamento das chaves (problema de troca inicial de chaves)
- Não garante *autenticidade* ou *não*-*repúdio*
### Modos
- Bloco
- Fluxo


# Cifras Assimétricas
As cifras assimétricas tem como intuito resolver o problema da *Troca de chaves*.
Dois interlocutores (A e B) querem trocar mensagens via rede. As mensagens secretas devem ser cifradas, então antes de iniciar a comunicação eles devem definir uma chave em comum. 

_como definir uma chave comum através da rede (ambiente inseguro)?_

_Existem funções matemáticas que permitam que A e B combinem uma chave através de um meio inseguro de comunicação?_

![[criptografiaassimetrica.png]]


### Problema da Troca de Chaves
Resolvido em 1976 e publicado por Withfiel Diffie, Martin Hellman e Ralph Merkle, criando o esquema de troca de chaves D-H, o primeiro algoritmo a resolver o problema da substituição de chaves estabelecendo uma chave secreta comum, que pode ser usada com canais inseguros (*sniffing*), com o problema de ser mais lenta que a cifra Simétrica.

---

# 09/03
### Privacidade e Internet - temas que não se misturam
constante fornecimento de dados para fontes publicas e provadas aplicações captura dados de usuários sem autorização.
- Stalker- expressão em lingual inglesa cuja a tradução se assemelha a "perseguidor"
- reconhecimento facial em tempo real
- sequestros digitais
- fontes de informação OSINT(Open Source Inteligence)

## Direito ao Esquecimento
Direito que uma pessoa possui de não permitir que um fato ainda que verídico, ocorrido em determinado momento de sua vida, seja exposto ao publico em geral, causando-lhe sofrimento ou transtorno.
No brasil o direito ao esquecimento possui assento constitucional e legal, considerando que uma consequência do direito a vida privada (privacidade), intimidade e honra, assegurados pela CF/88.

## Redes Descentralizadas - P2P (Peer to Peer)
Arquitetura de redes de computadores onde cada um dos pontos ou nós da rede funciona tanto como cliente quanto como servidor, permitindo compartilhamentos de serviços e dados sem a necessidade de um servidor central
Uma rede P2P possui constantemente, uma imensa quantidade de usuários conectados em alta atividade de trocas de arquivos(incluindo associados a praticas delitivas)
Empresas de mídia e órgão de inteligência cibernética vem distribuindo arquivos falsos em redes de compartilhamento, objetivando proteger o arquivo original de ser distribuído ilegalmente ou para monitorar usuários.

## HTTP e HTTPS
**HTTP** - Define dentre outras formalidades, como são requisitadas as paginas da Web, como são enviados os dados que o usuário insere m formulários e como o servidor envia mensagens para o navegador do usuário. 
No entanto como o http é um protocolo baseado em texto, ou seja, toda a informação transmitida esta em texto claro, os dados do usuário e do servidor podem ser interceptados oi alterados no meio do caminho.

### Spoofing
Spoofing e uma técnica usada para mascarar ou falsificar informações de identificação em comunicações eletrônicas. Pode incluir a falsificação de endereços MAC, IP, e-mails, números de telefone ou qualquer outro dado de identificação. O objetivo e enganar os destinatários e faze-los acreditarem que as comunicações são legitimas, permitindo ataques como: phishing, roubo de informações ou distribuição de malware.

## Proxy
Em redes de  computadores, um proxy ("procurador", "representante") é um servidor( um sistema de computador ou uma aplicação) que age como um intermediário para requisições de clientes solicitando recursos de outros servidores.

Diferente das VPN's os proxies não criptografam o trafego, podendo deixa-lo vulnerável a riscos de segurança. Não são uma boa opção para ambientes P2P, pois não ocultam toda sua atividade do seu provedor de internet.

## Rede Privada Virtual - VPN
A Rede de comunicações privada construída sobre uma rede de comunicações publica. Prove um canal de comunicações seguro entre dispositivos.
Serviço de rede intermediário entre o usuário e a internet, que oferece ferramentas adicionais de criptografia e navegação sigilosa. Cria conexão segura e criptografada, que pode ser considerada como um túnel, entre o cliente e um servidor operando pelo serviço VPN. Ferramenta extremamente poderosa para a segurança das informações pessoais. Forma mais solida, segura e simples de prover considerável nível de privacidade e anonimato.
Quando adequadamente implementados, estes protocolos podem assegurar comunicações seguras através de redes de computadores.

## Projeto TOR (The Onion Router)
Marinha norte americana como o objetivo de proteger as comunicaoes do governo.
Redireciona o trafego de internet através de uma rede de servidores voluntários, distribuidos pelo mundo (mais de oito mil servidores).
Garantir o anonimato e consequentemente a privacidade. Usuário poderá acessar paginas mesmo que estejam censuradas em seu pais e garantir que o seu trafego não será interceptado por terceiros. Vos a todas as pessoas ao longo do mundo, seja para lutar contra regimes ditatoriais empregados insatisfeitos com suas empresas, denuncia de autoridades de corrupção, entre muitos outros casos. !_6 nós ate a conexão com o serviço._
### Bloquear TOR BrowserVM
O navegador TOR não pode ser bloqueado impedindo trafego, pois nos TOP geralmente usam  a porta TCP 443(HTTPS)
Para bloquear o navegador TOR e necessários encontrar IP's dos nos TOR ativos.


---

# 16/03

## Portas
Software ou processo servindo de ponto final de comunicações em um sistema operacional hospedeiro.
Identifica aplicações e processos de um computador. A porta é identificada por um numero de 16 bits. E adicionado a um endereço de IP do computador, completando o endereço de destino para uma sessão de comunicação.
Pacotes de dados são encaminhados através da rede para um endereço IP de destino, e em seguida, ao atingir o computador de destino, são encaminhadas para o processo específico ligado ao número de porta de destino.

Aplicações e execuções de serviços comuns costumam ser especificamente reservadas, números bem conhecidos de porta para receber solicitações de serviços das maquinas.
As primeiras  1024 portas são reservadas ("Well Known Ports"). Geralmente, estão reservadas para os processos sistema (daemon) ou aos programas executados por utilizadores privilegiados.
Tradicionalmente associados aos protocolos TCP e UDP da camada de transporte.

## Verificando Estado de Portas
netstat (estatísticas de rede) ferramenta utilitária de rede de linha de comando que exibe conexões de rede TCP e UDP, tabelas de roteamento e estatísticas de protocolo de rede.

## NetCat
Utilitário de rede capaz de enviar e receber dados através de conexões de rede , usando protocolo TCP.
Ferramenta de depuração e exploração de rede rica em recursos. Permite a abertura de portas (listening) e tunelamento de comunicações.

## Bind Shells & Reverse Shells
redireciona operações shell para um host de destino. Útil para execução remota de comandos em hosts comprometidos. Comum em backdoors.
![[bind-shells.png]]
![[reverse-shells.jpg]]


## Nmap
Utilitário para mapeamento de rede e auditoria de segurança, utilizado por profissionais de segurança cibernética e iniciantes para auditar e descobrir portas abertas locais e remotas, alem de hosts e infromações de rede.
Ideal para identificar serviços ou servidores em uma rede.
### Recursos
Os recursos que o Nmap incluem:
- **Descoberta de Hosts** - Identificando hosts na rede
- **Scanner de Portas** - Mostrando as portas TCP e UDP abertas
- **Detecção de versão** - interrogando serviços na rede para determinar a aplicações e o número da versão.
- **Detecção de sistema operacional** - Remotamente determina o sistema operacional e as características de hardware do host(ex:windows).
- **Detecção de vulnerabilidades** - Executando scripts atomizados.


## IDS - Intrusion Detection System
Monitora ambientes computacionais em busca de eventos que possam violar regras de segurança. Dentre esses eventos, destacam-se programas realizando atividade que fogem ao seu comportamento comum, malwares (trojans e worms), e invasões de nós.
Funciona coletando dados, armazenando-os e analisando (em tempo real) padrões de comportamentais, fluxo de dados, horários, dentre outros. Com essas informações, aliado ao conhecimento prévio de padrões de ataque é possível discernir se o evento em questão é um evento malicioso ou não.
Existem modelos baseado em host e outro baseado em rede. A coleta de dados é feita de variadas formas, desde mecanismo de entrada e saída, como mouse e teclado, a arquivos salvos em seus computadores; tabelas de regras, etc. Também é possível analisar a camada de rede do protocolo TCP/IP e analisar o tipo de fluxo, pacotes que entram e saem conexões estabelecidas, dentre outros.

### Diferença de IDS e IPS
Um IDS passivo é projetado para detectar ameaças e informar ao administrados da rede sobre a atividade maliciosa detectada.
Os sistema de prevenção de intrusão (IPS), por outro lado, representa o comportamento de um IDS ativo, ou seja, é projetado com o objetivo de bloquear automaticamente a atividade maliciosa, seja por configuração de firewalls e computadores ou outras tecnicas, como encerramento de conexão via envio de pacores reset.
[SNORT](https://www.snort.org) - Open Source Network-based instruction detection/prevention (IDS/IPS)


## CVE - Commom Vulnerabilities and Exposures
Base de dados internacional e publica para troca de informações sobre falhas de seguranca.
Seu objetivo e padronizar nomes para todas as vulnerabilidades e exposições.

## Honey Pots (Potes de Mel)
Usados para enganar hacker exponto vulnerabilidades conhecidas deliberadamente. Uma vez que o hacker ache um pote de mel, é comum que esse hacker fique em torno desse pote por algum tempo. Durante esse tempo, pode-se catalogar as atividades do hacker para descobrir suas ações tecnicas. Geralmente possui servicos comuns em execução http(80) tcp(21), entre outros. Pode tambem haver a configuração do firewall para redirecionar o trafego em algumas portas para um pote de mel, onde o intruso estará pensando que esta se conectando a um servidor real.
Como o pote de mel deve parecer real, devem ser criados alguns arquivos de dados contas de usuários, entre outros, todos FALSOS, para garantir que o hacker pense que se trata mesmo de um sistema real, o que fara com que o hacker se coise.


# 23/03

## Obtendo o IP
usado o comando apos descobrir o IP da maquina alvo.

`sudo netdiscover -i vboxnet0 -r 192.168.56.0/24` 

vamos destrinchar cada argumento...:

`netdiscover`: ferramenta utilizada para descobrir

`-i`: i de interface que sera pesquisada, pois temos varias interfaces de rede, como:
- `wlan0` - interface lan de wifi.
- `eth0` - interface ethernet de rede cabeada.
- `vboxnet0` - interface da maquina virtual.

`vboxnet0`: Quando a VM sobe, ela emula uma rede virtual que sera conectada pela VM criada, sendo a vboxnet, que fica fixa conectada no host. 

`-r`: O parâmetro `-r`especifica a range da busca, como já obtemos os primeiros 24 dos 34 bits do ip, vamos especificar com os primeiros bits iniciais para estabelecer a range, sendo estes...

`192.168.56`: Como sabemos que a maquina alvo esta na mesma rede virtual  (vlan) da nossa maquina hosta na vbox, especificamos com estes 24 bits do IP.

isso dará uma lista das maquina no mesmo host, ou seja, que estão usando o mesma faixa de IP 192.168.56.*

Após obter a lista com os IP acima, (exemplo: `192.168.56.101`) usaremos o [[#Nmap]] obter relatório completo da maquina alvo, usando o comando:

## Descobrindo Portas 

`sudo nmap -A 192.168.56.101`
com este relatório teremos quais portas da maquinas estão abertas, como:
- 21 - FTP
- 80 - HTTP
Caso tivermos uma porta `21/tcp` aberta, indica que temos um servidor http aberto e uma conexão ftp. 
Com esta conexão ftp podemos ver qual serviço esta utilizando e qual a versão, como exemplo `vsftpd 2.3.4` que podemos verificar as vulnerabilidades de sua versão usando o **Exploit-DB** ou o comando `searchsploit` com o comando `searchsploit vsftpd 2.3.4`.
Outra alternativa muito escalável seria usar o **MSF CONSOLE**.
Usando o comando `msfconsole`. Ele conta com mais de 2.000 exploits catalogados, além de **Payloads**.

## Payloads
Payloads são códigos maliciosos executados na maquina alvo depois que a brecha foi explorada e a conexão estabelecida em casos de portas abertas como acabamos de usar.

dentro do msfconsole, use o comando `search vsftpd 2.3.4`para consultar os exploits disponíveis para esta versão de serviço. 
use o exploit `unix/ftp/vsftpd_234_backdoor` para atacar esta versão.

`msf exploit (unix/ftp/vsftpd_234_backdoor)`

Dentro do msconsole, podemos usar o comando `show payloads`para mostrar os payloads disponíveis para usar.


## Força Bruta
Para descobrirmos o usuario e senha usando forca bruta, usaremos o `auxiliary(scanner/ftp/ftp_login` do msfconsole. definiremos alguns parametros como:
```
use auxiliary/scanner/ftp/ftp_login 
set RHOSTS 192.168.56.102 # -> IP alvo
set USER_FILE /root/usuarios.txt # -> arquivo de usuarios.txt
set PASS_FILE /root/senhas.txt set THREADS 4 
set BRUTEFORCE_SPEED 2 set STOP_ON_SUCCESS true # -> parar quando acessado
set VERBOSE true # -> mostrar passos
run
```

desta form ele cruzara todos os usuários com todas as senhas, até que encontre o login ou falhe.


---

# 30/03

## Elevação de Privilégios
### Vulnerabilidade 
uma vulnerabilidade e um defeito ou problema presenta na especificação ou implementação, configuração ou operação de um software, hardware ou sistema, que possa ser explorado para violar as propriedades de segurança do mesmo.

### Elevação ou Escalonamento 
elevação de privilégios consiste no ato de explorar vulnerabilidades ou deficiências de configuração em sistemas operacionais ou aplicativos de software para obter acesso a recursos que normalmente são protegidos.
Pode ser classificado em duas categorias:
- **Escalonamento Vertical**: Um usuário ou aplicativo de privilegio inferior acessa funções ou conteúdos reservados para usuários ou aplicativos de privilegio superior: (usuários -> super usuário).
- **Escalonamento Horizontal**: Ocorre quando um usuário normal acessa funções ou conteúdos reservados para usuários de mesmo nível de privilegio: (usuários -> usuário).

A elevação de privilégios frequentemente se faz necessária apos a obtenção de acesso não autorizado a um determinado alvo.
Empreendida em duas etapas:
- Enumeração (identificar informações acerca do sistema alvo);
- Exploração (Abusar de vulnerabilizardes porventura existentes).

Podem ser obtidas através da exploração de:
- Forca bruta em hashes de senhas de baixa complexidade
- Arquivos provativos de autenticação (id_rsa)
- Vulnerabilidades do hardware (chipset)
- Vulnerabilidade  de  kernel
- Vulnerabilidade de aplicações
- Permissões de sudo
- Tarefas agendadas
- Permissões SUID

### **Enumeração** de operações do sistema operacional Kernel Linux...
Identificar informações acerca do sistema:
```Qterminal
$ uname -a
$ cat /etc/issue
$ cat /proc/version
```

Identificar informações acerca dos usuários:
```Qterminal
$ id
$ whoami
$ sudo -l
$ groups
$ cat /etc/passwd
$ cat /etc/shadow
$ cat /etc/group
```

Identificar arquivos de diretodios de historicos:
```Qterminal
$ cat ~/.bash_history
$ cat ~/.mysql_history 
```

Identificar informações de pacotes vulneráveis:
```Qterminal
$ dpkg -l
$ mysql --version
$ sudo --version
$ snap --version
```

Ferramentas usadas para automatização destas...:
- LinPEAS
- LinENUM

### forca bruta em hashes de senhas de baixa complexidade.
arquivos que armazenam credenciais de usuários:
`/etc/passwd`
`/etc/shadow`


Comando de gerar  chave ssh usando algoritmo rsa
`ssh-keygen -t rsa`



