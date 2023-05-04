# Cheat Sheet de Segurança Informática

## Linux

### Comprimir um ficheiro
```console
$ zip ficheiro-comprimido.zip ficheiro.txt
```

### Criar ficheiro vazio
```console
$ touch ficheiro.txt
```

### Comparar 2 ficheiros
```console
$ diff ficheiro1.txt ficheiro2.txt # (não dá output nenhum se os ficheiros forem iguais)
```

### Acesso ao manual de um *toolkit*
```console
$ man aplicação # (ex: man openssl)
```

### “Pesquisa” num output no terminal
```console
$ man openssl | grep md5
```

### Ver conteúdo de um ficheiro
```console
$ cat ficheiro.txt
```

### *Overwrite* num ficheiro com uma string sem incluir o `\n`
```console
$ echo -n "texto" > texto-limpo.txt
```

### Concatenar uma string num ficheiro existente sem o `\n`
```console
$ echo -n "texto" >> texto-limpo.txt
```

### Verificar ficheiro em HEX
```console
$ hexdump -C ficheiro.txt
```

## Comandos utilizados no OpenSSL

### Parametros gerais OpenSSL
 - ``-K`` especifica chave em HEX;
 - ``-k`` especifica chave em ASCII (Não usado na UC);
 - ``-out`` ficheiro de saida;
 - ``-in`` ficheiro de entrada;
 - ``-e`` operação de cifragem;
 - ``-d`` operação de decifragem;

Formato para usar o comando OpenSSL:
```console
$ openssl <MÉTODO> <FLAGS> <ARGUMENTOS>
```

## Métodos conhecidos:

### Rand
**Gera** um conjunto de bytes pseudo-aleatórios.

Exemplo:
```console
$ openssl rand -hex 16 # Gera 16 bytes pseudo-aleatórios em hexadecimal
```

### Enc
Cifra/Decifra um ficheiro.

Exemplo para **encriptar**:
```console
$ openssl enc -e <ALGORITMO> -in <FICHEIRO> -out <FICHEIRO_CIFRADO> -K <CHAVE> -iv <VETOR_INICIALIZAÇÃO> 
# ALGORITMO pode ser -aes-128-cbc, -aes-128-ecb, -aes-128-cfb, -aes-128-ofb, chacha20
```

Exemplo para **desencriptar**:
```console
$ openssl enc -d <ALGORITMO> -in <FICHEIRO_CIFRADO> -out <FICHEIRO_DECIFRADO> -K <CHAVE> -iv <VETOR_INICIALIZAÇÃO> 
# ALGORITMO pode ser -aes-128-cbc, -aes-128-ecb, -aes-128-cfb, -aes-128-ofb, chacha20
```

### Digest
**Gera** um resumo criptográfico (hash) de um ficheiro.

Exemplo:
```console
$ openssl dgst <FLAG> <FICHEIRO> # FLAG pode ser -md5, -sha1, -sha256, -sha512
```

### HMAC
**Gera** um HMAC (Hash Message Authentication Code) de um ficheiro.

Exemplo:
```console
$ openssl mac -digest <DIGEST> -macopt <CHAVE> -in <FICHEIRO> -out <FICHEIRO_CIFRADO> HMAC # CHAVE pode ser -hexkey <CHAVE_EM_HEX>
```

### RSA
Aqui os comandos *standard* usados são o `genrsa`, `rsa` e `rsautl`.

**Gerar** um par de chaves RSA (Aqui está contida a chave pública e a privada):

```console
$ openssl genrsa -out <FICHEIRO_CHAVE_PRIVADA> <TAMANHO_DA_CHAVE> 
# Tamanho da chave pode ser 1024, 2048, 3072, 4096
```

**Gerar** um par de chaves, mas protegidas por cifra simétrica (Aqui está contida a chave pública e a privada):

```console
$ openssl genrsa -aes128 -out <FICHEIRO_CHAVE_PRIVADA> <TAMANHO_DA_CHAVE>
```

**Extrair** a chave pública de um par de chaves RSA:

```console
$ openssl rsa -in <FICHEIRO_CHAVE_PRIVADA> -pubout -out <FICHEIRO_CHAVE_PUBLICA>
# Caso não seja especificado o ficheiro de saída, a chave pública é escrita para o terminal
```

Comando para **cifrar** um ficheiro com a chave pública recebida:
```console
$ openssl rsautl -encrypt -pubin -inkey <FICHEIRO_CHAVE_PUBLICA> -in <FICHEIRO_A_CIFRAR> -out <FICHEIRO_CIFRADO>
```

Comando para **decifrar** um ficheiro com a chave privada:
```console
$ openssl rsautl -decrypt -inkey <FICHEIRO_CHAVE_PRIVADA> -in <FICHEIRO_A_DECIFRAR> -out <FICHEIRO_DECIFRADO>
```

Comandos para trocar chave de cifra simétrica com RSA:
 - Para **cifrar**:
```console
$ openssl enc -aes-128-cbc -e -in <FICHEIRO_A_CIFRAR> -out <FICHEIRO_CIFRADO> -pass file:<FICHEIRO_CHAVE_PUBLICA>
```
 - Para **decifrar**:
```console
$ openssl enc -aes-128-cbc -d -in <FICHEIRO_CIFRADO> -out <FICHEIRO_DECIFRADO> -pass file:<FICHEIRO_CHAVE_PRIVADA>
```


### Assinatura Digital

Comando para gerar uma assinatura digital de um ficheiro:
```console
$ openssl dgst -sha256 -sign <FICHEIRO_CHAVE_PRIVADA> -out <FICHEIRO_ASSINATURA> <FICHEIRO_A_ASSINAR>
```

Outro modo, de antigir o mesmo resultado:
```console
$ openssl dgst -sha256 -out <FICHEIRO_HASH> <FICHEIRO_A_ASSINAR>
$ openssl rsautl -sign -inkey <FICHEIRO_CHAVE_PRIVADA> -in <FICHEIRO_HASH> -out <FICHEIRO_ASSINATURA>
```

E para confirmar a assinatura:
```console
$ openssl rsautl -verify -inkey <FICHEIRO_CHAVE_PUBLICA> -in <FICHEIRO_ASSINATURA> -out <FICHEIRO_HASH>
$ openssl dgst -sha256 -verify <FICHEIRO_CHAVE_PUBLICA> -signature <FICHEIRO_HASH> <FICHEIRO_A_ASSINAR>
```
