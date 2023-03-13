# Aula 3

## Modelos de ataque
Para testar a qualidade de uma cifra, é necessário testar a sua resistência a ataques. Para isso podemos fazer um jogo onde temos **dois personagens**:

**Desafiador**: Começa por escolher uma chave gerada aleatoriamente e cifra uma mensagem com essa chave. A mensagem cifrada é enviada ao **Concorrente**.

**Concorrente (Adversário)**: Adivinhar qual a mensagem foi cifrada pelo **Desafiador**.

Nota: A força criptográfica aceite hoje em dia é de, pelo menos, 80 bits.

## Tipos de ataques
Alguns exemplos dos tipos de ataques mais comuns:

### Ataque força bruta (Brute force)
É uma técnica de ataque que consiste em tentar todas as possíveis chaves de cifra até encontrar a chave correta.

### Ataque com conhecimento de texto-limpo original (Known plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra a partir de um texto-limpo original e do texto-cifrado correspondente.

### Ataque com o conhecimento apenas do criptograma (Ciphertext-only attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo, a partir de um texto-cifrado.

### Ataque com o texto-limpo original escolhido pelo atacante (Chosen plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um texto-limpo original escolhido pelo atacante.

### Ataque com o texto-limpo original escolhido pelo ataque adaptativo (Adaptative Chosen plaintext attack)
Semelhante ao anterior, porém o atacante obtém exemplos de texto cifrado antes e depois de começar o ataque.

### Ataques com criptogramas escolhidos pelo atacante (Chosen ciphertext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um conjunto de textos-cifrados escolhidos pelo atacante, diferentes do texto que queremos cifrar.

Nota: Não é uma técnica de criptanálise.

### Ataque do homem no meio
Este tipo de ataque é feito quando a **Pessoa A (Alice)** e a **Pessoa B (Bob)** estão sujeitos a um ataque por uma **Pessoa C (Claire)** que se encontra no meio da comunicação entre as duas pessoas. Existem dois tipos de ataque do homem no meio:
- **Ataque do homem no meio passivo**: A **Pessoa C (Claire)** não consegue alterar (apenas vê) a mensagem cifrada (também chamada de **Pessoa E (Eve)**).
- **Ataque do homem no meio ativo**: A **Pessoa C (Claire)** consegue alterar e ver a mensagem cifrada.


## *Eletronic Code Book* (ECB)
O **ECB** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma independente. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (caso os blocos não sejam iguais) para cada bloco de dados.

Nota: Não é recomendado o uso para mensagens acima de 12 bytes não pseudo-aleatórios.

Exemplo para **cifrar**:
| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |
| Algoritmo | AES-e(k,m[0]) | AES-e(k,m[1]) | AES-e(k,m[2]) |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |

Exemplo para **decifrar**:
| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |
| Algoritmo | AES-d(k,c[0]) | AES-d(k,c[1]) | AES-d(k,c[2]) |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |

### *Cipher Block Chaining* (CBC)
### *Couter Mode* (CTR)
### *Output Feeback Mode* (OFM)
### *Ciphertext Feedback Mode* (CFM)
### *Padding* (Preenchimento)
O **padding** é uma técnica de preenchimento de dados que consiste em adicionar um número de bytes ao final de um bloco de dados, de forma a que o tamanho do bloco de dados seja múltiplo do tamanho do bloco de dados da cifra.

Nota: O último bloco tem sempre *padding*, mesmo que o bloco da mensagem seja múltiplo do tamanho do bloco da cifra é acrescentado um bloco de *padding*.