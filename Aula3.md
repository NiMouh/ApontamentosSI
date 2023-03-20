# Aula 3

## Algoritmos conhecidos

### RSA (Rivest, Shamir, Adleman)
É um algoritmo de cifra pública que utiliza uma chave de 512 a 4096 bits. Ele é bastante usado para criptografar dados em trânsito na internet.

### AES (Advanced Encryption Standard)
É um algoritmo de cifra simétrica de bloco que utiliza uma chave de 128, 256 OU 512 bits. Ele é bastante usado para criptografar dados em trânsito na internet.

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

Nota: **Não é recomendado** o uso para mensagens acima de 12 bytes não pseudo-aleatórios.

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
O **CBC** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma dependente do bloco anterior. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (mesmo os blocos sendo iguais) para cada bloco de dados. Este método evita **alguns** ataques por maninupulação de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Recebe um vetor de inicialização (IV) - gerado aleatóriamente, único para cada mensagem e partilhado entre as duas partes;
 - É feito o XOR entre o bloco de texto-limpo e o IV;
 - O resultado do XOR é cifrado com a chave;
 - O resultado cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte;
 - Processo repete-se até ao fim da mensagem;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Este bloco é decifrado com a chave;
 - É feito o XOR entre o bloco de decifrado e o IV;
 - Esse bloco cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte após ser decifrado;
 - Processo repete-se até ao fim da mensagem;

Nota: Não suporta processamento paralelo a **cifrar** mas suporta a **decifrar**.

## Resolução da ficha prática 4

1. Logb(N), sendo b a base utilizada (pode ser 10) e n simboliza as possíveis ocorrências de cada símbolo.
2. 2^8 = 256
3. 2.41
4. O modo de cifra do AES é o **CBC**.
5. A chave "0123456789abcdef0123456789abcdef" tem tamanho 256 bits.
6. Primeiro comprimir e depois cifrar
7. AES = Advanced Encryption Standard
8. AES é uma cifra simétrica de bloco
9. Sim, existem duas linhas semelhantes no visualizador de conteudos do ficheiro cifrado.
10. .
11. Não precisa.
12. Falta o vetor de inicialização.
13. CBC = Cipher Block Chaining
14. CBC é um modo de utilizar a cifra AES.

```python
# Tarefa 1: Calcula a entropia dos caracteres (bytes) de um ficheiro. 
# O programa deve deolver os valores da entropia do ficheiro e a entropia máxima.

from math import log10

def entropia(ficheiro):
    # Abrir o ficheiro
    f = open(ficheiro, "rb")
    # Ler o ficheiro
    conteudo = f.read()
    # Fechar o ficheiro
    f.close()
    # Calcular o tamanho do ficheiro
    tamanho = len(conteudo)
    # Calcular a entropia
    entropia = 0
    for i in range(256):
        # Calcular a probabilidade de cada byte
        probabilidade = conteudo.count(bytes([i])) / tamanho
        # Calcular a entropia
        if probabilidade > 0:
            entropia += probabilidade * log10(probabilidade)
    # Calcular a entropia máxima
    entropia_maxima = log10(256)
    # Devolver os valores da entropia do ficheiro e a entropia máxima
    return -entropia, entropia_maxima

if __name__ == "__main__":
    # Calcular a entropia do ficheiro
    entropia, entropia_maxima = entropia("ficheiro.txt")
    # Imprimir os valores da entropia do ficheiro e a entropia máxima
    print("Entropia do ficheiro: " + str(entropia))
    print("Entropia máxima: " + str(entropia_maxima))
```