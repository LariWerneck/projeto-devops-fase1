# 🚀 Containerização com Docker e Deploy Manual na AWS

Este projeto demonstra o processo completo de containerização de uma aplicação web estática utilizando Docker e seu deploy manual em uma instância EC2 na AWS, com gerenciamento de imagens via Amazon ECR.

O objetivo foi simular um fluxo real de deploy utilizado no mercado, aplicando conceitos de DevOps e Cloud Computing.

A atividade foi baseada no projeto original disponível em:
https://github.com/marialazara/laboratorio-devops/tree/main/projeto-devops-fase-1

This repository is available in Portuguese (PT), English (EN), and French (FR).

Ce projet est documenté en portugais, anglais et français afin d’assurer l’accessibilité à un public plus large.

# 🎯 Objetivo do Projeto

- Containerizar um website (HTML, CSS e JavaScript)
- Publicar a imagem Docker em um registry privado (Amazon ECR)
- Provisionar infraestrutura na AWS (EC2)
- Realizar deploy manual via SSH
- Expor a aplicação publicamente via IP


# 🐳 Tecnologias Utilizadas

- Docker
- Nginx (imagem base Alpine)
- AWS CLI
- Amazon ECR
- Amazon EC2
- Linux (Amazon Linux 2023)
- SSH

# 🔨 Processo Executado
## 1 - Containerização
```bash
# Criação do Dockerfile utilizando Nginx como servidor web:
FROM nginx:alpine
COPY website/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Build da imagem:
docker build -t meu-website:v1.0 .
```
## 2 - Teste Local

```bash
# Execução do container:
docker run -d -p 8080:80 --name meu-website-container meu-website:v1.0

# Validação via:
http://localhost:8080
```

## 3 - Publicação no Amazon ECR
```bash
# Autenticação:
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin SEU_ACCOUNT_ID.dkr.ecr.us-east-2.amazonaws.com

# Tag da imagem:
docker tag meu-website:v1.0 SEU_ECR_URI:v1.0

# Push:
docker push SEU_ECR_URI:v1.0
```
## 4 - Provisionamento da EC2

- AMI: Amazon Linux 2023
- Tipo: t2.micro (Free Tier)
- Security Group: SSH (22) – My IP |||| HTTP (80) – 0.0.0.0/0
- IAM Role com permissão de leitura no ECR


## 5 - Deploy na EC2
```bash
# Instalação do Docker:
sudo yum install docker -y
sudo systemctl start docker

# Pull da imagem:
docker pull SEU_ECR_URI:v1.0

# Execução do container:
docker run -d -p 80:80 --name meu-website-prod --restart always SEU_ECR_URI:v1.0

# Acesso público via IP da instância:
http://IP_PUBLICO_DA_EC2
```

# ✅ Resultados

- Aplicação publicada na AWS
- Container rodando em produção
- Exposição via IP público
- Configuração segura de permissões via IAM
- Deploy funcional validado via navegador

# 🧠 Conceitos Aplicados

- Containerização
- Imagens Docker
- Registry privado
- Infraestrutura como serviço (IaaS)
- Gerenciamento de permissões (IAM)
- Deploy manual via SSH
- Configuração de Security Groups
- Execução persistente de containers (--restart always)



# 🇺🇸 🚀 Containerization with Docker and Manual Deployment on AWS

This project demonstrates the complete process of containerizing a static web application using Docker and its manual deployment on an EC2 instance in AWS, with image management via Amazon ECR.

The objective was to simulate a real-world deployment workflow used in the industry, applying DevOps and Cloud Computing concepts.

The activity was based on the original project available at:
https://github.com/marialazara/laboratorio-devops/tree/main/projeto-devops-fase-1

This repository is available in Portuguese (PT), English (EN), and French (FR).

Ce projet est documenté en portugais, anglais et français afin d’assurer l’accessibilité à un public plus large.

# 🎯 Project Objective

- Containerize a website (HTML, CSS, and JavaScript)
- Publish the Docker image to a private registry (Amazon ECR)
- Provision infrastructure on AWS (EC2)
- Perform manual deployment via SSH
- Expose the application publicly via IP address


# 🐳 Technologies Used

- Docker
- Nginx (Alpine base image)
- AWS CLI
- Amazon ECR
- Amazon EC2
- Linux (Amazon Linux 2023)
- SSH

# 🔨 Execution Process
## 1 - Containerization


```bash
# Creating the Dockerfile using Nginx as the web server:
FROM nginx:alpine
COPY website/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Building the image:
docker build -t meu-website:v1.0 .
```
## 2 - Local Testing

```bash
# Running the container:
docker run -d -p 8080:80 --name meu-website-container meu-website:v1.0

# Validation via:
http://localhost:8080
```

## 3 - Publishing to Amazon ECR
```bash
# Authentication:
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin SEU_ACCOUNT_ID.dkr.ecr.us-east-2.amazonaws.com

# Tagging the image:
docker tag meu-website:v1.0 SEU_ECR_URI:v1.0

# Push:
docker push SEU_ECR_URI:v1.0
```
## 4 - EC2 Provisioning

- AMI: Amazon Linux 2023
- Type: t2.micro (Free Tier)
- Security Group: SSH (22) – My IP |||| HTTP (80) – 0.0.0.0/0
- IAM Role with ECR read permissions


## 5 - Deployment on EC2
```bash
# Installing Docker:
sudo yum install docker -y
sudo systemctl start docker

# Pulling the image:
docker pull SEU_ECR_URI:v1.0

# Running the container:
docker run -d -p 80:80 --name meu-website-prod --restart always SEU_ECR_URI:v1.0

# Public access via instance IP:
http://IP_PUBLICO_DA_EC2
```

# ✅ Results

- Application published on AWS
- Container running in production
- Public exposure via IP address
- Secure permission configuration via IAM
- Functional deployment validated via browser

# 🧠 Concepts Applied

- Containerization
- Docker Images
- Private registry
- Infrastructure as a Service (IaaS)
- Permission management (IAM)
- Manual deployment via SSH
- Security Group configuration
- Persistent container execution (--restart always)



# 🇫🇷 🚀 Conteneurisation avec Docker et Déploiement Manuel sur AWS

Ce projet démontre le processus complet de conteneurisation d'une application web statique à l’aide de Docker et son déploiement manuel sur une instance EC2 dans AWS, avec gestion des images via Amazon ECR.

L'objectif était de simuler un flux de déploiement réel utilisé dans l'industrie, en appliquant des concepts DevOps et Cloud Computing.

L’activité était basée sur le projet original disponible à :
https://github.com/marialazara/laboratorio-devops/tree/main/projeto-devops-fase-1

This repository is available in Portuguese (PT), English (EN), and French (FR).

Ce projet est documenté en portugais, anglais et français afin d’assurer l’accessibilité à un public plus large.

# 🎯 Objectif du Projet

- Conteneuriser un site web (HTML, CSS et JavaScript)
- Publier l’image Docker dans un registre privé (Amazon ECR)
- Provisionner l’infrastructure sur AWS (EC2)
- Réaliser un déploiement manuel via SSH
- Exposer l’application publiquement via adresse IP


# 🐳 Technologies Utilisées

- Docker
- Nginx (image de base Alpine)
- AWS CLI
- Amazon ECR
- Amazon EC2
- Linux (Amazon Linux 2023)
- SSH

# 🔨 Processus Réalisé
## 1 - Conteneurisation


```bash
# Création du Dockerfile en utilisant Nginx comme serveur web :
FROM nginx:alpine
COPY website/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Construction de l’image :
docker build -t meu-website:v1.0 .
```
## 2 - Test Local

```bash
# Exécution du conteneur :
docker run -d -p 8080:80 --name meu-website-container meu-website:v1.0

# Validation via :
http://localhost:8080
```

## 3 - Publication sur Amazon ECR
```bash
# Authentification :
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin SEU_ACCOUNT_ID.dkr.ecr.us-east-2.amazonaws.com

# Tag de l’image :
docker tag meu-website:v1.0 SEU_ECR_URI:v1.0

# Push :
docker push SEU_ECR_URI:v1.0
```
## 4 - Provisionnement de l’EC2

- AMI : Amazon Linux 2023
- Type : t2.micro (Free Tier)
- Security Group : SSH (22) – My IP |||| HTTP (80) – 0.0.0.0/0
- IAM Role avec permission de lecture ECR


## 5 - Déploiement sur EC2
```bash
# Installation de Docker :
sudo yum install docker -y
sudo systemctl start docker

# Récupération de l’image :
docker pull SEU_ECR_URI:v1.0

# Exécution du conteneur :
docker run -d -p 80:80 --name meu-website-prod --restart always SEU_ECR_URI:v1.0

# Accès public via IP de l’instance :
http://IP_PUBLICO_DA_EC2
```

# ✅ Résultats

- Application publiée sur AWS
- Conteneur en exécution en production
- Exposition publique via adresse IP
- Configuration sécurisée des permissions via IAM
- Déploiement fonctionnel validé via navigateur

# 🧠 Concepts Appliqués

- Conteneurisation
- Images Docker
- Registre privé
- Infrastructure as a Service (IaaS)
- Gestion des permissions (IAM)
- Déploiement manuel via SSH
- Configuration des Security Groups
- Exécution persistante des conteneurs (--restart always)
