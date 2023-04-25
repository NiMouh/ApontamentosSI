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

## Fim da aula 8
Link para a [Aula anterior](Aula7.md)

Não tem link ainda para a próxima aula.

Link para os [CheatSheets](CheatSheet.md)