# Projeto ANOUT_OUT24_D03_AWS

Este repositório contém uma documentação detalhada sobre como configurar e utilizar serviços essenciais da AWS para aplicações, incluindo a criação de instâncias EC2 para banco de dados e APIs, além da configuração de buckets S3. O objetivo é fornecer um guia prático para facilitar a implementação de soluções em nuvem com AWS.

---

## 📄 Documentação

### 1. **Criação de uma Instância EC2 para Banco de Dados**
- Configuração de uma instância EC2 utilizando **Ubuntu** como sistema operacional.
- Passos detalhados para instalar e configurar o banco de dados na instância.
- Inclui boas práticas de segurança e ajustes de rede (como configurações de grupos de segurança e regras de firewall).

Arquivo: [banco-instancia.md](banco-instancia.md)

---

### 2. **Criação de uma Instância EC2 para API**
- Implementação de uma instância EC2 para hospedar uma API.
- Documentação baseada no uso de **Amazon Links** para configurar e gerenciar os serviços de API.
- Instruções para deploy e gerenciamento.

Arquivo: [api-compass.md](api-compass.md)

---

### 3. **Configuração de Buckets S3**
- Guia para criar e configurar buckets S3 na AWS.
- Detalhes sobre permissões, políticas de acesso e armazenamento.
- Utilização prática para armazenar dados ou integrar com outras soluções.

Arquivo: [bucketS3.md](bucketS3.md)

---

### 4. **Deploy**
- Documentação adicional explicando o processo de deploy das instâncias e integração entre os serviços.

Arquivo: [deploy.md](deploy.md)

---

## 📂 Estrutura do Repositório

- `README.md`: Resumo do repositório e links para a documentação.
- `api-compass.md`: Passo a passo para configurar uma instância EC2 para API.
- `banco-instancia.md`: Passo a passo para configurar uma instância EC2 para banco de dados.
- `bucketS3.md`: Guia para configuração de buckets S3.
- `deploy.md`: Documentação complementar para deploy.
- `swagger.json`: Definições da API (Swagger).
- `index.html`: Visualização da documentação (se necessário).

---

## 🛠 Tecnologias Utilizadas

- **AWS EC2**: Para hospedar a API e o banco de dados.
- **AWS S3**: Para armazenamento de dados.
- **Ubuntu**: Sistema operacional das instâncias EC2.

---
