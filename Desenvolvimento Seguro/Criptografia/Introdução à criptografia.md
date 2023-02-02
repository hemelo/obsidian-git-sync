>Chaves simétricas

Mesma chave na criptografia/decriptação

- AES, RC5, DES, IDEA, 3DES

>Chaves assimétricas

Duas chaves, uma pra criptação outra pra decriptação

- RSA, Diffie-Helmann

> Hash

One-way functions

- MD5, SHA-1, SHA-256

>[!INFO] Integridade
>Garantir que a mensagem não chega modificada durante o trânsito
>>[!SUCCESS] Hash
>

>[!INFO] Confidencialidade
>Garantir que ninguém veja o conteúdo da mensagem

## Data Encryption Standard (DES)

- Desenvolvido pela IBM
![[Pasted image 20230201212124.png]]
- Mais utilizado no mundo junto às variações como 3DES que aumenta de 2<sup>56</sup> a 2<sup>168</sup>
- Encripta blocos de 8 bytes com chaves de 7 bytes + 1 byte de paridade

>[!WARNING]
>Dados que não sejam múltiplos de 8 bytes devem ter **padding**

> Eletronic Code Block

Dois blocos idênticos de texto simples levam a dois blocos idênticos de textos cifrados

>Cypher Block Chaining








