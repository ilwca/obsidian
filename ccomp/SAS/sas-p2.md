1) Ataque de negação de serviço (ddos)

R: Nao sendo considerado um metodo de invasao e sim uma forma de comprometer a disponibilidade de um certo serviço, tentando esgotar um recurso critico, mas diferente do dos, faz o uso de varios sistemas para gerar atques, esses sitemas eram tipicamente estaçoes de trabalho ou PCS comprometidos de usuarios (zumbis)

2) Estouro de buffer → Foto para identificar o problema e falar sobre ele

R: um estouro de buffer ocorre quando um programa tenta gravar dados alem do que o buffer de memoria permite, assim sobrecarrega o sistema, bufer é uma seçao contnua de memoria que armazena dados, problemas surgem quando etntamos colocar mais dados no buffer do que ele pode acomodar. Quando um programa tenta colocar mais dados, ele substiiu locais de memoria adjacentes, sendo assim pode perder informaçoes ou da a possibilidade de executar outras tarefas.

3) Explicar o seguinte

a)WEP 

R: WEP é um protocolo de rede sem fio, foi o pioneiro no assunto , opera na camada de enlance de dados, utiliza o algoritimo RC4 para criptografia, sendo um algoritmo de cifra simetrica de fluxo, sendo esse mesmo algoritmo foi apontado como principal causa da falha desse protocolo

b) WAP/WPA2 

R: Protocolo que veio para substituir o WEP, melhorando sua segurança, substituindo o vetor de 24bits para 48 e logo depois mudou o metodo de criptografia para o algoritmo AES utilizando cifragem simetrica de bloco.

c) Fake Acess Point e Evil Twin

Fake Acess Point - cria um falso ponto de acesso, imitando configurações basicas da rede alvo, com o objetivo de enganar usuários e interceptar seus dados. 

Evil Twin - consiste na clonagem de um acess point valido, com todos os detalhes de ip, mac, bssid, canal e criptografia, depois basta forcar os clientes conectados ao access point verdadeiro e se desconectarem e em seguida conectar ao Evil Twin

Ataque que consiste em obter informações sem o conhecimento do
usuário, fazendo ele acreditar que está se conectando a um hotspot com
um sinal
forte. Na realidade, o usuário pode estar se conectando a um servidor
malicioso que
pode monitorar e obter os dados digitais do usuário.

4) É possível obter 100% do código de original a partir de um executavel binário?

Na maioria das vezes nao é possivel, por que muita informação é perdida durante o processo de compilaçao, nomes de metodos, funcoes, variaveis, porem é possivel determinar o comporamento do binario e ate mesmo produzir um codigo fonte que funcione de maneira equivalente 

5) Ataque XSS Refletido 

R: um ataque de XSS consiste em que o invasor insere um script em uma aplicaçao web em um campo de texto d pagina e esse script é executado no navegador do usuario.

o persistente fica alojado no servidor de destino e todos os usuarios que entrarem na pagina irao ver oque o script faz

Já o refletido o script nao fica alojado em um servidor de destino, por isso precisa ser entregue a cada vitima e

Baseado em DOM: explora o document object model (DOM), que é a
interface que define a leitura de HTML e XML no navegador. o script é
capaz de alterar as propriedades das aplicações diretamente no
navegador, portanto, sem necessidade de interação com o servidor para
performar o ataque.

6) SQL injection

R: Ocorre quando dados nao confiaveis sao inseridos diretamente em uma instruçao, sql sem validaçao adequada, invasores podem explorar essa falha, inserindo dados que alteram a logica da consulta, permitindo a execucao de comandos nao autorizados. O objetivo é manipular a consulta SQL original para executar comandos indesejados, como acessar, modificar ou excluir dados armazenados no banco de dados da aplicação.

podendo mostrar dados de uma tabela inteira 

## Ataques de reflexão

- O atacante envia pacotes a um serviço conhecido no intermediário, com endereço de origem falsificado do sistema visado. quando o intermediário responde, a resposta é enviada ao alvo. Efetivamente, isso causa a reflexão do ataque no intermediário, que é denominado refletor, e é por isso que esse ataque é denominado ataque de reflexão.

## Ataque de amplificação

- Também envolvem enviar a intermediário um pacote com o endereço de origem falsificado do sistema alvo. Eles diferem na geração de vários pacotes de resposta para cada pacote original enviado. Isso pode ser conseguido dirigindo a requisição original ao endereço de broadcast de alguma rede.
- O resultado é que todas as estações nessa rede podem potencialmente responder a requisição, gerando um inundação de respostas.

## *Vulnerability: File Inclusion*

- permite a inclusão de arquivo para explorar o mecanismo dynamic file inclusion implementando na aplicação alvo
- Atacante pode passar qualquer valor para o parâmetro da aplicação alvo e a mesma não faz a validação correta do valor informado antes de executar a operação.
- Aplicação web poderá vir a apresentar o conteúdo de determinados arquivos (vazamentos de informações sensíveis).
- Ocorre, por exemplo , quando uma página recebe como entrada, o caminho para o arquivo que será incluído, e esta entrada nao é validade de forma correta, possibilitando assim que caracteres de Directory Traversal (../../)sejam injetados.

## *Vulnerability: Remote File Inclusion*

- É o processo de inclusão de arquivos remotos, através da exploração dos processos de inclusão vulneráveis, implementados na aplicação web alvo.
- Esta falha ocorre, por exemplo, quando uma página recebe como entrada, caminho para o arquivo que será incluído, e esta entrada não é validada de forma correta pela aplicação web, permitindo assim que uma URL externa seja injetada na aplicação alvo.

### Command Injection

- A injeção de comando é um ataque em que o objetivo é a execução de comandos arbitrários no sistema operacional alvo por meio de um aplicativo vulnerável
- São possíveis quando um aplicativo passa dados não seguros fornecidos pelo usuário (formulários, cookies, cabeçalhos HTTP etc.) para um shell do sistema
- Os comandos fornecidos são geralmente executados com os privilégios do aplicativo vulnerável (elevation of prileges pode ser necessário).

### *Vulnerability: File Upload*

- Vulnerabilidade presente em serviços web que permitem uploads negligentes de arquivos maliciosos.
- o atacante podera enviar arquivo contendo instruções maliciosas diversas (ex.: rever shell ou bind shell)
- Criar o arquivo dvwa-file-upload.php:

## File Upload

---

- vulnerabilidade presente em serviçoes web que permitem uploads negligentes de arquivos maliciosos.
- (ER) reside logo após o endereço do ponteiro de base de pilha($RBP)
- $RBP = Base point/Aponta para final do quadro de pilha
- $RSP = Source Pointer/ Aponta para inicio do quadro de pilha.
- $RIP = instruction pointer/aponta para a próxima instrução a ser executada.

RSP (Register Stack Point) e RBP (Register Base Point) são registradores usados em arquiteturas
de processadores para controlar o uso da pilha de memória durante a execução de um programa.

O RSP mantém o ponteiro para o topo da pilha, enquanto o RBP mantém o ponteiro para a base
da pilha. Esses registradores são importantes para garantir que as chamadas de função, alocação
de memória e outras operações relacionadas à pilha sejam executadas corretamente.

Esses registradores têm funções específicas no gerenciamento da pilha e do fluxo de execução de programas em sistemas de 64 bits. Vamos detalhar cada um deles:

### $RBP (Base Pointer)

- *Função*: O registrador $RBP, também conhecido como "Base Pointer" ou "Frame Pointer", é utilizado para apontar para a base do quadro de pilha (stack frame) da função atual em execução.
- *Uso Típico*: Durante a entrada em uma função, o valor do $RBP é salvo na pilha e $RBP é atualizado para apontar para o início do novo quadro de pilha. Isso facilita a navegação entre variáveis locais e parâmetros da função, pois esses valores têm deslocamentos fixos relativos ao $RBP.

### RSP (Stack Pointer)

- *Função*: O registrador $RSP, ou "Stack Pointer", aponta para o topo da pilha. A pilha é uma estrutura de dados LIFO (Last In, First Out) usada para armazenar dados temporários, como variáveis locais e endereços de retorno.
- *Uso Típico*: $RSP é automaticamente atualizado pelas instruções que empilham (push) ou desempilham (pop) valores. Modificações explícitas a $RSP são menos comuns e geralmente são feitas para ajustar a alocação de espaço na pilha.

### $RIP (Instruction Pointer)

- *Função*: O registrador $RIP, ou "Instruction Pointer", contém o endereço da próxima instrução a ser executada. Ele é fundamental para o controle do fluxo de execução de um programa.
- *Uso Típico*: $RIP é automaticamente incrementado conforme as instruções são executadas. Instruções de controle de fluxo, como chamadas de função (call), saltos (jump) e retornos (return), alteram diretamente o valor de $RIP.

d) O que é Endereço de Retorno?
O Endereço de Retorno é um valor armazenado na pilha de memória que indica o local para onde
um programa deve retornar após a conclusão de uma função ou rotina. Durante a execução do
programa, quando uma função é chamada, o endereço de retorno é colocado na pilha para que
o programa saiba para onde retornar depois que a função for concluída. No contexto de um
ataque de estouro de buffer, um atacante pode manipular o endereço de retorno para
redirecionar o fluxo de execução para um local arbitrário na memória, permitindo a execução de
código malicioso.