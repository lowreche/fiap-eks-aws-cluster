# 🚀 Live: Criando Cluster Kubernetes na AWS (EKS) 

Repositório destinado ao laboratório prático da **Pós Tech FIAP - DevOps & Cloud Architecture**. O objetivo deste lab é provisionar um cluster Kubernetes gerenciado (EKS) utilizando o AWS CloudShell e a ferramenta `eksctl`, focando nas permissões do ambiente **AWS Academy**.

---

## 📋 Pré-requisitos

* Acesso ao **AWS Academy Learner Lab**.
* Terminal **AWS CloudShell**.
* Este repositório clonado no ambiente.

---

## 🛠️ Tecnologias Utilizadas

* **Amazon EKS**: Kubernetes Gerenciado.
* **eksctl**: CLI para automação de infraestrutura EKS.
* **kubectl**: CLI para administração do cluster.
* **AWS CloudShell**: Ambiente de execução.

---

## 🏗️ Estrutura de Arquivos

* `cluster.yaml`: Configuração do cluster (instâncias e roles).
* `app.yaml`: Manifesto da aplicação Nginx e LoadBalancer.
* `setup.sh`: Script para instalação do eksctl.

---

## 🚀 Passo a Passo do Laboratório

### 1. Preparação do CloudShell
Execute o comando abaixo para instalar o `eksctl`:

```chmod +x setup.sh
./setup.sh
```
### 2. Ajuste de Permissões (AWS Academy)
No ambiente do AWS Academy, é obrigatório o uso da `LabRole`. Primeiro, identifique o ID da sua conta AWS para configurar o arquivo YAML (cluster.yaml) corretamente:

```bash
aws sts get-caller-identity --query Account --output text
```
### 3. Provisionamento do Cluster
Inicie a criação da infraestrutura (este processo leva entre 15 e 20 minutos):

```
eksctl create cluster -f cluster.yaml
```

### 4. Deploy da Aplicação e Exposição
Com o cluster ativo e os nós em status Ready, execute o deploy da aplicação de teste:

```
kubectl apply -f app.yaml
```

Para visualizar a aplicação rodando na AWS, obtenha a URL do Load Balancer:

```
kubectl get svc nginx-service
```

Copie o endereço listado em EXTERNAL-IP e cole no seu navegador.

### 🧹 Cleanup (Destruição dos Recursos)
Para garantir que o budget do AWS Academy não seja consumido desnecessariamente após a aula:

```
eksctl delete cluster -f cluster.yaml
```

👨‍🏫 Instrutor
Prof. Luiz Reche FIAP Pós Tech - DevOps & Cloud Architecture
