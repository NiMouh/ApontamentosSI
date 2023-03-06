# Aula 2

## Criptografia
Conjunto de técnicas que visam a comunicação **secreta** entre dois agentes, sobre um canal aberto.

### Motivações da criptografia
Algumas motivações para a existência da criptografia:
 - Confidencialidade (inicialmente);
 - Integridade;
 - Anonimato;
 - Autenticação da origem de informação;
 - Autenticidade;
 - Autenticação de entidades;

### Criptanálise
Conjunto de técnicas que visam a quebra de sistemas criptográficos. Consistem em decifrar sem saber a chave ou tendo a chave.

#### Ataque com conhecimento de texto-limpo original (Known plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra a partir de um texto-limpo original e do texto-cifrado correspondente.

#### Ataque com o conhecimento apenas do criptograma (Ciphertext-only attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo, a partir de um texto-cifrado.

#### Ataque com o texto-limpo original escolhido pelo atacante (Chosen plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um texto-limpo original escolhido pelo atacante.

#### Ataques com criptogramas escolhidos pelo atacante (Chosen ciphertext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um conjunto de textos-cifrados escolhidos pelo atacante, diferentes do texto que queremos cifrar.

#### Ataque força bruta (Brute force)
É uma técnica de ataque que consiste em tentar todas as possíveis chaves de cifra até encontrar a chave correta.

Nota: Não é uma técnica de criptanálise.

## Criptologia
Cientifica que estuda a criptografia e a criptanálise.

## Cifras
Mecanismos de **integridade** e de **troca de chaves** ou segredos criptográficos.

### Propriedades necessárias de cifras seguras
Estas são algumas das propriedades que uma cifra segura tem:
- **Difusão**: Se uma cifra for de qualidade, quaisquer propriedades estatísticas do texto limpo estão completamente **difusas** (sem qualquer tipo de correlação) por todo o criptograma.
- **Não maneável**: Se uma cifra for de qualidade, não é possível **manejar** (alterar) o texto cifrado sem que o texto limpo seja alterado.
- **Semântica**: Se uma cifra for de qualidade, o adversário não deverá ser capaz de obter informações sobre o texto limpo a partir do texto cifrado.
- **Não determinística**: Esta propriedade permite que a cifra produza saídas diferentes para o mesmo texto limpo e chave de cifra.

Nota: Todas estas propriedades acima têm que ser balenceadas com a **usabilidade** da cifra.

### Cifras clássicas
São algoritmos que utilizam a mesma chave para cifrar e decifrar. Cifras clássicas têm **um** algoritmo (para cifrar e para decifrar).

Exemplos:
 - Cifra de César;
 - Cifra de Vigenère (mais difusa que a de César);
 - Cifra Enigma;
 - Cifra de Vernam (perfeita em termos de secretismo, contudo não é usável);

### Cifras de chave simétrica
São algoritmos que utilizam a mesma chave para cifrar e decifrar (simétrica). Cifras de chave simétrica têm **dois** algoritmos (para cifrar e para decifrar).

Para **cifrar**:
 - Input: Texto-limpo, Chave de cifra
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave de cifra
 - Output: Texto-limpo

### Cifras de chave simétrica continuas
As cifras de chave simétrica continuas usam um algoritmo que a partir de uma chave com tamanho **fixo** e **comportável**, geral uma sequência tão grande quanto necessária para cifrar um ficheiro. Cifras de chave simétrica continua têm **três** algoritmos (para cifrar, para decifrar e para gerar chaves).

Para **cifrar**:
 - Input: Texto-limpo, Chave de cifra, Algoritmo de geração de chaves (pseudo-aleatório)
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave de cifra, Algoritmo de geração de chaves (pseudo-aleatório)
 - Output: Texto-limpo

Nota: Este tipo de cifra tem como defeito a sua **maneabilidade** (facilidade da alteração do texto cifrado).

#### RC4 (Rivest Cipher 4)
É um algoritmo de cifra simétrica que utiliza uma chave de 40 a 2048 bits.

Nota: O algoritmo para **decifrar** é o mesmo que o de **cifrar**.

### Cifras de chave simétrica de bloco
O algoritmo para **decifrar** é diferente que o de **cifrar**.

### Cifras de chave pública
São algoritmos que utilizam chaves diferentes para cifrar e decifrar (igual á chave simétrica). Cifras de chave pública têm **três** algoritmos (para cifrar, para decifrar e para gerar chaves).

Para **par de chaves**:
 - Input: Chave pública, Chave secreta
 - Output: Par de chaves

Para **cifrar**:
 - Input: Texto-limpo, Chave pública
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave secreta
 - Output: Texto-limpo

#### RSA (Rivest, Shamir, Adleman)
É um algoritmo de cifra simétrica pública que utiliza uma chave de 512 a 4096 bits. Ele é bastante usado para criptografar dados em trânsito na internet.