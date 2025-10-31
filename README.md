# provisionamentoComoCodigo.trabFinal

Grupo: Rafael, Maria Emília e Warley

O Projeto Final consiste em criar uma estrutura através do AWS CloudFormation. Precisa conter os seguintes serviços:

- Amazon EC2; (obrigatorio)
- Auto Scaling em duas AZ's (com política de scaling); (obrigatorio)
- Elastic Load Balancer em duas AZ's;(obrigatorio)
- Amazon RDS;
- Amazon EFS;
- Security Groups garantindo o menor privilégio necessário para os respectivos recursos; (obrigatorio)

É pretendido mostrar a instância funcionando mesmo ao desligarmos uma das EC2.

OBS: Nosso código copia uma aplicação HTML (jogo da velha) de um bucket S3 (`s3://jogo-da-velha-projeto-final/`) para o EFS.

## Como Implantar

1.  **Bucket S3:** Este template assume que o bucket `s3://jogo-da-velha-projeto-final` e os arquivos da aplicação já existem.

2.  **Implantação via AWS CLI:**

    ```bash
    aws cloudformation deploy \
      --template-file cloud-formation-corrigido.yaml \
      --stack-name projeto-final-grupo \
      --capabilities CAPABILITY_IAM \
      --parameter-overrides \
        KeyName=SEU_PAR_DE_CHAVES \
        SSHLocation=SEU_IP_PUBLICO/32 \
        DBPassword=UmaSenhaForteParaSeuBanco
    ```

3.  **Implantação via Console:**
    * Faça o upload do `cloud-formation-corrigido.yaml`.
    * Preencha os parâmetros:
        * `KeyName`: O nome do seu par de chaves EC2.
        * `SSHLocation`: Seu IP (ex: `190.170.160.150/32`).
        * `DBPassword`: Crie uma senha para o banco de dados.
    * Marque a caixa "Eu reconheço que o AWS CloudFormation pode criar recursos do IAM."
