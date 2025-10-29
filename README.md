# Projeto Final - WordPress com EC2, ASG, EFS e RDS

Este projeto implanta a arquitetura completa solicitada no módulo de Infraestrutura como Código, usando CloudFormation.

A infraestrutura provisiona:
* **Rede (VPC):** Uma nova VPC com sub-redes públicas (para o ALB) e privadas (para EC2 e RDS) em duas Zonas de Disponibilidade.
* **Gateways:** Um Internet Gateway (para o público) e um NAT Gateway (para o privado acessar a internet para atualizações).
* **Balanceador (ALB):** Um Application Load Balancer nas sub-redes públicas.
* **Computação (EC2/ASG):** Um Auto Scaling Group (ASG) que gerencia instâncias EC2 nas sub-redes privadas.
* **Política de Scaling:** Uma política de Target Tracking Scaling baseada em CPU.
* **Armazenamento (EFS):** Um Amazon EFS para persistir os arquivos do WordPress (`/var/www/html`).
* **Banco de Dados (RDS):** Uma instância de banco de dados MySQL Multi-AZ (Amazon RDS) em sub-redes privadas.
* **Segurança (Security Groups):** Grupos de segurança com regras de "menor privilégio".

## Pré-requisitos

1.  Uma conta AWS.
2.  Um Par de Chaves (Key Pair) EC2 já existente na região. Você precisará do nome dele para o parâmetro `KeyName`.

## Passos para Implantação

### 1. Obter seu Endereço IP

Para segurança, a pilha só permite acesso SSH às instâncias a partir do seu IP. Descubra seu IP (Google "what is my ip") e anote-o.

### 2. Implantar a Pilha (Stack)

Use o arquivo `projeto-final-completo.yml`.

#### Opção A: AWS CLI (Recomendado)

Substitua os valores de `SUA_SENHA_SEGURA`, `NOME_DA_SUA_CHAVE_SSH` e `SEU_IP_PUBLICO/32`.

```bash
aws cloudformation deploy \
  --template-file projeto-final-completo.yml \
  --stack-name projeto-final-wordpress \
  --capabilities CAPABILITY_IAM \
  --parameter-overrides \
    DBMasterPassword=SUA_SENHA_SEGURA \
    KeyName=NOME_DA_SUA_CHAVE_SSH \
    SSHLocation=SEU_IP_PUBLICO/32
