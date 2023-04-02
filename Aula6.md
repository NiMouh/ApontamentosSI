# Aula 6

## Cifra Autenticada
O conceito basea-se na implementação da combinação, de alguma forma, de cifragem e código de autenticação da mensagem. As **três formas possíveis** de combinar os dois mecanismos são:
 1. *MAC and Encrypt*: Processo de calcular o MAC da mensagem, cifrar a mensagem e concatenar o criptograma com o MAC (e.g. *SSH*);
 2. *MAC then Encrypt*: Processo de calcular o MAC da mensagem, concatená-lo à mensagem e cifrar o resultado desta operação (e.g. *TLS*);
 3. *Encrypt then MAC*: Processo de cifrar a mensagem, calcular o MAC do criptograma e concatenar os dois (e.g. *IPSec*);

Nota: A forma considerada correta é a terceira, já que a inclusão do MAC não degenera nunca o vazamento de informação.

## Criptografia de chave pública
A criptografia de chave pública moderna é baseada na teoria dos números e em problemas difíceis de resolver. Alguns exemplos são os protocolos de acordos de chaves, assinaturas digitais e cifras de chave pública.

Exemplos de **problemas intratáveis** com mais relevância:
 - O problema do **logaritmo discreto**;
 - O problema da **fatorização de números compostos** em números primos;

### Problema do logaritmo discreto
Consiste em encontrar o valor de um **número inteiro** (exponencial) que é utilizado para cifrar uma mensagem, conhecido o valor da base e o resultado da exponenciação, num grupo finito. Esse problema é considerado difícil de resolver computacionalmente quando se trabalha com números grandes, tornando-o fundamental para garantir a segurança da criptografia de chave pública.

Nota: A definição mais geral do problema recorre apenas a grupos cíclicos, aplicando-se, por isso a outros grupos diferentes de números primos. O melhor algoritmo conhecido para resolver o problema do logaritmo discreto é conhecido por *general number field sieve*, determinando o tamanho que o número tem de ter para que o problema seja considerado seguro.

### Problema da fatorização de números compostos
Consiste em decompor um número composto nos seus **fatores primos**. Por exemplo, se tivermos o número 15, ele pode ser decomposto em 3 e 5, que são números primos. O problema da fatorização torna-se difícil à medida que os números tornam-se maiores, e isso é utilizado em **esquemas de criptografia de chave pública** baseados em algoritmos como o **RSA**. A segurança desses esquemas depende do fato de que a fatorização de números grandes em fatores primos é **computacionalmente difícil** de ser realizada em tempo razoável, tornando a criptografia de chave pública segura contra ataques de criptoanálise.

## Protocolos de acordos de chaves
Neste capítulo é apresentado formas de trocar ou estabelecer um segredo entre duas entidades sem haver nada **secreto** acordado à partida. Essa troca é realizada por uma comunicação segura, aonde as partes enviam mensagens encriptadas uma para a outra e usam técnicas de criptografia e matemática para garantir que apenas elas possam obter a chave secreta compartilhada. O objetivo é garantir a segurança e a privacidade das comunicações entre as partes envolvidas.