# Aula 5

## Funções Resumo Criptográfico (Hashes)

### CIA - Confidencialidade, Integridade e Disponibilidade
Estas são as propriedades que um sistema (em termos de segurança) deve ter:
 - Confidencialidade: A informação é mantida em segredo;
 - Integridade: A informação não é alterada;
 - Disponibilidade: A informação está disponível quando necessário;

### Requisitos de segurança
 - Confidencialidade (cifra);
 - Integridade (MAC - Message Authentication Code);
 - Anonimato (assinatura digital);

### Funções de Hash
Funções que dado um input de qualquer tamanho, produzem um output de um tamanho fixo. Estas funções são **one-way** (não há forma de obter o input a partir do output).

Exemplos de funções de hash:
 - MD5 (Message Digest 5) - 128 bits;

### Funções de Hash Criptográficas
Funções que dado um input de qualquer tamanho, produzem um output de um tamanho fixo. Estas funções são **one-way** (não há forma de obter o input a partir do output). São **resistentes a colisões**, ou seja, é difícil encontrar dois inputs diferentes que produzam o mesmo output (em tempo útil). Também têm como propriedade a **resistência a previsão de uma pré-imagem** e a **resistência a previsão de uma segunda pré-imagem**, ou seja, é difícil encontrar um input que produza um output conhecido.

Exemplos de funções de hash criptográficas:
 - SHA-1 (desencorajada) - Secure Hash Algorithm 160 bits;
 - SHA-256 (Secure Hash Algorithm 256 bits);
 - SHA-512 (Secure Hash Algorithm 512 bits);
 - SHA-3 (Secure Hash Algorithm 3) - permite especificar o número de bits;

## Message Authentication Code (MAC)
Há várias formas de construir um MAC, algumas delas são:
 - HMAC (Hash-based Message Authentication Code): este MAC tem dois algoritmos, um para construção e outro para verificação e recebe dois inputs, um é a chave e o outro é a mensagem;


## Resolução da ficha prática 6

### Tarefa 1
```c
#include <openssl/des.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define NUMBER_OF_BYTES 8

void cifraDES(char * nomeInput, char * chave, char * nomeOutput, int enc){

FILE * ficheiroInput = fopen(nomeInput, "rb");
FILE * ficheiroOutput = fopen(nomeOutput, "wb");

if(ficheiroInput == NULL || ficheiroOutput == NULL){
	fprintf(stderr,"Não foi possível criar/ler o ficheiro!\n");
	exit(0);
}


DES_cblock keyBlock;
DES_key_schedule schedule;

DES_cblock blockInput,blockOutput;

memcpy(&keyBlock,chave, NUMBER_OF_BYTES);

DES_set_odd_parity(&keyBlock);
DES_set_key_checked(&keyBlock, &schedule);

size_t bytesLidos;
while(bytesLidos = fread(&blockInput, 1, NUMBER_OF_BYTES, ficheiroInput) == NUMBER_OF_BYTES){
	DES_ecb_encrypt(&blockInput,&blockOutput, &schedule, enc);
	fwrite(&blockOutput, 1, NUMBER_OF_BYTES, ficheiroOutput);
}

if(bytesLidos != 0){
	fwrite(&blockInput, 1, bytesLidos, ficheiroOutput);
}

fclose(ficheiroInput);
fclose(ficheiroOutput);

}



int main(int argc, char **argv){

if(argc != 5){
	fprintf(stderr,"Número de argumentos inválidos\n");
	exit(0);
}
char * flag = argv[1];
char * input = argv[2];
char * key = argv[3];
char * output = argv[4];

if(strcmp(flag,"-e") == 0){
	// Encriptar
	cifraDES(input,key,output,DES_ENCRYPT);
	printf("Ficheiro encriptado com sucesso!\n");
}else if(strcmp(flag,"-d") == 0){
	// Desencriptar
	cifraDES(input,key,output,DES_DECRYPT);
	printf("Ficheiro desencriptado com sucesso!\n");
}else {
	fprintf(stderr, "Flag inserida inválida\n");
}


return 0;
}
```

1. A tamanho do bloco na DES é de 8 bytes.
2. Como compilar um programa escrito em linguagem C que use funções da toolkit do OpenSSL:
```console 
$ cc programa.c -lcrypto
```
3. Desde que use a codificação da chave certa em ambas implementações, o resultado será o mesmo.


## Fim da aula 5
Link para a [Próxima aula](Aula6.md)

Link para os [CheatSheets](OpenSSL.md)