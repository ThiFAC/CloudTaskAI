# CloudTask AI - SaaS de Gerenciamento de Tarefas

> Plataforma SaaS para gerenciamento de tarefas em nuvem, construída com arquitetura moderna e escalável.

---

# 📌 Objetivo do Projeto

O **CloudTask AI** foca na configuração e criação de um ambiente SaaS completo para gerenciamento de tarefas.

O projeto utiliza tecnologias modernas para garantir que a aplicação seja resiliente, segura e escalável na nuvem, servindo como uma base sólida para ferramentas de produtividade.

---

# 🚀 Passo a Passo para Rodar o Projeto

## 1. Pré-requisitos

Certifique-se de ter instalado:

- Docker
- Docker Compose
- Git
- Visual Studio Code
- Extensão **Dev Containers** do VS Code

---

## 2. Clone o Projeto

```bash
git clone https://github.com/ThiFAC/CloudTaskAI.git
cd CloudTaskAI
```

---

## 3. Copie o arquivo de configuração

Crie seu arquivo `.env` a partir do modelo:

```bash
cp .env.example .env
```

---

## 4. Build da aplicação

Execute o build dos containers:

```bash
docker compose up --build
```

Na primeira execução o processo pode levar alguns minutos.

---

## 5. Abrir no Dev Container

Após o build:

1. Abra o projeto no Visual Studio Code.
2. Pressione **F1**.
3. Escolha:

```
Dev Containers: Reopen in Container
```

O VS Code irá recriar o ambiente de desenvolvimento dentro do container.

---

# 🔐 Configuração dos Secrets do Kubernetes

Crie o arquivo de secrets:

```bash
cp infra/k8s/aws/secret.example.yaml infra/k8s/aws/secret.yaml
```

Agora gere os valores em Base64.

### Nome do banco

```bash
echo -n 'cloudtask' | base64
```

### Senha do PostgreSQL

```bash
openssl rand -hex 16 | tr -d '\n' | base64
```

### Secret Key da aplicação

```bash
openssl rand -hex 32 | tr -d '\n' | base64
```

### DATABASE_URL

Substitua **SUA_SENHA** pela senha gerada anteriormente:

```bash
echo -n "postgresql://cloudtask:SUA_SENHA@postgres:5432/cloudtask" | base64
```

Depois cole todos esses valores dentro do arquivo:

```
infra/k8s/aws/secret.yaml
```

---

# ☁️ Configurando as Credenciais da AWS

Crie a pasta das credenciais:

```bash
mkdir -p ~/.aws
```

Abra o arquivo de credenciais:

```bash
nano ~/.aws/credentials
```

Cole as credenciais fornecidas pelo **AWS Academy Learner Lab**.

Exemplo:

```ini
[default]
aws_access_key_id=SEU_ACCESS_KEY
aws_secret_access_key=SUA_SECRET_KEY
aws_session_token=SEU_SESSION_TOKEN
```

---

## Configurando a Região

Crie ou edite o arquivo:

```bash
nano ~/.aws/config
```

Cole:

```ini
[default]
region = us-east-1
output = json
```

---

# 🚀 Deploy da Infraestrutura com AWS CDK

Entre na pasta do CDK:

```bash
cd infra/cdk
```

Verifique se o CDK está instalado corretamente:

```bash
python3 -c "import aws_cdk; print('aws-cdk-lib OK')"
```

Sintetize a infraestrutura:

```bash
cdk synth
```

Caso não exista nenhum erro, execute o deploy:

```bash
./semana-06-cdk-deploy.sh deploy
```

Esse comando criará toda a infraestrutura necessária na AWS.

---

# 🛠 Tecnologias Utilizadas

- Python
- FastAPI
- PostgreSQL
- Docker
- Docker Compose
- Kubernetes
- AWS CDK
- Amazon EKS
- Amazon ECR
- AWS IAM

---

# 📄 Licença

Este projeto é destinado para fins educacionais e estudos sobre arquitetura SaaS utilizando Docker, Kubernetes e AWS.