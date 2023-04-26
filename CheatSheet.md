# Cheat Sheet de Segurança Informática

## Linux

### Criar ficheiro vazio
```console
$ touch ficheiro.txt
```

### Comparar 2 ficheiros
```console
$ diff ficheiro1.txt ficheiro2.txt # (não dá output nenhum se os ficheiros forem iguais)
```

### Acesso ao manual de uma opração / aplicação
```console
$ man aplicação # (ex: man openssl)
```

### “Pesquisa” num output no terminal
```console
$ man openssl | grep md5
```

### Ver conteudo de um ficheiro
```console
$ cat ficheiro.txt
```

### Criar um ficheiro com uma string sem incluir os `\n`
```console
$ echo -n "texto" > texto-limpo.txt
```

### Adicionar mais string a um ficheiro existente sem os `\n`
```console
$ echo -n "texto" >> texto-limpo.txt
```

### Verificar ficheiro em HEX
```console
$ hexdump -C ficheiro.txt
```

## Comandos utilizados no OpenSSL

### Parametros gerais OpenSSL
 - ``-K`` especifica chave em HEX
 - ``-k`` especifica chave em ASCII (Não usado na UC)
 - ``-out`` ficheiro de saida
 - ``-in`` ficheiro de entrada
 - ``-e`` operação de cifragem
 - ``-d`` operação de decifragem

Formato para usar o comando OpenSSL:
```console
$ openssl <MÉTODO> <FLAGS> <ARGUMENTOS>
```

## Métodos conhecidos:

### Rand
Gera um conjunto de bytes pseudo-aleatórios.

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
Gera um resumo criptográfico (hash) de um ficheiro.

Exemplo:
```console
$ openssl dgst <FLAG> <FICHEIRO> # FLAG pode ser -md5, -sha1, -sha256, -sha512
```

### HMAC
Gera um HMAC (Hash Message Authentication Code) de um ficheiro.

Exemplo:
```console
$ openssl mac -digest <DIGEST> -macopt <CHAVE> -in <FICHEIRO> -out <FICHEIRO_CIFRADO> HMAC # CHAVE pode ser -hexkey <CHAVE_EM_HEX>
```
