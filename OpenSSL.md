# Comandos utilizados no OpenSSL

Formato para usar o comando OpenSSL:
```console
$ openssl <MÉTODO> <FLAGS> <ARGUMENTOS>
```

# Métodos conhecidos:

## Rand
Gera um conjunto de bytes pseudo-aleatórios.

Exemplo:
```console
$ openssl rand -hex 16 # Gera 16 bytes pseudo-aleatórios em hexadecimal
```

## Enc
Cifra/Decifra um ficheiro.

Exemplo para **cifrar**:
```console
$ openssl enc -c <ALGORITMO> -in <FICHEIRO> -out <FICHEIRO_CIFRADO> -K <CHAVE> -iv <VETOR_INICIALIZAÇÃO> # ALGORITMO pode ser -aes-128-cbc, -aes-128-ecb, -aes-128-cfb, -aes-128-ofb, chacha20
```

Exemplo para **decifrar**:
```console
$ openssl enc -d <ALGORITMO> -in <FICHEIRO_CIFRADO> -out <FICHEIRO_DECIFRADO> -K <CHAVE> -iv <VETOR_INICIALIZAÇÃO> # ALGORITMO pode ser -aes-128-cbc, -aes-128-ecb, -aes-128-cfb, -aes-128-ofb, chacha20
```

## Digest
Gera um resumo criptográfico (hash) de um ficheiro.

Exemplo:
```console
$ openssl dgst <FLAG> <FICHEIRO> # FLAG pode ser -md5, -sha1, -sha256, -sha512
```