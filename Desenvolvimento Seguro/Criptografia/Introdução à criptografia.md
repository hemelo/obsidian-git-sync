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

## Sessões Dinâmicas

Criptografia assimétrica para trocar uma chave de sessão, e a partir disso, utilizar criptografia simétrica para criptografia simétrica para encriptar grande quantidade de dados

![[Pasted image 20230201222430.png]]

## Garantia de integridade

Como garantir, criptograficamente, a integridade e autenticidade de uma mensagem?

>Hash

Historicamente, checksums e CRCs vêm sendo utilizados como hashes há muitos anos

>[!DANGER] Problema
>Diferentes blocos de entrada facilmente produzem o mesmo resultado. 

Funções modernas:
- MD5 → 16 bytes
- SHA-1 → 20 bytes
- SHA-256 → 256 bytes

### Solução ao problema do Hash

Nota: Para a solução podem ser utilizadas chaves simétricas ou assimétricas. Mas por convenção de segurança, o exemplo usa assimétrica.

>Assinatura de documentos

1. Calcular o hash do documento
2. Encriptar o hash calculado junto com o conteúdo da mensagem
3. Assinatura terá o tamanho da chave privada utilizada

>Validação de documentos assinados

1. Recalcular o hash do documento recebido
2. Decriptar a assinatura com a chave pública

>[!DANGER] Problema
>Como garantir que a chave pública é de quem realmente diz ser?

### Solução ao problema da identidade da chave

>Geração de Certificados

1. Montar um buffer com vários dados + chave pública
2. Criar um hash
3. Encriptar hash com chave privada
4. Montar certificado final com buffer + assinatura encriptada

>Validação de Certificados

1. Decriptar a assinatura (com a chave pública da CA) e recuperar o hash 
2. Recalcular o hash
3. Validar se hashes são idênticos

## Public Key Infrastructure

>[!INFO] Exemplo envolvendo cartões
>CA → Emissor → Cliente

1. O emissor gera um par de chaves
2. Solicita-se à CA para certificar a chave pública
3. A CA devolve um certificado com os dados solicitados e a chave pública original assinada
4. Durante a personalziação, gera-se um par de chaves para cada cliente
5. O emissor utiliza a chave privada para certiifcar a chave pública dos cartões de seu cliente
6. Para validar o cartão, um terminal valida o certificado do emissor através da chave pública da CA
7. Por sua vez, o terminal valida o certificado do cliente através da chave pública do emissor
![[Pasted image 20230201225244.png]]


