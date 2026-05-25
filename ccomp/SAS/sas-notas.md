# 23/02

**informação** : dados que possuem algum valor ( financeiro, )
**exploits**: códigos, dados ou sequencias de comandos criados para tirar vantagens de vulnerabilidades em softwares, hardwares ou sistemas permitindo ações não autorizadas como roubo de dados ou instalação de malwares.

## Três Pilares da Segurança
**integridade**: refere-se a manutenção das condições iniciais das informações de acordo com a forma que foram produzidas e armazenadas.

**disponibilidade**: propriedade de resistência a flash (hardware, software, energia) objetivando manter os serviços disponibilizados o máximo de tempo possível

**confiabilidade**: a informação será somente acessível para indivíduos entidades ou processos devidamente autorizados. 

`Um agente externo pode oferecer uma AMEAÇA a um sistema que se encontra em estado de vulnerabilidade, podendo efetuar um ataque. por isso é importante haver mecanismos de CONTROLE sobre as vulnerabilidades para minimizar a PROBABILIDADE de chances de falha e IMPACTOS indesejados.`

## Vulnerabilidades
**confiabilidade**: A informação sera somente acessível para indivíduos entidades ou processos devidamente autorizados. 

- Humanas (Elo mais fraco - engenharia social)

- Físicas (perímetro de segurança fragilizado)

- Naturais (Terremoto, maremoto, inundações, secas)

- Hardware (Exemplo EDL, em chipset qualcomm)

- Software (zero-day vs one-day)

- Mídias (Campos magnéticos podem danificar mídias)

- Comunicação (canal inseguro)

**Zero-Day**: que não é conhecida pelo fabricante
**One-Day**: Falha já catalogada.

## Ransomware
É um sequestro de informação, onde o atacante captura os dados da vítima e os criptografa, exigindo um pagamento para o resgate, apos isso libera uma chave especial capaz de descriptografar os dados.

## Engenharia Social
Método de ataque onde alguém faz uso da persuasão, muitas vezes abusando da ingenuidade ou confiança do usuário, para obter informações que podem ser utilizadas para ter acesso não autorizado aos ativos da informação.

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
Dado seu atributo de **unidirecionalidade**, a partir de seu resultado é impraticável produzir o parâmetro de entrada.
_Ou seja, impossível obter o conteúdo que foi utilizado na geração daquele hash._
### Resistência a colisão
A propriedade da resistência a colisão diz que deve ser computacionalmente difícil ou impossível encontrar um par de $(m, n)$, de forma que $h(m) = h(n)$, em outras palavras, é difícil ou impossível encontrar duas mensagens diferentes que possuem o mesmo código hash, no entanto se isso ocorrer, seria categorizado como uma **colisão**, logo uma vulnerabilidade.

## Esteganografia
E a prática de ocultar informações secretas dentro de outros arquivos (imagens, textos...), tornando a mensagem oculta invisível ou indetectável para quem não sabe da sua existência.

## Criptografia
- termo de origem grega que significa "escrita secreta"
	 Permite dois indivíduos troquem mensagens confidenciais por um canal inseguro
- A mensagem só poderá ser revelada com a presença de uma chave secreta, conhecida apenas pelo remetente e pelo destinatário (usuários autorizados)

Diferente da esteganografia, na criptografia as pessoas sabem que ha um conteúdo escondido.

- Texto em claro ou dado decifrado
	- informação inteligível ou desprotegida
		- informação antes de ser protegida
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
Marinha norte americana como o objetivo de proteger as comunicações do governo.
Redireciona o tráfego de internet através de uma rede de servidores voluntários, distribuídos pelo mundo (mais de oito mil servidores).
Garantir o anonimato e consequentemente a privacidade. Usuário poderá acessar paginas mesmo que estejam censuradas em seu pais e garantir que o seu tráfego não será interceptado por terceiros. Dando voz a todas as pessoas ao longo do mundo, seja para lutar contra regimes ditatoriais empregados insatisfeitos com suas empresas, denúncia de autoridades de corrupção, entre muitos outros casos. !_6 nós ate a conexão com o serviço._
O grau de efetividade da rede TOR depende diretamente do número de voluntários que contribuem para a rede, oferecendo seus servidores para redirecionar o tráfego.
### Bloquear TOR BrowserVM
O navegador TOR não pode ser bloqueado impedindo trafego, pois nos TOP geralmente usam  a porta TCP 443(HTTPS)
Para bloquear o navegador TOR e necessários encontrar IP's dos nós TOR ativos.

### Cenários de Comprometimento da rede TOR
- Um individuo ou organização podem ter controle de uma quantidade significativa dos nós da rede, uma vez que todos os nós são voluntários podendo assim, rastrear os dados.
- Uma software adulterado (navegador) pode ser distribuído, e quando o usuário enganado fizer o uso deste, seus dados e trafego pode sem monitorados.
- Derrubar a porta 443(https) do sistema, uma vez que é a porta utilizada pela rede TOR, é também usada pelo https, bloqueando assim o acesso a grande parte da internet, além do acesso a rede TOR.
 
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
Um IDS passivo é projetado para detectar ameaças e informar ao administrador da rede sobre a atividade maliciosa detectada.
Os sistema de prevenção de intrusão (IPS), por outro lado, representa o comportamento de um IDS ativo, ou seja, é projetado com o objetivo de bloquear automaticamente a atividade maliciosa, seja por configuração de firewalls e computadores ou outras tecnicas, como encerramento de conexão via envio de pacores reset.
[SNORT](https://www.snort.org) - Open Source Network-based instruction detection/prevention (IDS/IPS)


## CVE - Commom Vulnerabilities and Exposures
Base de dados internacional e publica para troca de informações sobre falhas de seguranca.
Seu objetivo e padronizar nomes para todas as vulnerabilidades e exposições.

## Honey Pots (Potes de Mel)
Usados para enganar hacker expondo vulnerabilidades conhecidas deliberadamente. Uma vez que o hacker ache um pote de mel, é comum que esse hacker fique em torno desse pote por algum tempo. Durante esse tempo, pode-se catalogar as atividades do hacker para descobrir suas ações tecnicas. Geralmente possui servicos comuns em execução http(80) tcp(21), entre outros. Pode tambem haver a configuração do firewall para redirecionar o trafego em algumas portas para um pote de mel, onde o intruso estará pensando que esta se conectando a um servidor real.
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

---

# 06/04

## Vulnerabilidades de Hardware
Resultado do modo de operacao de dispisitivos fisicos. Podem ser exploradas fisicamente ou remotamente.
- CVE-2020-069 ()
- CVE-2019-9800
- CVE-2017-5754
Com eleveda frequencia nao podem ser sanadas atras de atualizações a nível de software (), sendo necessario.

## Vulnerabilidades de Kernel
Referem-se a falhas de segurança ou fraquezas no núcleo do sistema operacional de um computador, conhecido como kernel.
Quando ocorrem podem permitir que atacantes obtenham acesso a informações não autorizadas ou que assumam o controle administrativo da máquina alvo.
Podem ser exploradas ate mesmo remotamente e sem qualquer interação do usuário (zero-click).
O comando `uname -a` mostra as informações do kernel do atual SO.
**Exemplo pratico:**
Alguns kernels do ubunto tem vulnerabilidades.

## Vulnerabilidades de Aplicações 
Referem-se a falhas a nivel de codigo, de seguranca ou deficiências de configuração presentes em um produto de software.
Exemplo:
- CVE-2019-7304(Dirty Sock)
Isto impacta versões do gerenciados de pacotes snapd inferiores a 2.37
- [Exploit 1](https://exploit-db/exploits/46361 )
- [Exploit 2](https://exploit-db/exploits/46362)
Capaz de se registrar um novo usuario (dirty_sock)

## Permissões de SUDO
O usuário root em sistemas operacionais com kernel linux é o usuário que tem acesso de nível administrativo. Os usuários normais não tem este acesso por razões de segurança.

Manual sudo: Permite que usuários devidamente autorizados de maneira segura e controlada execute comandos com privilégios de super usuários, conforme especificado pelas politicas de segurança do SÓ.
```Qterminal
sudo -l
sudo nmap
sudo apt install
```


## Tarefas Agendadas
### Cron e Contab
Cron do Linux é um utilitário que executa comandos ou scripts que são agendados por uma tabela chamada de Crontab.
Quando iniciado o Cron procura por arquivos Crontab, com o objetivo de carrega-los em memoria, realizando a leitura do arquivo `/etc/crontab` e dos arquivos armazenados em `/etc/cron.d`.
**Crontab** é um arquivo que contem informações sobre quando um comando ou script deve ser executado e quem é o responsável pela ação. Trata-se de um arquivo de texto com um formato especial para que o Cron entenda e trabalhe em sintonia.

Estrutura do arquivo Crontab:
![[blog-head_syntax-of-cron.webp]]

Com o comando `Crontab -l` é exibido toda a lista de tarefas agendadas do linux.

## Arquivos com permissões SUID
## Arquivos em sistemas operacionais com kernel Linux
No linux, quando um arquivo ou diretório é criado, algumas permissões são atribuídas automaticamente. Essas permissões são divididas em três grupos:
- O usuário que criou o arquivo (usuário dono)
- O grupo dono do arquivo (que pode conter vários usuários)
- Os demais usuários que não pertencem ao grupo dono do arquivo.
Essas permissões por sua vez podem ser de:
- Leitura (r, read, 4) - Permite visualizar o conteúdo
- Escrita (w, write, 2) - Permite alterar o conteúdo
- Execução (x, execute, 1) - Torna o arquivo um executável

![[sas-suid.jpeg]]

Exist tambem uma opção equivalente ao SUID para grupos, a SGID (set group ID). Ela tem o mesmo comportamento que a SUID porem funciona com grupos.


Execute o comando `find`para executar busca por arquivos ou diretórios, podendo também ser adicionado um ação ao efetuar tarefa com sucesso.

**Exemplo Prático:***
```Qterminal
find /etc/passwd -exec "whoami" \;

find /etc/passwd -exec "/bin/sh" -p \;
```



# 13/04

Iniciamos a VM _thales_ com ela na mesma rede vboxnet, descobrimos o ip da VM usando: `sudo netdiscover -i vboxnet0 192.168.56.0/24`.

Em seguida usamos o nmap para escanear todas (`-A`) as portas abertas:
`sudo nmap -A 192.168.56.105` 

E vamos explorar as portas abertas começando pelo tomcat...
usaremos o `msfconsole` e pesquisaremos pelos exploits do Tomcat pesquisando `search Tomcat`

Para usar forca bruta na porta do Tomcat usando o Payload  65 :
`msf auxiliary(scanner/http/tomcat_mgr_login`
 definiremos o: 
 - RHOSTS - IP
 - VERBOSE - true
 - STOP_ON_SUCCCESS - true

---
04/05
# WebHacking

## Data Leak
Exposição de dados sensíveis, resultante de falhas humanadas de processes ou de tecnologias.
_"É possível obter a ficha cadastral na integra de pacientes, acessos a logins médicos, emails internos, planilhas financeiras exames de paciente e ate certidões de óbito e imagens de raio-x"_
### Técnicas práticas de exploração de vulnerabilidades em ambientes Web
- LFI - Local File Inclusion
- RFI - remote File Inclusion
- Command Injection
- SQL Injection
- XSS - Cross Site Scripting
- Brute Force Attack
- Google Hacking
- Denial of Service Attack

## Google Hacking
**Buscando Falhas em sites com auxilio do google**
O Google utiliza de uma tecnologia denominada spiders (ou webcrawlers):Robos que fazem a varredura na web buscando e indexando páginas.Quando  realizamos uma busca pela ferramenta, ela procura por este termo nas páginas indexadas. Cada resultado  retornado é composto por um titulo, uma URL e uma descrição. Um servidor mal configurado pode expor informações da empresa no Google.

Google hackin nada mais é do que uma prática para encontrar arquivos e/ou falhas a partir do Google, utilizando-o como uma especia de scanner, o informando comandos e manipulando buscas avançadas por strings.

## Google DORK's
Com a composição de DORK's podemos retornar domínios específicos, títulos, palavras, arquivos e metadados.
ex:
`site:`
`site:uft.edu.br noticias`-  estas tags irão pesquisar somente noticias com o domínio da UFT.

`inurl:`
`site:uft.edu.br inurl:noticias` - Somente sites com noticias na URL.

`indexof:` - contém diretórios de arquivos.

`intitle:`- Somente conteúdo no title.

`filetype:pdf` - somente conteúdos com arquivos pdf.

## Ataques de negação de Serviços - DoS
Esse serviço esta relacionado a acessibilidade e a capacidade de utilização sob demanda por usuários autorizados.
Um ataque de negação de serviço (Denial of service - DoS) é uma tentativa de comprometer a disponibilidade, impedindo ou bloqueando completamente o fornecimento de algum serviço. O ataque tenta exaurir algum recurso critico associado ao serviço. Um exemplo é inundar um servidor web com tantas requisições espúrias que ele é incapaz de responder a tempo as requisições válidas de usuários. O ataque de negação de serviços **Não é invasão**.

### DDoS - Distribuited Denied of Services
Reconhecendo as limitações de ataques de inundação gerados por um único sistema, uma das primeiras evoluções mais significativas em ferramentas de ataque de DoS foi a utilização de vários sistemas para gerar ataques.
Esses sistemas eram tipicamente estações de trabalho ou PCs comprometidos de usuários (Zumbis).
A _Computer Security Incident Handiling Guide_ do NIST define ataque de negação de servisos da seguinte maneira:
_" É uma ação que impede ou prejudica a outro autorizada de redes, sistemas ou aplicação."_
### Ataques de Inundação - Flooders
Inundam o enlace da rede ligada ao servidor com um torrente de pacotes maliciosos os quais competem com o fluxo de tráfego válido até o servidor e usualmente atropelam, Em resposta ao congestionamento que isso causa em alguns reteadores no caminho até o servidor visado, muitos pacotes serão descartados.  Ataques de inundação comuns usam qualquer um dos tipos de pacote de ICMP, UDP ou TCP SYN.

**Largura de Banda**
A Largura de banda de rede está relaacionada a capacidade dos enlaces de rede que conectam um servidor a internet. Para a maioria das organizações, essa é a conexão com o provedor de serviços de Internet (Internet Service Provider - ISP). Usualmente, essa conexão terá capacidade mais baixa do que os enlaces dentro de roteadores do provedor de serviços de internet. Isso significa que é possivel chegar uma quantidade de trafego aos roteadores do ISO por esses enlaces de maior capacidade, que seja mais alta do que a  quantidade que pode ser transmitida pelo enlace com a organização.

Outra forma de ataque  recursos de sistema usa pacotes cuja estrutura aciona um bug no software de tratamento de rede do sistema, causando sua interrupção. Isso significa que o sistema não pode mais se comunicar pela rede ate esse software ser reativado, em geral mediante a reinicialização do sistema-alvo. Isso é conhecido como pacote envenenado.
Um ataque a uma aplicação especifica, como um servidor Web normalmente envolva varias requisições validas, cada uma das quais consome recursos significativos. Então isso limita a capacidade do servidor de responder a requisições

Os clássicos ataques do Ping da Morte é da lágrima, dirigindo a sistemas windows (antigos e atuais), assumiam essa forma. Eles visavam bugs no código de rede do Windows que tratava.

### Inundações HTTP
Requisições HTTP de muitos bots diferentes podem ser projetadas para consumir recursos consideráveis. 
### Ataques de largura de banda baseados em Aplicação
Uma estratégia potencialmente efetiva para a negação de serviço é forcar o alvo a executar operações que consomem recursos de forma desproporcional ao esforço do ataque.
Ex: Sites da web podem dedicar-se a operações longas como buscas, em resposta a uma requisição simples. `SELECT * FROM + join + WHERE` 
### Slowloris 
Servidores web utilizam threads para dar suporte a varias requisições. esse ataque tenta monopolizar todas as threads de tratamento de requisição disponíveis no servidor web, enviando requisições HTTP que nunca são concluídas. Visto que cada requisição consome um threads, a certa altura o ataque Slowloris consome toda a capacidade de conexão dos servidor Web, efetivamente negando acesso a usuários legítimos.

## Ataques Refletores e Amplificadores 
O atacante envia um pacote de rede com endereço de origem falsificado a um serviço que e executado em algum servidor de rede. O servidor responde a esse pacote enviando-o ao endereço de origem falsificado que pertence ao alvo do ataque propriamente dito. Se o atacante enviar varias requisições a vários servidores, todas com o mesmo endereço de origem falsificado, a inundação de respostas resultante pode sobrecarregar o enlace de rede do alvo. 
Há duas variantes básicas desse tipo de ataque: o ataque de reflexão simples e o ataque de amplificação.
### Ataques de reflexão
O atacante envia pacotes a um serviço conhecido intermediário, com endereço de origem falsificado do sistema visado. Quando o intermediário responde, a resposta é enviada ao alvo. Efetivamente, isso causa a reflexão do ataque no intermediário, que é denominado refletor, e é por isso que esse ataque é denominado ataque de reflexão.
### Ataques de Amplificação
Também envolvem enviar a intermediários um pacote com o endereço de origem falsificado do sistema alvo. Eles diferem na geração de vários pacotes de resposta para cada pacote original enviado. Isso pode ser conseguido dirigindo a requisição original ao endereço BroadCast de alguma rede. O resultado é que todas as estações nessa rede podem potencialmente responder a requisição, gerando uma inundação de respostas.

## Defesas contra ataques de Negação de Serviços.
É importante reconhecer que esses ataques nao podem ser interiramente evitados. Se um atacante puder dirigir um volume de trafego legitimo suficintemente grande ao seu sistema, existe alta chance de que ele sobrecarregará a conexão de rede do seu sistema, e assim, limitará requisições de tráfego legitimas vindas de outros usuários.
Em geral, há quatro linhas de fegeas contrar ataqeus DDoS:
- Prevenção e preempção de ataque (Antes do ataque)
- Detecção e filtragem de ataque (durante o ataque)
- Rastreamento retroativo e identificação da fonte
- Reação ao ataque

---
# 11/05
## Web Hacking 
### Local File Inclusion
permite e inclusão de arquivo para explorar o mecanismo _Dynamic File Inclusion_ Implementando na aplicação web abaixo.
### Remote File inclusion
é o processo de inclusão de arquivos remoto, atravésda exploração dos processos de inclusão de vulnerabilidades.
### Comand Injection
A injeção de comando é um ataque em que o objetivos é a execução de comandos arbitrarios no sistema operacional alvo por meio de um aplicativo vulnerável
São possíveis quando um aplicativo passa dados não seguros fornecidos pelo usuário (formulários, coockies, cabeçalhos HTTP etc.) para um shell.
### File Upload 
Vulnerabilidade presente em serviço web que permite uploads negligentes de arquivos maliciosos.
O atacante poderá enviar arquivo contendo instruções maliciosas diversas.
### Brute Force
Método  exaustivo (tentativa e erro) utilizado para decodificar dados confidenciais (ex: arquivos criptografados) ou identificar credenciais de autenticação.
São ataques relativamente simples de executar e, se houver tempo suficiente e nenhuma estrategia de mitigação para o alvo, possuem considerável probabilidade de sucesso.
O que diferencia os ataques de forca bruta de outros métodos de quebra de segurança é que os ataques.
**Ferramentas**
#### Hydra
Ferramenta para descoberta de credenciais por meio de forca bruta.

### SQL-Injection
Linguagem padrão universal para a manipulação de bancos de dados relacionais. Utilizada, dentre outras tarefas de linguagens relacionais.
### Blind SQL-Injection
Nem sempre o servidor alvo responde iterativamente as injeções do usuário. Por isso chamados _SQL Injection Cega_.

### Cross Site Scripting (XSS)
Tipo de ataque de injeção de código malicioso em aplicações web. Através de um XSS, o hacker injeta códigos JavaScritp em um campo de texto de uma página e este JS é executado pelo navegador do usuário. Em geral o ataque acontece em função de falha na validação dos dados de entrada do usuário e a resposta do servidor Web.
Existe três tipos de CSS
**Persistenete:** O script injetado pelo atacante fica alojado de forma permanente no servidor de destino.
**Não Persistente:** O script nao fica alojado em um servidor de destino e por isso precisará ser entregue para cada vitimi (ex: Engenharia social ou um resultado de busca). Ao acionar o servidor, por meio do link, o script 
**Refletido:** 

---
# 18/05

## Comparativo 
Redes cabeadas nao utilizam nenhum recurso especial de seguranca, mas, mesmo assim, os dados são protegidos. O motivo é simples: tudo se passa dentro do cabo.

## Segurança
nem sempre é possivel evitar que as informações em redes sem fio sejam capturados. O que pode ser feito é criptografar, ou seja, transmitir as informações de tal forma que , mesmo que eleas sejam capturadas, não possam ser compreendidas.
Esse trabalho é feito por protocolos de segurancas qeu codificam os dados que navegam entre o PC e o roteador para impedir ...

## Protocolos 
### WEP
WIred Equivalent Privacy ou privacidade equivalente a de redes com fios
### WPA
Wi-Fi Protected Acess ou Acesso sem fio protegido.

## WEP - Wired Equivalent Privacy
Utiliza o algoritmo RC4 (cifra simetrica de fluxo) para criptografar os pacotes em redes sem fio. Implementa função detectora de erros que verifica se a mensagem recebida foi corrompida ou alterada no meio do caminho.
O próprio algorimo de criptografia RC4 foi apontado como o principal calcanhar de Aquiles do protocolo, e mesmo sendo indiadas outras opções para substitui-lo, o WEP caiu em descrédito e deixou de ser usado em aplicações sérias.
Desde 2004 o WEP é considerado "obsoleto". Apesar de estar obsoleto, muitos roteadores ainda trazem o WEP como opção, e alguns usuários ainda fazem uso do WEP devido à compatibilidade.
O WEP utiliza algoritmo de criptografia simétrica (RC4), portanto, existe uma chave secreta que deve ser compartilhada entre as estações de trabalho e o concentrador, para cifrar e decifrar as mensagens trefegadas.
Em outras palabras, cada computador de uma rede receve a mesma chave que está configurada no ponto de acesso sem fio, descrito como concentrador. A chave serve para cifrar uma mensagem enquanto ela é transmitida da base (roteador) para o computador ou vice-versa.
### Falha na WEP
O WEP utiliza o RC4, que é um codificador de fluxo, o que siginifica que a chave para criptografar os dados deve estar, pelo menos teoricamente, em constante mutação.
A solução veio da seguinte maneira: a chave criptografica, usada pelo WEP, é composta por dois itens:
- uma chave.
- Um componente chamado _Initialization Vector_, que acompanha essa chave.
Esse vetor de inicialização é permutado constantemente, oi seja, a cada transmissão temos um novo conjunto do vetor de inicialização, capturar as mensagens em que ele.
Programas como o _aircrack-ng_ fazem isso em questão de minutos. Este possui métodos de burla do sistema.

## WPA - (Wi-Fi Protected Access)
Surgiu a partir de um esforço conjunto de membro da Aliança Wi-Fi e do IEEE para combater algumas das vulnerabilidades do WEP e aumentar o nivel de seguranca das redes sem fio.
Lançado em 2003, utilizava criptografia TKIP (substituição do vetor de inicialização de 24 bits para 48 bits) era comumente chamado de WEP2.
Em 2004 receveu atualização, adotando o algoritmo de cifra de bloco.
Existem dois métodos de operçaão.
- **Uso doméstico PSK** _(Pre-Shared Key)_: Chave previamente compartilhada é utilizada.
- **Grandes Organizações**: Não depende de uma chave previamente compartilhada. Utiliza servidores de autenticação para validarem a conexão (ex: Eduraom/UFT).
É considerada o padrão mais seguro atualmente e deve ser utilizado sempre que possivel.
### Segurança no WPA/WPA2
Técnicas de ataque aos padrões WPA/WPA2 exogem frequentemente a atualização de dicionarios. Um ataque de dicionário é um método que consiste em invadir um computador ou servidor protegido por senha (neste caso, uma rede Wi-Fi) inseridno sistematicamente cada palavra em um dicionário.
### Ataques em Redes Wireless
#### Modos operacionais de adaptadores sem fio
- **Modo managed (Gerenciado):** Interface de rede Wi-Fi ignora todos os pacotes de dados , exceto aqueles especificamente endereçados a ela.
- **Modo Monitor (Promiscuo):** O adaptador Wi-Fi captura todo o tráfego da rede sem fio(em um determinado canal Wi-Fi) independentemente do destino. Pode capturar pacotes sem sequer estar conectado a qualquer ponto de acesso. É um agente livre farejando e bisbilhotando todos os dados no ar.
[AirCrack-ng ](https://www.aircrack-ng.org)
Conjunto de ferramentas para avaliar seguranças de redes Wi-Fi.
- airmon-ng
- airodump-ng
- aireplay-ng
- aircrack-ng

### Identificando...
identificando  modo de operação do adaptador wireless:
```shell
iwconfig wlan0
```

### Modo monitor
``` terminal
sudo airmon-ng check
sudo airmon-ng check kill
sudo airmon-ng start wlan0
```
Identificando redes wifi ao alcance.
```terminal
sudo airodump-ng wlan0mon
```

### Quabrando redes com criptografias WPA2
Ao contrario do WEP nao existe uma metodologia tao simples e direta para a obtenção da senha.
AES - seguro e eficiente. Uso recomendável para quem desejava alto grau de permissão.

```terminal
sudo airodump-ng -c 11  --bssid 14:5B:D1:47:0E:04 -w arquivo_captura_wpa2 wlan0mon
```


## Fake Access Point
Técnica que visa a criação de um falso Acess Point, imitando as configurações básicas de uma rede alvo. Também conhecidos como _Rougue Acess Point_.
### Evil Twin
Consiste na clonagem de um Access Point verdadeiro. Depois busca forcar os clientes conetados ao AP verdadeiro a se desconectarem e em seguida conectar ao nosso Evil Twin.

---
# 25/05

## Buffer
buffer e uma seção continua de memoria que armazena dados. Problemas surgem quando tentamos colocar mais dados no buffer do que ele pode acomodar (capacidade)
Quando um programa renta colocar mais dados em um buffer ele substitui os locais de memoria adjacentes.
Criar um buffer e uma tarefa relativamente simples para desenvolvedores. Basta definir um array de determinado tamanho. Um exemplo em linguagem C pode ser o seguinte: 
`char buffer[8]`
Se excedermos a capacidade do `buffer[8]` poderemos alcançar partes da memoria que leem o código executável em um endereço especifico.

### Buffer Overflow
Condição na qual um buffer recebe uma quantidade de entrada maior do que a capacidade alocada, sobrescrevendo outras informações .
Essas posições poderiam conter outras vaiareis, parâmetros ou controles de fluxo de dados, como endereços de retorno e ponteiros para estruturas de pilha anteriores.
As consequências desse erro incluem corrupção de dados pelo programa, transferências  inesperada de controle no programa, possíveis violações de acesso à memoria e muito provavelmente, a eventual finalização do programa.

Computadores gerenciam pulha atraves de registradores. Em arquiteturas 64 bits os registradores RSP(Register Stack Point) e RBP(Register Base Point) são especialmente importantes.

Muitas funçõe s de biblioteacas comuns e amplamente usadas especialmente as relacionadas a entrada de processamento de cadeias de caracteres, não executavam verificações do tamanho dos buffers sendo usados.

O grau de seriedade disso dependará muito da estrutura lógica do programa atacado. Para explorar o atacante precisa:
- identificar uma vulnerabilidade de estouro de capacidade de um buffer em algum programa, a qual possa ser acionada usadno dadaos fornecidos por uma fonte externa sob o controle dos atacantes.
- Estender, como esse buffer sera armazenado na memória de processos e, portanto, o potencial  de execução.
Para fins didáticos,, faz se necessario desativar o _Adressing space layout Randomization (ASLR)_. O ASLR seleciona aleatoriamente onde os dados associadso ao programa estao na memoriam dificultando a determinação de onde as coisas estão localizadas e como vamos assumir o controle do programa.
Para desativar o ASLR:
`echo 0 > /proc/sys/kernel/randomize_va_space`

## GDB (Gnu Debbuger)
Permite depurar (monitorar em nicel mais refinado) aplicativos.
`gdb -q [nome do Programa]`


### Exemplo Real - ChimayRed
CIA(NSA) Hacking Toolds Revealed
Exploit utilizando contra roteadores Mikrotik executando sistema operacional RouterOS. Usado para enviar Payload (TinShell) para o roteador.

