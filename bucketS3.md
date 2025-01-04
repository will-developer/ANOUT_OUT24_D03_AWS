### **Como fazer upload de um site estático em uma bucket S3 na AWS**

---

#### **Passo 1**: Baixar o arquivo JSON do Swagger  
1. Acesse o link do Swagger gerado no processo anterior e adicione `-json` no final da URL, conforme o exemplo no print.  

![1b](https://github.com/user-attachments/assets/a8aefda2-b65e-49ab-b3a2-2bfdf831e1a6)

2. Clique com o botão direito na página JSON e selecione "Salvar como". Salve o arquivo como `swagger.json` em uma pasta no seu computador.   

![1 1b](https://github.com/user-attachments/assets/41efbf93-13a0-48b7-9d18-60d7f00ca311)

---

#### **Passo 2**: Instalar o ReDoc e converter o JSON em HTML  

##### - **Instalar o ReDoc**  
1. Certifique-se de ter o Node.js e o npm instalados no sistema:  
   ```bash
   node -v
   ```
   
    ```bash
   npm -v
   ``` 
   Se não estiver instalado, baixe e instale o Node.js: [https://nodejs.org](https://nodejs.org).  

2. Instale o ReDoc globalmente:  
   ```bash
   npm install -g redoc-cli
   ```

##### - **Converter o arquivo JSON em HTML**  
1. Abra o Git Bash e navegue até a pasta onde o arquivo JSON foi salvo:  
   ```bash
   cd /c/caminho/para/sua/pasta
   ```  

2. Converta o arquivo `swagger.json` para `index.html`:  
   ```bash
   redoc-cli bundle swagger.json -o index.html
   ```  

![2 1b](https://github.com/user-attachments/assets/90ae7101-cbbb-4028-9ffd-8299f09f4e65)

3. Abra o arquivo HTML no navegador para conferir o resultado.  

![2 2b](https://github.com/user-attachments/assets/a11b224e-d413-4a70-9ba7-33cda2734c64)
![2 3b](https://github.com/user-attachments/assets/8690fbd8-2b68-4226-8a51-cfad8aea2482)

---

#### **Passo 3**: Criar uma Bucket no AWS S3  
1. Acesse o console AWS e procure por **S3**.  
   
![3b](https://github.com/user-attachments/assets/3b4b3978-b9f1-41ed-9dd6-0f54ecbf286f)

2. Clique em **Create Bucket**.  

![4b](https://github.com/user-attachments/assets/16c77fd3-1ba4-47d7-ac36-4fcfdbaca523)

---

#### **Passo 4**: Configurar a Bucket  
1. Insira um nome para a bucket em **Bucket Name**.  

![5 1b](https://github.com/user-attachments/assets/e0061121-4088-4ebc-9d27-2a6e187cb8a5)

2. Em **Block Public Access settings for this bucket**, desmarque **Block all public access** e marque a opção:  
   **I acknowledge that the current settings might result in this bucket and the objects within becoming public**.  
 
![5 2b](https://github.com/user-attachments/assets/f9f8b340-7825-4c10-8604-8b4fc48a27a5)

3. Clique em **Create Bucket**.  

![5 3b](https://github.com/user-attachments/assets/541fe0ba-f53e-4c1d-b526-3a1499a8ddbb)

---

#### **Passo 5**: Habilitar a função de hospedagem de site estático  
1. Clique em **View Details** na bucket criada.  

![5 4b](https://github.com/user-attachments/assets/f330f8c1-4685-494c-9308-2619f516475b)

2. Vá até a aba **Properties**, encontre a seção **Static website hosting** e clique em **Edit**.  

![6 1b](https://github.com/user-attachments/assets/e79d2808-7cfb-417f-a2d9-506e0ada63fb)
![6 2b](https://github.com/user-attachments/assets/9c14aff0-47fb-4268-b137-80922f46924d)

3. Habilite a opção **Enable**, insira `index.html` em **Index Document** e salve as alterações.  
   
![6 3b](https://github.com/user-attachments/assets/86235c1a-6454-4466-96d1-07d2ced23e97)

---

#### **Passo 6**: Configurar permissões para arquivos públicos  
1. Vá até a aba **Permissions**, localize **Object Ownership** e clique em **Edit**.  
 
![7 1b](https://github.com/user-attachments/assets/d6212b64-2d30-4e6a-80dd-4496e1f67df5)

2. Alterne para **ACLs enabled**, habilite **I acknowledge that ACLs will be restored** e salve as alterações.  

![7 2b](https://github.com/user-attachments/assets/f3734739-6732-4fe5-bf12-8141cf15f21d)

3. Em **Access control list (ACL)**, clique em **Edit**:  
   - Habilite **Read** na seção **Everyone (public access)**.  
   - Marque **I understand the effects of these changes on my objects and buckets**.  
   - Salve as alterações.  
  
![7 3b](https://github.com/user-attachments/assets/83223468-569f-4e19-bc88-1f9ecad5fc85)
![7 4b](https://github.com/user-attachments/assets/aab1432c-79d0-4183-b560-e51ad2eee8de)

---

#### **Passo 7**: Fazer upload do arquivo `index.html`  

1. Vá para a aba **Objects** e clique em **Upload**.  

![8 1b](https://github.com/user-attachments/assets/47e5dbbd-d929-4dc9-8f4a-b3933b52c4f2)

2. Clique em **Add Files**, selecione o arquivo `index.html` gerado, e clique em **Abrir**.  
 
![8 2b](https://github.com/user-attachments/assets/e8704df5-4e25-4e3b-a89b-a76381182be0)

3. Habilite o arquivo, vá para **Permissions**, altere **Predefined ACLs** para **Grant public-read access**, marque a opção adicional, e clique em **Upload**.  
   
![8 3b](https://github.com/user-attachments/assets/423e05c2-5f0e-486e-9800-ed8f19000add)

---

#### **Passo 8**: Acessar o site hospedado  
1. Clique no arquivo enviado para abrir os detalhes.  
   
![9 1b](https://github.com/user-attachments/assets/a1999282-9d61-4b10-b4fd-b3aa0abb0b27)

2. Copie a **Object URL** fornecida e acesse no navegador para visualizar o site.  

![9 2b](https://github.com/user-attachments/assets/5d5e575a-6183-4d79-8ec6-fa4b8a819525)
![9 3b](https://github.com/user-attachments/assets/c7b8a45a-b6d7-42f0-86a3-db1d4b9298d7)

---  
