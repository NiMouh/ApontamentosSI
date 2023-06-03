# Aula 10

## Quantificiação de risco
É possível definitr uma forma simples para o cálculo do risco (R) associado a uma determinada vulnerabilidade:

R = P x V, sendo o P a probabilidade de ocorrência de um ataque e o V o valor do ativo.

Apesar de ser uma forma simples de calcular o risco, esta fórmula não é muito precisa, pois implica:
 - Identificação e caracterização de vulnerabilidades;
 - Dedução da probabilidade de ocorrência de um ataque;

## Detetores de vulnerabilidades
Um dos primeiros passos para prevenir um possivel ataque será a **identificação do Sistema Operativo** (SO) e das **vulnerabilidades** da máquina alvo.

Estas são algumas das formulas de identificar vulnerabilidades:
 - Flâmulas (*Banners*): Consiste em observar o *banner* publicitado por servidores aquando o seu acesso, não é muito usado em máquinas cliente pois normalmente não têm serviços de rede ativos.
 - Impressão digital da Pilha IP: Consiste em identificar e coletar informações específicas sobre um dispositivo ou rede com base no seu endereço IP. Esta técnica é usada para identificar o SO e a versão do mesmo.
 - RING (Responder Identification Next Generation): Consiste em enviar um pacote ICMP para o alvo e analisar a resposta.
 - NMAP: Consiste em enviar pacotes TCP SYN para as portas mais comuns e analisar as respostas.
 - Inventariação de Serviços (Service Scanning): Consiste em enviar pacotes TCP SYN (ou UDP) para as portas mais comuns e analisar as respostas com o objetivo de identificar os serviços que estão a correr na máquina alvo.
 - Rastreio de Portas (Port Scanning): Consiste em enviar pacotes TCP SYN (ou UDP) para as portas mais comuns e analisar as respostas com o objetivo de identificar as portas que estão abertas na máquina alvo.
 - Inventariação de Deficiências de Administração: Consiste na exploração de vulnerabilidades conhecidas em serviços e aplicações comuns.
 - Ataques LAND: Consiste em enviar pacotes TCP SYN com o endereço IP de origem igual ao endereço IP de destino.
 - Ataques Teardrop: Consiste em enviar pacotes IP com fragmentos sobrepostos.
 - Ataques Echo-Chargen: enviar um pacote UDP com o mesmo endereço IP fonte e destino para a máquina vítima, e com os portos UDP de um e de outro serviço na fonte e no destino. O *echo* (porta 7) reenvia para o *chargen* (porta 19), e o *chargen* reenvia para o *echo*.
 - Ataque de Inundação de inicialização (SYN Flood): Consiste em enviar um grande número de pacotes TCP SYN para a máquina vítima, sem nunca enviar o pacote ACK para completar a ligação.

## Erros de Realização
Por norma são mencionados **dois tipos** de ataques ou vulnerabilidades:
 - Vulnerabilidade de transbordamento de memória (*Buffer Overflow*): Consiste em escrever dados para além do limite de um *buffer* de memória, podendo assim corromper dados de outros programas ou do próprio sistema operativo.
 - Vulnerabilidades associadas a cadeias de formato (*Format String*): Consiste em usar dados de entrada com códigos de controlo de formatação de *strings*.

## Resolução da prática 10

1. Apache HTTP Server, MySQL, PHP, Perl
2. Let´s encrypt
3. Mozilla, Google, Facebook, Cisco

### Tarefa 2

```php
<?php

echo "
<!DOCTYPE HTML>
<html>
<body>
    <h1>Registration form. Enter username and password.</h1>
    <form action="insert.php" method="post">
        Name: <input type="username" name="username"><br>
        E-mail: <input type="password" name="password"><br>
    <input type="submit">
    <input type="reset">
    </form>
</body>
</html> "
?php>
```

4. `cp register.php insert.php`
5. `mysql > CREATE DATABASE WebApp`
6. `CREATE TABLE User (username VARCHAR(30), salt CHAR(32), rep CHAR(64));` - Cria a tabela USER

### Tarefa 7

```php
<?php
function generate_salt(){
    $randomNumber = md5(rand());
    $randomNumber = substr($randomNumber, 0, 32);
    return $randomNumber;
}

function create_hash($password, $salt, $hash_algorithm){
    $new_password = $password + $salt;
    return hash($hash_algorithm, $new_password);
}
?>
```

### Tarefa 9

```php
<?php
// Estabelecer a ligação à base de dados
$connection = mysql_connect("localhost", "root", "password");

// Selecionar a base de dados correta
mysql_select_db("WebApp", $connection);

// Escapar caracteres especiais para evitar injeção de SQL
$username = mysql_real_escape_string($username);
$salt = mysql_real_escape_string($salt);
$rep = mysql_real_escape_string($rep);

// Instrução SQL para inserção dos valores na tabela User
$query = "INSERT INTO User (username, salt, rep) VALUES ('$username', '$salt', '$rep')";

// Executar a instrução SQL
$result = mysql_query($query);

// Verificar se a inserção foi bem sucedida
if ($result) {
    echo "Inserção realizada com sucesso!";
} else {
    echo "Erro ao inserir os dados: " . mysql_error();
}

// Fechar a ligação à base de dados
mysql_close($connection);
?>
```


### Tarefa 10

No `login.php`:
```php
<?php
echo "
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <form action="validate.php" method="post">
        <label for="username">Username:</label>
        <input type="text" name="username" id="username" required><br><br>
        <label for="password">Password:</label>
        <input type="password" name="password" id="password" required><br><br>
        <input type="submit" value="Login">
    </form>
</body>
</html> "
?>
```

No `validate.php`:
```php
<?php
// Estabelecer a ligação à base de dados
$connection = mysql_connect("localhost", "root", "password");

// Selecionar a base de dados correta
mysql_select_db("WebApp", $connection);

// Obter os valores do formulário
$username = $_POST['username'];
$password = $_POST['password'];

// Escapar caracteres especiais para evitar injeção de SQL
$username = mysql_real_escape_string($username);

// Consultar a tabela User para verificar as credenciais
$query = "SELECT * FROM User WHERE username = '$username'";
$result = mysql_query($query);

// Verificar se o usuário existe e a senha está correta
if (mysql_num_rows($result) > 0) {
    $row = mysql_fetch_assoc($result);
    $stored_password = $row['password'];

    // Validar a senha usando o esquema adequado
    // Substitua esta verificação com a lógica correta para o seu esquema de senha
    if (password_verify($password, $stored_password)) {
        echo "Tótil, bacano(a)!";
    } else {
        echo "Credenciais inválidas. Por favor, tente novamente.";
    }
} else {
    echo "Credenciais inválidas. Por favor, tente novamente.";
}

// Fechar a ligação à base de dados
mysql_close($connection);
?>
```