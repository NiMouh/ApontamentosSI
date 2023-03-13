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

## Criptologia
Cientifica que estuda a criptografia e a criptanálise.

## Cifras
Mecanismos de **integridade** e de **troca de chaves** ou segredos criptográficos.

### Propriedades necessárias de cifras seguras
Estas são algumas das propriedades que uma cifra segura tem:
- **Difusão**: Se uma cifra for de qualidade, quaisquer propriedades estatísticas do texto limpo estão completamente **difusas** (sem qualquer tipo de correlação) por todo o criptograma.
- **Confusão**: Se uma cifra for de qualidade, não são perceptiveis quaisquer relações entre um bloco de texto-limpo, a chave de cifra e o bloco de criptograma.
- **Não maneável**: Se uma cifra for de qualidade, não é possível **manejar** (alterar) o texto cifrado sem que o texto limpo seja alterado. Esta propriedade é mantida por um código de **autenticação de mensagem**.
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
 - Input: Texto-limpo, Chave de cifra, Algoritmo de geração de chaves (pseudo-aleatório)
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave de cifra
 - Output: Texto-limpo

#### Cifras de chave simétrica continuas
As cifras de chave simétrica continuas usam um algoritmo que a partir de uma chave com tamanho **fixo** e **comportável**, geral uma sequência tão grande quanto necessária para cifrar um ficheiro. Cifras de chave simétrica continua têm **três** algoritmos (para cifrar, para decifrar e para gerar chaves).

Nota: Este tipo de cifra tem como defeito a sua **maneabilidade** (facilidade da alteração do texto cifrado). Se cifrarmos um ficheiro já antes cifrado com a **mesma chave**, iremos obter o texto-limpo.

#### RC4 (Rivest Cipher 4)
É um algoritmo de cifra simétrica que utiliza uma chave de 40 a 2048 bits.

Nota: O algoritmo para **decifrar** é o mesmo que o de **cifrar**.

#### Cifras de chave simétrica de bloco
O algoritmo para **decifrar** é diferente que o de **cifrar**. A diferença entre as cifras de chave simétrica de bloco e as cifras de chave simétrica continua é que as cifras de chave simétrica de bloco geram uma cifra de tamanho fixo (bloco) e não uma cifra de tamanho variável. Caso a cifra de chave simétrica de bloco seja alterada (maneada), o texto cifrado perderá toda a sua integridade.

Nota: Este tipo de cifra é mais segura, dependendo de como são usadas, quando o canal de comunicação permite a **alteração** da mensagem cifrada.

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


## Exercicios das aulas práticas
Os algoritmos seguintes foram feitos no âmbito das aulas práticas da semana 2:
```c
#include <stdio.h>
#include <stdlib.h>

// Função que recebe string com o nome do ficheiro a ler, ficheiro a receber e a chave pseudoaleatória para o cifrar
void encrypt(char * inputFile, char * outputFile, int key){
    FILE *fInput, *fOutput;
    fInput = fopen(inputFile, "r");
    fOutput = fopen(outputFile, "w");
    srand(key);

    // ler primeiro byte do ficheiro
    int byte = fgetc(fInput);
    while(byte != EOF){
        // cifrar byte
        byte = byte ^ rand();
        // escrever byte cifrado no ficheiro e ler o próximo byte
        fputc(byte, fOutput);
        byte = fgetc(fInput);
    }
    fclose(fInput);
    fclose(fOutput);
}

// Função que recebe string com o nome do ficheiro a ler, ficheiro a receber e a posição do byte a alterar
void alterbyte(char * inputFile, char * outputFile, int bytePosition){
    FILE *fInput, *fOutput;
    fInput = fopen(inputFile, "r");
    fOutput = fopen(outputFile, "w");

    if(fInput == NULL || fOutput == NULL){
        printf("Erro ao abrir ficheiro");
        exit(1);
    }

    int i = 1;
    int byte = fgetc(fInput);
    while(byte != EOF){
        if(i == bytePosition){
            // alterar byte
            byte = byte ^ 0x01;
        }
        // escrever byte cifrado no ficheiro e ler o próximo byte
        fputc(byte, fOutput);
        byte = fgetc(fInput);
        i++;
    }
    fclose(fInput);
    fclose(fOutput);
}

int main(int argc, char *argv[]){
    if(argc != 4){
        printf("Erro no número de argumentos");
        exit(1);
    }

    char *inputFile = argv[1];
    char *outputFile = argv[2];
    int key = atoi(argv[3]); // unsigned int ikey = 123456789;

    encrypt(inputFile, outputFile, key);
    alterbyte(outputFile, "alterado.txt", 10);

    return 0;
}
```