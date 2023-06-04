# Aula 11

## Levantamento de informação arquitetural
A **informação arquitetural** consiste na descrição das máquinas que fazem parte de uma rede e qual a função que nela desempenham.

Nota: Uma das principais fontes de informação é o **DNS**. Pois mesmo que não debite mais informação do que o seu serviço principal permite, é possível obter nomes dos endereços de IP que sabemos para induzirmos a sua função na rede.

### DNS
O procedimento de um atacante seria o:
 - **IP Sweep**: Consiste em fazer um varrimento de IPs para identificar os que estão ativos (e.g. `nslookup -type=A www.di.ubi.pt`).
 - **DNS Sweep**: Consiste em fazer um varrimento de nomes de domínio para identificar os que estão ativos (e.g. `nslookup 192.168.1.253`).

## Resolução de endereços
Um serviço DNS (ou Domain Name System) é um serviço que permite a resolução de nomes de domínio em endereços IP e vice-versa, pois é mais fácil de memorizar um nome do que um endereço IP.

Funciona no seguinte modo:
 1. O cliente **envia um pedido** ao servidor DNS para resolver um nome de domínio.
 2. O servidor DNS **responde com o endereço IP** correspondente ao nome de domínio.
 3. O cliente **aceita** o endereço IP e estabelece a ligação com o servidor desejado.

Isto pode trazer as seguintes vulnerabilidades:
 - **Spoofing**: Consiste em fazer-se passar por um servidor DNS para redirecionar o tráfego para um servidor malicioso.
 - **Cache Poisoning**: Consiste em alterar o conteúdo da cache de um servidor DNS para redirecionar o tráfego para um servidor malicioso.
 - **DNS Hijacking**: Consiste em direcionar o tráfego para um servidor DNS controlado pelo invasor.
 - **DNS Tunneling**: Consiste em utilizar o protocolo DNS para enviar dados para fora da rede.

## Confidencialidade

### Confidencialidade de Interações em Rede
Pode ser vista de dois modos diferentes:
 - No tráfego de rede: Consiste em esconder o emissor e o receptor final.
 - No conteúdo do tráfego: Consiste em esconder dados úteis trocados entre o emissor e o recetor.

#### *Peer-to-Peer* (P2P)
É um modelo de rede em que todos os nós são iguais e podem funcionar como cliente e servidor ao mesmo tempo (e.g. BitTorrent).

### Captura de palavras-passe
O risco pode ser reduzido através de soluções como:
 1. **Cifrar** as comunicações.
 2. **Usar** palavras-passe fortes (evita ataques de dicionário) e únicas (evita ataques de reutilização).
 3. **Usar** protocolos de troca de desafios e respostas (e.g. CHAP).


## Autenticidade
Pode ser vista de dois modos diferentes:
 - De interlocutores (emissor e recetor): Consiste em garantir que o emissor e o recetor são quem dizem ser.
 - De conteúdo: Consiste em garantir que o conteúdo não foi alterado.

Existem vulnerabilidades a explorar aqui. Nisto temos técnicas de efetuar o controlo de acesso em redes IP's:
 - Pedidos fraudulentos sobre UDP: Consiste em enviar um pedido UDP com um endereço IP de origem forjado (*spoofed*).
 - Iniciação fraudulenta de ligações TCP: Consiste em mandar um pedido TCP SYN com um endereço IP de origem forjado (*spoofed*), o receptor irá responder com um TCP SYN-ACK para o endereço IP forjado, e emissor intermediário (Claire) irá mandar um ACK para o receptor, estabelencendo assim a comunicação. Caso conttrário, o emissor irá responder com um TCP RST para o endereço IP forjado.
 - Redirecionamento de tráfego (ICMP Redirect): Consiste em enviar um pedido ICMP Redirect com um endereço IP de origem forjado (*spoofed*), o emissor irá atualizar a sua tabela de rotas e passar a enviar os pacotes para o endereço IP forjado.
 - Redirecionamento de tráfego (Source Route): Consiste em inverter a rota definida no pacote IP, um atacante pode então enviar um pacote IP com um endereço IP de origem forjado (*spoofed*) e com uma rota definida para o endereço IP forjado, o emissor irá enviar o pacote para o endereço IP forjado.

## Ataques de negação de serviço
Um ataque de negação de serviço (os DoS) consiste em impedir o acesso a um serviço por parte de utilizadores legítimos. 

Usando técnicas como:
 - **Exploração de vulnerabilidades**: Consiste em explorar vulnerabilidades de um serviço para o tornar indisponível.
 - **Inundação dos servidores**: Consiste em inundar os servidores com pedidos para os tornar indisponíveis. Isto acontece nos servidores onde o atacante pode usar os seus serviços à **discrição**, usem o **protocolo UDP** para troca de mensagens, gerem respostas **maiores** que perguntas (e.g. pedir a um servidor DNS toda a informação que ele tem de um determinado endereço).
 - **Inundação da rede de acesso**: Consiste em inundar a rede de acesso com tráfego para tornar os servidores indisponíveis.

A **amplicação** dos ataques é antigida de duas formas:
 - **Uso** de *Botnets*;
 - **Uso** de mecanismos de amplificação de tráfego.

## *Botnets*
É uma rede de computadores infetados com software malicioso que permite ao atacante controlar os computadores infetados remotamente (e.g. Mariposa).

## Ataque *Smurf*
Basea-se no **envio de pacotes** ICMP Echo Request para um endereço de broadcast com o endereço IP de origem forjado (*spoofed*).

## Ataque *Fraggle*
Semelhante ao ataque *Smurf*, mas basea-se no **envio de pacotes** UDP Echo Request para um endereço de broadcast com o endereço IP de origem forjado (*spoofed*).

## Solução parcial do *IP Spoofing*
Possível solução seria definir e concretizar as políticas de segurança em routers e switches, de modo a não deixarem fazer difusão para dentro da rede. Caso o *IP Spoofing* não fosse possível, nenhum atacante poderia efetuar um ataque a uma vítima **remota**.

Outras medidas que podem ajudar a diminuir o risco seria:
 - **Desativar serviços** desnecessários;
 - **Limitar o número de pedidos atentidos** por segundo;
 - Não permitir transferência de zona DNS;


## Resolução da prática 11
1. 172.29.25.9/20
2. Sim, tem endereço IPV6
3. 10.0.2.0
4. /24 especifica a gama de endereços IP's que podem ser atribuídos a dispositivos na rede. O /24 significa que os primeiros 24 bits são usados para identificar a rede e os restantes 8 bits são usados para identificar os dispositivos na rede.

### Tarefa 2
Comando: `nmap -sn <endereço-de-rede/IP>`

5. A flag `-sn` é usado para realizar um ping sweep.
6. Enviando pacotes Internet Control Message Protocol (ICMP) do tipo echo request para todas as máquinas e considerando que estão ligadas aquelas para que recebe uma resposta.
7. Eh.. sim,tomei.
8. Sim, consigo, o gateway.

### Tarefa 3
`-sX` - TCP Xmas Scan

`-vv` - Verbose

`-O` - OS detection

11. As sequências são previsíveis.
13. O sistema operativo é da famila Linux.
14. Localhost é o endereço IP 127.0.0.1. É usado para se referir ao próprio computador.
15. 
