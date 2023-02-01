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

- Os módulos de segurança de hardware são dispositivos reforçados e resistentes a adulteração que protegem processos criptográficos gerando, protegendo e gerenciando chaves usadas para criptografar e descriptografar dados e criar assinaturas e certificados digitais.