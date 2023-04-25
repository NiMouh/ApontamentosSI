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


## Resolução da ficha prática 5

### Tarefa 1
Comando para obter a hash de um ficheiro (MD5):
```console
$ openssl dgst -md5 ficheiro.txt
```

Comando para obter a hash de um ficheiro (SHA1):
```console
$ openssl dgst -sha1 ficheiro.txt
```

1. Os valores são iguais.
2. Que, neste caso, o ficheiro que chegou à minha máquina foi o mesmo que o emissor enviou.
3. Ron Rivest foi quem inventou o MD5.
4. Sim, já conhecia pelo menos outra obra dele, o RSA.
5. MD5 tem 128 bits, SHA1 tem 160 bits.
6. A letra S do acrónimo SHA significa *Secure*.
7. A letra D do acrónimo MD significa *Digest*.

### Tarefa 2
Comando para obter a hash de um ficheiro (MD5):
```console
$ openssl dgst -md5 ficheiro.txt
```

Comando para obter a hash de um ficheiro (SHA1):
```console
$ openssl dgst -sha1 ficheiro.txt
```

8. O valor da hash MD5 é diferente.
9. Creio que alguém me quis enganar.
10. A função de hash tem como utilidade a integridade dos dados e a identificação de possíveis alterações/burlas.
11. Contém um ficheiro ISO e o hash correspondente.

### Tarefa 4
Comando para obter a hash de uma string vazia (MD5):
```console
$ echo -n "" | openssl dgst -md5
```

12. Os valores de hash ficaram totalmente diferentes.
13. Mudaram aproximadamente 50% dos bits.
14. Obtínhamos exatamente o mesmo comportamento que observamos quando mudamos 1 só byte
15. Sim, consigo notar uma relação entre a alteração de qualquer byte e vários bits do valor de hash, mas é muito muito complexa, e só a minha cabeça é que consegue perceber essa relação.
16. Não estou a ver como iria fazer isso para já, mas creio que iria conseguir.
17. A propriedade referida na pergunta anterior é a resistência à descoberta de um segundo texto original.
18. Não seria possível arranjar dois ficheiros diferentes com o mesmo SHA1 em tempo útil pois o SHA1 tem 160 bits, o que significa que existem 2^160 possibilidades, o que é muito difícil de ser calculado.
19. A propriedade referida na pergunta anterior é a resistência a colisões.
20. Sim, é `pedro`.
21. Não, porque não protege contra ataques que usam rainbow tables ou tabelas de hash précomputadas. Ora bolas!

## Fim da aula 4
Link para a [Aula anterior](Aula3.md)

Link para a [Próxima aula](Aula5.md)

Link para os [CheatSheets](CheatSheet.md)
