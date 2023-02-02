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

# Chaves Simétricas

>[!DANGER]
>Sempre existe algum risco no compartilhamento de chaves

>[!SUCCESS]
>Armazenar em [[Criptografia baseada em Hardware x Software#Hardware|hardware]] ajuda, mas não resolve

## Data Encryption Standard (DES)

- Desenvolvido pela IBM
![[Pasted image 20230201212124.png]]
- Mais utilizado no mundo junto às variações como 3DES que aumenta de 2<sup>56</sup> a 2<sup>168</sup>
- Encripta blocos de 8 bytes com chaves de 7 bytes + 1 byte de paridade

>[!WARNING]
>Dados que não sejam múltiplos de 8 bytes devem ter **padding**

> Eletronic Code Block

Dois blocos idênticos de texto simples levam a dois blocos idênticos de textos cifrados

- Trocar a ordem não impede que se recupere a informação

>Cypher Block Chaining

Como o resultado de cada passo é utilizado para alimentar o passo seguinte, dois blocos idênticos de texto levam a dois blocos totalmente diferentes de textos cifrados

- Trocar a ordem impede de se recuperar a informação

>[!INFO] 
>Essa metodologia é utilizada na urna eletrônica brasileira e na blockchain

- Dificulta criptoanálises estatísticas

## Diversificação de chaves

Processo pela qual uma chave simétrica é transformada em outra chave simétrica

![[Pasted image 20230201215139.png]]

# Chaves Assimétricas

>[!DANGER] Complexas de serem geradas

>[!DANGER] Menos velocidade

>[!DANGER] Maior tamanho de chave

>[!SUCCESS] Drástica redução do número de chaves

>[!SUCCESS] Permite disponibilizar uma das chaves (a pública)

> [!SUCCESS] Permite implementar mecanismos de não repudiação




