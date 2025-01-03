Processo completo de deploy de uma aplicação em uma instância EC2 com outra instância EC2 com o banco de dados:  

---

### **Passo 1**  
Acesse o console da AWS e procure por EC2.  

![1](https://github.com/user-attachments/assets/07a03cae-5eb6-4dce-9cb2-5a46ae62f47a)


---

### **Passo 2**  
Clique em **Instances** e selecione o **Instance ID** referente à EC2 criada para a API. No nosso caso, será a instância com o nome *CompassCarApi*.  

![2-ec2](https://github.com/user-attachments/assets/cc97ced5-29f9-45bb-a639-e5b79c0e5e47)

---

### **Passo 3**  
Copie o **Public IPv4 address** da instância selecionada.  

![3-ec2-3](https://github.com/user-attachments/assets/77c23fae-d7df-42ef-91f3-8910b43c7244)

---

### **Passo 4**  
Abra o terminal via PuTTY usando a chave privada salva nos tutoriais anteriores:  

- Abra o PuTTY e insira o username `ec2-user` seguido pelo IPv4 copiado, por exemplo:  
  `ec2-user@<IPv4>`.  

![4-ec2](https://github.com/user-attachments/assets/bac4549d-7551-4bcb-9a0f-7bebd228ae68)

- Em **SSH > Auth > Credentials**, clique em **Browse** e selecione sua chave privada.  

![4-1-11 3](https://github.com/user-attachments/assets/d7859324-2571-45a8-b6ae-6d9bd15b7e34)
![4-2-11 4](https://github.com/user-attachments/assets/9b896fc5-5ddf-44a2-83ee-37aca1204b71)
![4-3-11 5](https://github.com/user-attachments/assets/dd2c259b-6cce-41cd-b229-f72e884a4f17)


- Quando aparecer o alerta *Putty Security Alert*, clique em **Accept**.  

![4-4ec2](https://github.com/user-attachments/assets/231ca3f2-4e71-4e1e-8aad-3cb9814afcf7)

---

### **Passo 5**  
Atualize o sistema, instale o Git, e configure o Node.js com NVM:  

- Atualize o sistema:  
   ```bash
   sudo yum update -y
   ```

- Instale o Git:  
   ```bash
   sudo yum install git -y
   ```

- Baixe e instale o NVM:  
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
   source ~/.nvm/nvm.sh
   ```

    ```bash
   source ~/.nvm/nvm.sh
   ```

- Verifique se o NVM foi instalado corretamente:  
   ```bash
   nvm --version
   ```

- Instale o Node.js com NVM:  
   ```bash
   nvm install 18
   ```

- Verifique a instalação do Node.js e do NPM:  
   ```bash
   node --version
   ```

   ```bash
   npm --version
   ```

![5-ec2](https://github.com/user-attachments/assets/570b6e55-c8bf-4744-aa1e-317cf6f5ff3d)

---

### **Passo 6**  
Clone o repositório da aplicação na instância EC2:  

- Obtenha um Personal Access Token (PAT) no GitHub com permissão **repo**.  

![6 1-ec2](https://github.com/user-attachments/assets/20bd8521-01c5-4a38-a5f6-4359c58c5622)

![6 2-ec2](https://github.com/user-attachments/assets/79c97bc8-4040-430e-b923-cd3d10c267c1)

![6 3-ec2](https://github.com/user-attachments/assets/25db8eb8-a4b6-4811-8496-703ba4cd3eda)

![6 4-ec2](https://github.com/user-attachments/assets/82eedaa1-8c7e-4a1a-9f92-65804234c925)

![6 5-ec2](https://github.com/user-attachments/assets/67918f62-e98e-4c3d-99a5-b6eb952c0563)

![6 6-ec2](https://github.com/user-attachments/assets/a353abd0-c70b-42b2-86ba-ff3d7f0bcef0)


- Faça o clone do repositório:  
   ```bash
   git clone https://<TOKEN>@github.com/<SEU-USUARIO>/<NOME-DO-REPOSITORIO>.git
   ```
   
![6 7-ec2](https://github.com/user-attachments/assets/b051ef4f-ad1b-4247-bdba-579713ac8f3f)

---

### **Passo 7**  
Entre no diretório do projeto e instale as dependências:  

1. Acesse o diretório:  
   ```bash
   cd ANOUT24_D02_COMPASSCAR_ASYNCNEST
   ```

2. Instale as dependências:  
   ```bash
   npm install
   ```

![7-ec2](https://github.com/user-attachments/assets/c3469e96-6ec5-4bc5-86f1-64fed9dd7acc)

---

### **Passo 8**  
Suba a aplicação para testar:  

1. Compile a aplicação:  
   ```bash
   npm run build
   ```

2. Inicie a aplicação:  
   ```bash
   npm run start
   ```

Se estiver tudo certo, a aplicação estará rodando.  

![8-ec2](https://github.com/user-attachments/assets/068cfa69-5bbb-4f60-a2ad-2b468b2bb8d2)

---

### **Passo 9**  
Instale o PM2 para gerenciar a aplicação:  

1. Instale o PM2 globalmente:  
   ```bash
   npm install -g pm2
   ```

2. Inicie a aplicação com o PM2:  
   ```bash
   pm2 start dist/src/main.js --name "nest-app"
   ```

3. Configure o PM2 para iniciar automaticamente após reinicialização:  
   ```bash
   pm2 startup
   ```

   ```bash
   pm2 save
   ```

![9-ec2](https://github.com/user-attachments/assets/2d7019c2-9026-4e35-b8b6-04d05f88488d)

---

### **Passo 10**  
Configure o `.env` para conectar ao banco de dados:  

- Crie o `.env` a partir do `.env.example`:  
   ```bash
   cp .env.example .env
   ```

![10 1-ec2](https://github.com/user-attachments/assets/c23c2ef5-3240-4a7b-ab33-6bc8e27d8efd)


- Edite o `.env` e altere o `DATABASE_URL` substituindo `localhost` pelo **Private IPv4 Address** da instância do banco de dados:  
   ```bash
   nano .env
   ```

![10 2-ec2](https://github.com/user-attachments/assets/0da92033-f59d-48df-bc66-0f91ba57bafe)

Para salvar e sair: pressione `CTRL + O`, `Enter`, e `CTRL + X`.

---

### **Passo 11**  
Finalize a configuração da aplicação com Prisma:  

- Gere o cliente Prisma:  
   ```bash
   npx prisma generate
   ```

- Execute as migrações:  
   ```bash
   npx prisma migrate dev --name init
   ```

- Popule o banco de dados:  
   ```bash
   npx prisma db seed
   ```

![11-ec2](https://github.com/user-attachments/assets/281a3917-4ae4-4379-92ac-0e124978ecad)

---

### **Passo 12**  
Acesse a aplicação:  

- Suba a aplicação novamente:  
   ```bash
   npm run start
   ```

- Copie o **Public IPv4 address** da instância da API.  

![12-ec2](https://github.com/user-attachments/assets/5f7956ec-3fc7-4f2c-90aa-67d439c232e0)


- Acesse no navegador:  
   ```
   http://<PUBLIC_IPV4_ADDRESS>:3000/api
   ```

![12 2-ec2](https://github.com/user-attachments/assets/292c8d96-24a0-49e8-9da1-c647f843a9eb)


--- 
