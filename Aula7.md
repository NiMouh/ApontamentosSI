# Aula 7

## Cifras de chave pública
Usam problema de matemática intratáveis para gerar chaves. São baseadas em problemas de logaritmo discretos e fatorização de números compostos.

Exemplo:
São gerados dois números primos, X e Y (de tamanho de 512 bits) e geram o primo Z, sendo Z resultado da multiplicação de X e Y. O número Z é conhecido como **módulo** e é usado para gerar as chaves pública e privada.

## RSA
Um cifra de **chave pública** que precisa de:
 - Gerador de chaves: Primeiramente geramos dois números primos extremamente grandes, **X** e **Y**. Calcula-mos **Z** que é o produto de X e Y. Calcular números *phi* de Z, que é o produto de X-1 e Y-1. Finalmente, arranjamos dois números que multiplicados preencham esta condição: **((E * D) mod phi(Z)) = 1**. O número E é a chave pública e o D é a chave privada;
 - Um algoritmo para cifrar: Para cifrar fazemos a seguinte operação: C = M^E mod Z, sendo o M a mensagem a cifrar e C a mensagem cifrada;
 - Um algoritmo para decifrar: Para decifrar fazemos a seguinte operação: M = C^D mod Z, sendo o C a mensagem cifrada e M a mensagem decifrada.

Nota: Normalmente não se utiliza o **Text Book RSA**. Invés disso é acrescentado um *padding* para aumentar a segurança (OAEP).

## Esquema de assinatura digital
Recorrendo a chaves públicas (nomeadamente RSA), são usados três algoritmos:
 - Algoritmo para gerar chaves: É gerado um par de chaves, uma pública e outra privada;
   - (pub, priv) = RSA(512);
 - Algoritmo para gerar assinatura: É calculado o Hash da mensagem e decifrado com a chave privada;
   - t = RSA(priv, SHA256(m));
 - Algoritmo para verificar assinatura: É calculado o Hash da mensagem e decifrado com a chave pública;
   - v = RSA(pub, SHA256(m)) == t;

## Resolução da ficha prática 7

1. Message Authentication Code
2. Comandos usados:
```console
$ openssl dgst -sha1 texto-limpo.txt > texto-limpo.sha1
$ openssl enc -c -aes-128-cbc -in texto-limpo.sha1 -out texto-limpo.aes-sha1 -K 1234567890abcdef -iv 1234567890abcdef
```
3. Comandos usados para verificar a integridade do ficheiro:
```console
$ openssl enc -d -aes-128-cbc -in texto-limpo.aes-sha1 -out texto-limpo.sha1 -K 1234567890abcdef -iv 1234567890abcdef
$ openssl dgst -sha1 texto-limpo.txt > texto-limpo.sha1
$ diff texto-limpo.sha1 texto-limpo.sha1
```

4. O MAC que recebeu não verifica a integridade do ficheiro, pois o ficheiro foi alterado.
5. Não, pois o ficheiro foi alterado.
6. Dado ser um mecanismo da criptografia de chave simétrica todos os que possuem a chave secreta podem verificar a integridade do ficheiro.
7. Garante que o ficheiro não sofre erros aleatórios durante a sua transmissão. Garante que o ficheiro não foi alterado durante a sua transmissão.