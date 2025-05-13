# CLOUDN2
se voce esta vendo isso é pq esta no lugar certo prara receber meu trabalho da n2

# Migração de Aplicativo para AWS – Arquitetura Serverless

Este projeto tem como objetivo demonstrar a migração de um aplicativo para a AWS, utilizando uma arquitetura funcional serverless, com foco em infraestrutura, comunicação entre serviços e análise crítica da transição a partir de uma plataforma PaaS.

## 🌐 Tecnologias e Serviços Utilizados

- **Frontend**: HTML/CSS/JS hospedado em S3 com distribuição via CloudFront
- **Backend**: AWS Lambda com API Gateway
- **Banco de Dados**: Amazon RDS (PostgreSQL ou MySQL)
- **Armazenamento de arquivos**: Amazon S3
- **Segurança**: IAM, Security Groups, Secrets Manager
- **Monitoramento**: CloudWatch

## 🧱 Arquitetura

![Diagrama da Arquitetura](./A_flowchart_diagram_illustrates_an_AWS_serverless_.png)

### Fluxo Principal:

1. O usuário acessa o frontend via **CloudFront**, que serve os arquivos hospedados no **S3**.
2. As chamadas de API são roteadas pelo **API Gateway** para funções **Lambda**.
3. As funções **Lambda** acessam o **RDS** em uma subnet privada.
4. As credenciais sensíveis são gerenciadas pelo **Secrets Manager**.
5. Logs e métricas são gerados no **CloudWatch**.

## 🛠️ Como rodar localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/nome-do-repositorio.git
