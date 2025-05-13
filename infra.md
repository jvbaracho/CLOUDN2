Documentação da Infraestrutura AWS – Projeto de Migração

Sumário

1. Rede e Segurança (VPC)

2. IAM (Identidade e Acesso)

3. Armazenamento de Arquivos (S3 + CloudFront)

4. Backend Serverless (Lambda + API Gateway)

5. Banco de Dados (RDS)

6. Gerenciamento de Credenciais (Secrets Manager)

7. Monitoramento (CloudWatch)

1. Rede e Segurança (VPC)

VPC com duas subnets públicas (para Lambda/API) e duas privadas (para RDS)

Tabela de rotas para acesso à internet via Internet Gateway

NAT Gateway configurado para saída de serviços em subnets privadas

Security Groups:

SG-Frontend: permite tráfego HTTP/HTTPS (porta 80/443)

SG-Backend: permite acesso da Lambda ao RDS (porta 5432/3306)

SG-RDS: permite acesso somente de instâncias na subnet privada

2. IAM (Identidade e Acesso)

IAM Role: LambdaExecutionRole

Permissões:

lambda.amazonaws.com

rds:Connect

secretsmanager:GetSecretValue

logs:*

IAM Policy personalizada para acesso apenas ao Secret específico do banco

Roles separadas para deploy e monitoramento

3. Armazenamento de Arquivos (S3 + CloudFront)

Bucket S3 com:

Website hosting ativado

Políticas públicas para leitura (s3:GetObject)

Configuração CORS para frontend

CloudFront:

Origem no bucket S3

Certificado SSL via ACM

TTL configurado para cache de performance

4. Backend Serverless (Lambda + API Gateway)

API Gateway:

Criado como REST API

Recursos definidos como /produtos, /pedidos, etc.

CORS habilitado para todos os métodos

Lambda:

Conectado à VPC (subnet privada)

Acesso ao RDS via SG e VPC

Variáveis de ambiente: DB_HOST, DB_USER, SECRET_ARN

Timeout e memória ajustados conforme a carga

5. Banco de Dados (RDS)

Tipo: PostgreSQL (ou MySQL)

Acesso apenas por VPC privada

Subnet Group configurado com subnets privadas

Security Group aceita conexões apenas da Lambda

Backup e manutenção automática ativados

6. Gerenciamento de Credenciais (Secrets Manager)

Secret criado com chave rds/credentials

Contém: host, port, username, password

Permissão de acesso apenas via LambdaExecutionRole

ARN referenciado nas variáveis de ambiente da Lambda

7. Monitoramento (CloudWatch)

Logs de Lambda enviados para grupos de log nomeados por função

Métricas configuradas:

Invocações por segundo

Erros

Tempo de execução

Alarmes configuráveis com notificações via SNS (opcional)

Observações Finais

A infraestrutura segue boas práticas de segurança e isolamento.

As permissões são mínimas e específicas.

O sistema está pronto para escalar com demandas crescentes sem retrabalho de infraestrutura.

