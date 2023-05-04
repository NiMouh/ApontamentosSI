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

Nota: Normalmente não se utiliza o **Text Book RSA** (apenas cifrar o conteúdo pretendido). Invés disso é acrescentado um *padding* aleatório para aumentar a segurança (OAEP ou Optimal Assimetric Encription Padding).

## Esquema de assinatura digital
Recorrendo a chaves públicas (nomeadamente RSA), são usados três algoritmos:
 - Algoritmo para gerar chaves: É gerado um par de chaves, uma pública e outra privada;
   - (pub, priv) = RSA(512);
 - Algoritmo para gerar assinatura: É calculado o Hash da mensagem e decifrado com a chave privada;
   - t = RSA(priv, SHA256(m));
 - Algoritmo para verificar assinatura: É calculado o Hash da mensagem e decifrado com a chave pública;
   - v = RSA(pub, SHA256(m)) == t;

Nota: É possivel fazer um esquema de assinatura digital com chaves simétricas, porém seria necessário um agentes de confiança para garantir a integridade da chave.

### Propriedades principais de uma assinatura digital
Estas são as **cinco principais propriedades** de uma assinatura digital:
  - Autenticidade: A mensagem foi assinada pelo dono da chave privada;
  - Autenticação da origem de informação: A assinatura digital é única para cada mensagem;
  - Integridade dos dados: Qualquer alteração na mensagem invalida a assinatura;
  - Dificuldade de falsificação: É difícil falsificar uma assinatura digital;
  - Garantia de não repúdio: O dono da chave privada não pode negar que assinou a mensagem.

## Resolução da ficha prática 7

1. Message Authentication Code
2. Comandos usados:
```console
$ openssl dgst -sha1 texto-limpo.txt > texto-limpo.sha1
$ openssl enc -aes-128 -in texto-limpo.sha1 -out texto-limpo.aes-sha1 -K 1234567890abcdef -iv 1234567890abcdef
```
3. Comandos usados para verificar a integridade do ficheiro:
```console
$ openssl enc -d -aes-128 -in texto-limpo.aes-sha1 -out texto-limpo.sha1 -K 1234567890abcdef -iv 1234567890abcdef
$ openssl dgst -sha1 texto-limpo.txt > texto-limpo2.sha1
$ diff texto-limpo.sha1 texto-limpo2.sha1
```

4. O MAC que recebeu não verifica a integridade do ficheiro, pois o ficheiro foi alterado.
5. Não, pois o ficheiro foi alterado.
6. Dado ser um mecanismo da criptografia de chave simétrica todos os que possuem a chave secreta podem verificar a integridade do ficheiro.
7. Garante que o ficheiro não sofre erros aleatórios durante a sua transmissão. Garante que o ficheiro não foi alterado durante a sua transmissão.
8. Comandos usados para verificar a integridade do ficheiro:
```console
$ openssl dgst -sha1 -hmac 1234567890abcdef texto-limpo.txt > texto-limpo.sha1
$ diff texto-limpo.sha1 texto-limpo2.sha1
```
9. Para testar a tarefa 5:
```python
if __name__ == "__main__":
        for i in range(0,17):
                print(2**i % 17)
                print(3**i % 17)
```
Não, mas o 3 já é.
10. O número usado foi o 14.
11. Tentativa e erro.
12. Sim, concordo, porque o atacante apenas conseguia escutar as comunicações.

## Fim da aula 7
Link para a [Aula anterior](Aula6.md)

Link para a [Próxima aula](Aula8.md)

Link para os [CheatSheets](CheatSheet.md)