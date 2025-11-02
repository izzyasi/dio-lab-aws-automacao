# 🚀 Processamento Automatizado de Arquivos com AWS Lambda e S3

Este projeto é um "HandsOn" para demonstrar a criação de um pipeline serverless na AWS para processamento automático de arquivos. O fluxo utiliza o **Amazon S3** para armazenamento de objetos e o **AWS Lambda** para executar o código em resposta a eventos, com os dados sendo registrados no **Amazon DynamoDB**.

O projeto também é configurado para rodar inteiramente em um ambiente local usando **LocalStack**, permitindo o desenvolvimento e testes sem custos e sem a necessidade de acessar a infraestrutura real da AWS.

## ☁️ Fluxo da Arquitetura

O sistema segue o seguinte fluxo de eventos:

1.  **Upload:** O usuário faz o upload de um arquivo (como `.csv` ou `.json`) em um bucket S3.
2.  **Trigger:** O evento de criação de objeto no S3 (`s3:ObjectCreated:*`) dispara automaticamente uma função Lambda.
3.  **Processamento:** A função Lambda (escrita em Python) é executada, lê o conteúdo do arquivo, processa os dados (ex: extrai informações, valida campos) e grava os resultados em uma tabela no DynamoDB.
4.  **Consulta (Opcional):** Uma segunda função Lambda, exposta por um **API Gateway**, permite que usuários externos consultem os dados que foram processados e salvos no DynamoDB.

![Diagrama do Fluxo]()

## 🛠️ Tecnologias Utilizadas

* **AWS S3:** Serviço de armazenamento de objetos para receber os arquivos de entrada.
* **AWS Lambda:** Serviço de computação serverless para executar o código de processamento.
* **AWS DynamoDB:** Banco de dados NoSQL gerenciado para armazenar os dados processados.
* **AWS API Gateway:** (Opcional) Para criar uma API RESTful e expor os dados do DynamoDB.
* **AWS IAM:** Para gerenciar as permissões entre os serviços.
* **Python (Boto3):** Linguagem de programação e SDK da AWS para escrever a lógica da Lambda.
* **LocalStack:** Simulador de ambiente AWS para desenvolvimento e testes locais.

## 💻 Desenvolvimento Local com LocalStack

Para evitar custos e agilizar o desenvolvimento, usamos o LocalStack para simular os serviços AWS localmente.

### Pré-requisitos

* [Python 3.9+](https://www.python.org/)
* [Docker](https://www.docker.com/get-started) (O LocalStack roda em um contêiner Docker)
* [AWS CLI](https://aws.amazon.com/cli/)
* [LocalStack](https://localstack.cloud/)

Você pode instalar as ferramentas Python necessárias com:
```bash
pip install awscli-local localstack boto3
