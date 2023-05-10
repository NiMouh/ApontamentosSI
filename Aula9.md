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

É um documento com a lista de certificados que foram revogados. É uma lista que é atualizada regularmente e que é assinada pela autoridade de certificação. É uma lista que é descarregada pelo sistema operativo e pelo 'browser' e que é usada para verificar se um determinado certificado foi revogado (ou seja, se o certificado foi comprometido).

## Cartão de Cidadão

O cartão do cidadão tem dois certificados digitais X.509. Um certificado de autenticação e um certificado de assinatura. O cartão de cidadão tem uma chave privada e uma chave pública. A chave privada está protegida por um PIN. A chave pública está no certificado de autenticação e no certificado de assinatura.

OBS: O cartão de cidadão não permite cifrar mensagens.