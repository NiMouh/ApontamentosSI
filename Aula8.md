# Aula 8

## Criptograma do ElGamal
São necessários três algoritmos:
 - **Gerar chaves** públicas e privadas:
   - Gera um número P (número primo grande) e um número G (gerador);
   - Gera um x entre 1 e P;
   - Calcula X = G^x mod P;
   - A chave pública é (X, G, P);
 - Para **cifrar**:
   - Necessita da chave pública, do texto-limpo e de um número aleatório A entre 1 e P;
   - Calcula Y = G^A mod P;
   - Calcula K = X^A mod P;
   - Calcula o texto cifrado C = (m * K) mod P;
   - Envia o texto cifrado C e o Y;  
 - Para **decifrar**:
   - Recebe o texto cifrado C e o Y;
   - Calcula o K = Y^x mod P;
   - Calcula a mensagem m = (C * K^-1) mod P; 

Nota: neste criptograma caso eu cifre a mensagem duas vezes, irá resultar de dois textos cifrados diferentes.

## Certificados digitais
É um documento que liga dois conceitos, assinado por alguém, que certifica, e não dá para desfazer qualquer detalhe.

### Exemplo de certificado digital
  - **Nome para quem é passado**;
  - **Quem passou o certificado**;
  - **Data de início do certificado**;
  - **Data de fim do certificado**;
  - **Chave pública**;
  - **Algoritmo de assinatura**;
  - **Assinatura**;

Nota: Os sistemas operativos têm uma lista de certificados digitais de confiança e as respetivas chaves públicas.

## Resolução da ficha prática 8
### Tarefa 1
p = 17, q = 23, N = p * q = 391, ϕ(N) = (p - 1) * (q - 1) = 352

```python
from random import randint

def inverse_found(e,d,phi):
        return ((e * d) % phi) == 1

def get_numbers(phi):
        e = randint(2,phi)
        d = randint(2,phi)
        while not inverse_found(e,d,phi):
                e = randint(2,phi)
                d = randint(2,phi)
        return e, d



if __name__ == "__main__":
        phi = 392
        e, d = get_numbers(phi)
        print("e:", e)
        print("d:", d)
```

Resultado: e = 377, d = 209, pk = (377, 391), sk = 209

### Tarefa 2
Cifrar a mensagem "Mensagem" com a chave pública pk = (377, 391)

```python

def decrypt(sk, c, n):
        print(pow(c,sk) % n)

def encrypt(pk,m,n):
        print(pow(m,pk) % n)

if __name__ == "__main__":
    n = 391
    message = 200

    # Cifrar
    pk = 377
    cipher_text = encrypt(pk, message, n)

    # Decifrar
    sk = 209
    decrypt(sk, cipher_text, n)

```

1. Não, e não há qualquer problema de segurança nisso.
2. Porque eu lha dei diretamente.
3. Respondia que sim, mas com alguma hesitação.
4. Chave pública
5. Chave privada

### Tarefa 4

Comando no Openssl para gerar chaves RSA para o ficheiro `sk_and_pk.pem`:

```console
$ openssl genrsa -out sk_and_pk.pem
```

Comando para extrair a chave pública do ficheiro `sk-and-pk.pem` para o ficheiro `pk-nome-aluno.pem`:

```console
$ openssl rsa -in sk_and_pk.pem -pubout -out pk-nome-aluno.pem
```

Comando para ver a chave pública no ecrã:

```console
$ openssl rsa -in sk_and_pk.pem -pubout
```

Comando para gerar as chaves, mas protegidas por cifra simétrica:

```console
$ openssl genrsa -aes128 -out sk_and_pk.pem
```

### Tarefa 5

Gerar valor aleatório de 128 bits:

```console
$ openssl rand -hex 128 > secret.key
```

Comando para cifrar esse ficheiro com a chave pública recebida:
```console
$ openssl rsautl -encrypt -inkey pk-nome-aluno.pem -pubin -in secret.key -out secret.key.enc
```

6. Neste caso consegui, porque 128 bits é menor do que o tamanho do módulo que estou a usar.

### Tarefa 6

Comando para decifrar o ficheiro `secret.key.enc` com a chave privada:

```console
$ openssl rsautl -decrypt -inkey sk_and_pk.pem -in secret.key.enc -out secret.key.dec
```

7. 2048
8. Não consegui cifrar o paragrafo pois o texto é grande demais.
9. PGP = Pretty Good Privacy

### Tarefa 8

Para **Cifragem**:

```console
$ openssl enc -aes-128-cbc -in secret.key -out secret.key.enc
$ openssl rsautl -encrypt -inkey pk-nome-aluno.pem -pubin -in secret.key.enc -out secret.key.enc.enc
```

Parta **Decifragem**:

```console
$ openssl rsautl -decrypt -inkey sk_and_pk.pem -in secret.key.enc.enc -out secret.key.enc
$ openssl enc -d -aes-128-cbc -in secret.key.enc -out secret.key.dec -pass file:secret.key
$ cat secret.key.dec
```

10. Sou um(a) fulano(moça) certinho(a), e tenho tudo guardadinho.

### Tarefa 9

Comandos para gerar o valor de hash do ficheiro `Portugal.txt` e assinar o valor de hash com a chave privada:

```console
$ openssl dgst -sha256 -out Portugal.sha256 Portugal.txt
$ openssl rsautl -sign -inkey sk_and_pk.pem -in Portugal.sha256 -out Portugal.sig
```

Comandos para verificar a assinatura com a chave pública:

```console
$ openssl rsautl -verify -inkey pk-nome-aluno.pem -pubin -in Portugal.sig -out Portugal.sig.dec
$ openssl dgst -sha256 -verify pk-nome-aluno.pem -signature Portugal.sig.dec Portugal.txt
$ diff Portugal.sha256 Portugal.sig.dec
```

### Tarefa 10

Comando para calcular a assinatura digital de uma forma integrada no OpenSSL:

```console
$ openssl dgst -sha256 -sign sk_and_pk.pem -out Portugal.sig Portugal.txt
```

### Tarefa 11

11. Só quem tem chave privada.
12. Só quem tem chave simetrica
13. Quem tem chave pública
14. Quem tem chave simetrica
15. Autenticação da origem da informação, Integridade, Não repudiação, Autenticidade, Dificuldade de falsificação.
16. Integridade, Dificuldade de falsificação, Autenticidade.

## Fim da aula 8
Link para a [Aula anterior](Aula7.md)

Não tem link ainda para a próxima aula.

Link para os [CheatSheets](CheatSheet.md)
