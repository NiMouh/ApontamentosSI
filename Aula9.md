# Aula 9

## Infraestrutura de chave pública

Esta infraestrutura envolve os seguintes passos:
 - Um certificado de assinatura de chave pública é emitido por uma autoridade de certificação (CA) para um utilizador final.
 - Gera um par de chaves pública/privada.
 - Coloca a chave pública no certificado.
 - Instalo o certificado e a chave secreta no meu computador.

### Raiz de confiança

Normalmente o sistema operativo tem uma lista de certificados de confiança e as respetivas chaves públicas. Sempre que é pedido a um determinado site o seu certificado, ele manda em conjunto os certificados as autoridades certificadores e as acima das mesmas que passaram o certificado (cadeia de certificados). Caso estas autoridades do topo não se encontrem no 'browser' ou no sistema operativo, o certificado não é válido. Estas autoridades do topo são denominadas de raiz de confiança.

OBS: Só depois de estabelecer toda a certificação, é que comunicações podem ser feitas.

## Lista de revogação de certificados

É um documento com a lista de certificados que foram revogados. É uma lista que é atualizada regularmente e que é assinada pela autoridade de certificação. É uma lista que é descarregada pelo sistema operativo e pelo 'browser' e que é usada para verificar se um determinado certificado foi revogado (ou seja, se o certificado foi comprometido ou não válido).

## Cartão de Cidadão

O cartão do cidadão tem dois certificados digitais X.509. Um certificado de autenticação e um certificado de assinatura. O cartão de cidadão tem uma chave privada e uma chave pública. A chave privada está protegida por um **PIN**. A chave pública está no certificado de autenticação e no certificado de assinatura.

OBS: O cartão de cidadão não permite cifrar mensagens.

### Autenticação
O cartão de cidadão é conhecido por usar autenticação de dois fatores usando o Cartão do Cidadão, através do *smartcard* e a inserção do PIN do titular do cartão. Existe no cartão de cidadão **9 PINs** diferentes ao todo:
 - Ativação do *smartcard*: 8 dígitos
 - Assinatura digital: 4 dígitos
 - Cancelamento do *smartcard*: 8 dígitos
 - PIN da morada: 4 dígitos
 - PIN de autenticação: 4 dígitos
 - PIN de assinatura: 4 dígitos
 - Desbloqueio do PIN de morada: 4 dígitos
 - Desbloqueio do PIN de autenticação: 4 dígitos
 - Desbloqueio do PIN de assinatura: 4 dígitos

Nota: A **cada operação** feita com o cartão de cidadão, é pedido o PIN de autenticação.

#### PIN
Em termos de autorização de operações, há 3 PINs diferentes para o cartão de cidadão:
 - Um para autorizar a indicação da morada;
 - Outro para autenticação do titular;
 - Outro para produzir assinaturas digitais.

## Resolução da ficha prática 9

1. Gnu Privacy Guard.
2. Rivest Shamir Adleman.
3. GPG 2.2.
4. Autenticação,Confidencialidade,Integridade.
5. Criptografia sobre curvas elípticas, ElGamal.
6. Sim, noto.
7. Operações de leitura / escrita no disco, Interrupts ao processador, Introdução de dados pelo teclado, Movimentos e ações do rato.
8. Sim, mas este não pára (não bloqueia) à espera de eventos.
9. Acho que é muito seguro e, caso tenha de gerar chaves no meu trabalho prático de grupo, vou usar este ficheiro como fonte de aleatoriedade.
10. 2 chaves
11. Não preciso tomar precauções adicionais.
12. Caracteres de A a Z, de a a z, de 0 a 9, e os caracteres = a /.
13. Ao porta-chaves público
14. `gpg --import <FICHEIRO>`
15. As mesmas que antes.
16. --armor para gerar o ficheiro em formato ASCII. -s para assinar. -e para cifrar.
17. Neste caso não é preciso.
18. Porque o programa não é inteligente, e não sabe o que é a confiança. Porque nunca disse ao programa que confiava nesse utilizador e nas chaves dele(a). Porque nunca assinei nenhuma destas chaves com a minha chave privada.
19. `gpg --decrypt <FICHEIRO>`
20. Sim, emitiu um aviso.
21. Porque o programa precisa aceder ao porta-chaves privado.
22. 3 chaves de confiança marginal e 1 chave de confiança absoluta.
23. `--send-keys`
24. `--recieve-keys`
25. Que o GPG não deposita qualquer confiança nessa chave.
26. Sim, sem sombra de dúvidas.
