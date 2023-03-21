# Aula 4

## *Cipher Block Chaining Mode* (CBC) - Continuação

### *Randomized Couter Mode* (CTR)
O **CTR** é um modo de operação de cifra que consiste em cifrar através de uma chave de cifra de forma simétrica e continua a partir de uma cifra de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-limpo e o contador;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-cifrado e o contador;

Nota: Sendo ela uma cifra de chave simétrica contínua, ela fica **maneável**.

### Exemplos canónicos
Estes são alguns exemplos de cifras de chave simétrica por bloco:
 - Data Encryption Standard (DES)
 - Triple Data Encryption Standard (3DES)
 - Advanced Encryption Standard (AES)

## *Deterministic Counter Mode* (DCTR)
O **DCTR** é um modo de operação de cifra que consiste em cifrar através de uma chave de cifra de forma simétrica e continua a partir de uma cifra de blocos. A diferença para o **CTR** é que o **DCTR** é determinístico, ou seja, o contador é gerado a partir de uma função determinística (e.g. contador + 1).

Nota: Não é recomendado este modo de operação de cifra.

### *Output Feeback Mode* (OFM)
### *Ciphertext Feedback Mode* (CFM)

## Principio de Rack-off
O **princípio de Rack-off** é um princípio de segurança que consiste em que a chave de cifra é a única informação que deve ser mantida em segredo. Ou seja, se o algoritmo for conhecida, o atacante não deve conseguir descobrir o conteúdo da mensagem cifrada.

## Redes feistel
São funções sempre **invertíveis**, mas construídas a partir de funções que podem não ter inversa. É uma forma engenhosa de construir funções pseudoaleatórias (PRFs) e permutações pseudoaleatórias (PRPs).

A redes funciona na seguinte forma:
 - Recebe um bloco de texto-limpo;
 - Divide o bloco em duas partes (R0 e L0);
 - Aplica uma função f sobre R, aplica o xOR dela com L e obtém R1;
 - O R0 transita para L1;
 - O processo repete-se 'n' vezes;

Nota: Rackoff também refere que para uma PRP (*Pseudo random permutations*) ser segura, a rede de feistel tem de ser com **pelo menos três** rondas.

## Agente de confiança
É um agente que garante a autenticidade de uma mensagem. É um intermediário entre o emissor e o receptor da mensagem. O agente de confiança garante que a mensagem não foi alterada durante o seu transporte por um **canal seguro**.