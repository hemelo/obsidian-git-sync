# Resumo

>[!INFO] Pilares
>- Gestão de documentos
>- Autocontroles
>- Ações corretivas
>- Laudos
>- Gestão de não conformidades
>- Controle da qualidade
>- Ações preventivas

>[!IMPORTANT] Voice of costumer
>O cliente deve ser ouvido e ter voz

>[!WARNING] Critical customer requirement
>- O que é importante para o cliente
>- Avaliação
>	- Traz um atributo desejado?
>	- Estabelece uma meta?
>	- Pode ser medido?

>[!SUCCESS] Voice of business
>Variação entre o tempo de entrega da empresa e o tempo esperado pelo cliente

>[!HELP] Mapa estratégico
>- Processos internos
>	>[!IMPORTANT] Desenha os processos na busca da melhoria contínua
>- Aprendizado e crescimento
>	>[!PEOPLE] Medir como seus funcionários estão preparados no seu negócio
>- Finanças
>	>[!SUCCESS] Identificar a saúde financeira do seu negócio
>- Clientes
>	>[!WARNING] Responde como os clientes o avaliam

>[!INFO] Clientes
>- Internos
>- Externos
>- Certificadores

>[!IMPORTANT] [[#SIPOC]]
>Supplier -> Input -> Process -> Output -> Customer

>[!INFO] [[#Diagrama de Ishikawa]]
>6Ms - Método, Máquina, Mão de Obra, Material, Meio Ambiente, Medida

>[!SUCCESS] [[#Matriz GUT]]
>Gravidade, Urgência, Frequência




---
# SIPOC

- Definir as fronteiras de estudo do processo
- Conhecer o macro processo
- Base para discussão de tudo
- Consenso entre toda a equipe

![[Pasted image 20230203204216.png]]


---
# Indicadores de Desempenho

>[!SUCCESS] Eficiência => Seguir Regras
>- Estratégia
>- Objetivo
>- Performance


>[!DANGER] Eficácia => Conseguir Resultados
>- Avaliação
>- Medidas
>- Otimização


## Medição

Plano de Coleta de Dados e medida dos indicadores

| Medida de desempenho | Período/Frequência | Local | Tamanho da amostra | Responsável | Equipamento | Dados secundários |
| -------------------- | ------------------ | ----- | ------------------ | ----------- | ----------- | ----------------- |
|                      |                    |       |                    |             |             |                   |
|                      |                    |       |                    |             |             |                   |


| Como os dados serão utilizados? | Como os dados serão exibidos? |
| ------------------------------- | ----------------------------- |
|                                 |                               |


### Gráfico de Pareto

O gráfico de pareto é uma plotagem com barras verticais que indicam incidência e uma linha crescente que aponta a porcentagem cumulativa do problema

| Tipo de Defeito                  | Número de ocorrências | % de ocorrências | % acumulado |
| -------------------------------- | --------------------- | ---------------- | ----------- |
| Combustível adulterado           | 46                    | 36               | 36          |
| Bicos injetores entupidos        | 36                    | 28               | 64          |
| Tanque sujo                      | 20                    | 16               | 80          |
| Bomba de combustível com defeito | 14                    | 11               | 91          |
| Filtro de combustível entupido   | 8                     | 6                | 97          |
| Cabo das velas com defeito       | 4                     | 3                | 100         | 
![[Pasted image 20230203205410.png]]

Pela imagem, nota-se que eliminando os 3 principais problmas, 80% das ocorrências são reduzidas

## Encontrando as causas

### Diagrama de Ishikawa

>[!INFO] Conhecido como espinha de peixe

>[!SUCCESS] Método, máquina, material, mão de obra, medida, meio ambiente

![[Pasted image 20230203205847.png]]

### 5 porquês

- Que prova tenho de que essa causa
	- existe?
	- levará ao problema?
	- é a principal causa?
	- é a única?

>Um garçom processa um pagamento errado, o cliente fica bravo e xinga o garçom. As pessoas acham o garçom incompetente. Mas se analisar bem:
>- Por que o garçom errou?
>Não sabia fazer o pagamento
>- Por que não sabia fazer a operação de processar um pagamento?
>É novato
>- Por que o fato de ser novato dificultou a operação?
>Não foi treinado
>- Por que não foi treinado?
>Não foi selecionado alguém para treiná-lo
>- Por que o gerente não fez isso?
>Negligência


## Encontrando as soluções

### Matriz GUT

| Item                                          | Gravidade | Urgência | Frequência | Total |
| --------------------------------------------- | --------- | -------- | ---------- | ----- |
| Estoque Lento                                 | 3         | 5        | 1          | 15    |
| Leitura errada do sistema que checa o estoque | 2         | 3        | 2          | 12    |
| Sem Ar-condicionado                           | 2         | 3        | 1          | 6     |
| Erro na consulta do Pedido                    | 3         | 3        | 1          | 9     |
| Parada da Impressora                          | 3         | 3        | 5          | 45    |
| Falta de Treinamento                          | 2         | 3        | 1          | 6     |
| Tipos diferentes de clientes                  | 5         | 5        | 5          | 125   |
| Computador antigo                             | 4         | 5        | 5          | 100   |
|                                               |           |          |            |       |

>Certamente os maiores problemas são: Tipos diferentes de clientes, Computador antigo e parada da impressora