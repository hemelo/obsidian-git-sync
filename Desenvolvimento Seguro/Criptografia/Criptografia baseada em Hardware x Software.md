## Hardware

- Processador exclusivo
- Contém um gerador de número randômico para gerar chaves, chave essa que a senha do usuário deverá desbloquear
- Melhor desempenho ao retirar a criptografia do sistema host
- Chaves de proteção e parâmetros de segurança crítica dentro do hardware de criptografia
- Autenticação interna
- Econômica em ambientes com média/grande aplicação
- Escalonável
- A criptografia está associada a um dispositivo específico, assim a criptografia está "sempre ativa"
- Não exige nenhum tipo de instalação de driver ou software no PC host
- Proteção contra ataques como boot frio, código malicioso, força bruta...

## Software

- Compartilha recursos do computador para criptografar dados com outros programas no computador
- Usa a senha do usuário como chave de criptografia pra codificar dados
- Pode exigir atualizações de software
- Suscetível a ataques de força bruta
	- O computador tenta limitar as tentativas, mas os hackers podem acessar a memória do PC e reiniciar o contador
- Econômica em ambientes de pouca aplicabilidade
- Pode ser implementada em todos os tipos de mídia

---

# HSM

- Os módulos de segurança de hardware são dispositivos reforçados e resistentes a adulteração

- Protegem processos criptográficos gerando e gerenciando chaves usadas para criptografar e descriptografar dados e criar assinaturas e certificados digitais.

>[!INFO] Permitem às organizações
>
>Superar normas regulatórias como LGPD, GDPR, eIDAS, [[PCI]] DSS, HIPAA, entre outras...

- São testados e validados pela [[Federal Information Processing Standard|FIPS]] e Common Criteria

## Por que eu deveria usar um HSM?

<mark style="background: #BBFABBA6;">Operações criptográficas como criptografia e assinatura digital são inúteis se as chaves privadas que usam não estiverem bem protegidas</mark>

Motivação: Os invasores se tornaram sofitiscados em localizar chaves privadas armazendas ou em uso

## HSM _as a service_

>[!HELP] Cloud HSM

Produto com base em assinatura no qual os clientes podem usar um módulo de segurança de hardware na nuvem para gerar, acessar e proteger material de chave criptográfica de forma separada dos dados confidenciais.

O serviço normalmente oferece o mesmo nível de proteção

## Top 10 Casos

![[top-10-hsm-use-cases-2021-infographic.webp]]

## Que valor um HSM oferece?

>TLS/SSL

Chaves mestres de criptografia TLS/SSL seguras

>Containers e Nuvem

- Manter o controle das chaves e dados na nuvem
- Aplicativos seguros em contêineres

>PKI

Proteger a raiz de PKI e as chavews de assinatura CA

>Acesso privilegiado e gerenciamento de segredos

Aborde ameaças internas e simplifique o acesso a segredos para DevOps

>Criptografia e tokenização

Aprimore a proteção da chave de criptografia para dados em trânsito e armazenamento

>Gerenciamento de chaves

Aplique a política de gerenciamento de chaves em várias nuvens e aplicativos

>Assinatura digital e assinatura de código

Proteja as chaves que garantem a integridade do software e permitem transações legalmente vinculativas

>Identidade e autenticação

Crie credenciais de identidade confiáveis

>Pagamentos

Proteja as chaves que criam e assinam credenciais de pagamento

---

# Root of Trust

A raiz de confiança é a base de segurança da qual seu sistema de computação e dispositivos móveis conectados dependem. 

Como os esquemas são ineremente confiáveis, devem ser seguros desde a concepção. Normalmente, os esquemas de raiz de confiança contam com tecnologias de proteção de hardware como [[#HSM]]

## Por que ela é importante?

- Para impedir tentativas de ataques
- Ajuda a criar confiança em todo o ecossistema da informação

## Dispositivos móveis

- Diversos desafios
- Possuem maior risco de ataques físicos
- Difícil de garantir que esteja em conformidade com políticas corporativas

### O drama do _BYOD_

>BYOD significa Bring Your Own Device

A ideia é dar liberdade ao funcionário para que ele possa usar seus próprios aparelhos e dispositivos para acessar e modificar informações da empresa. 

Com a comodidade de lidar com computadores ou smartphones que lhe convêm, o funcionário consegue cuidar de questões importantes de qualquer lugar.

>[!SUCCESS] Desafio de sucesso!
>
>Encontrar o equilíbrio entre um ambiente extremamente seguro e a capacidade de permitir que seus funcionários acessem os dados de diversas e simplificadas formas.

#### MDM com BYOD

>MDM significa Mobile Devices Management

A Entrust Datacard fornece um serviço administrativo de gerenciamento de dispositivos móveis que consiste em provisionamento e gerenciamento de certificados poderosos, confiáveis e uniformes para acesso contínuo às redes para funcionários remotos e teletrabalho seguro. 

Além disso, tal serviço conta com gerenciamento completo do ciclo de vida da credencial e integração com produtos como VMWARE, Microsoft InTune, entre outros

Para saber mais: [Entrust MDM](https://www.entrust.com/pt/digital-security/certificate-solutions/solutions/use-cases/mobile-device-management-byod)




