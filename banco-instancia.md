# Como criar uma instância EC2 para banco de dados MySQL e instalá-lo

## 1. Acesse o console da AWS e procure por EC2:

![1](https://github.com/user-attachments/assets/139da57e-bb3a-4b8c-947d-02f8fa1a9976)

## 2. Vá em 'Instance' e clique em 'Launch Instances':

![2](https://github.com/user-attachments/assets/22089d11-c86a-4630-b692-5bf6a9bc2600)


## 3. Clique em Add additional tags:

![3](https://github.com/user-attachments/assets/e745522a-4e5e-4fb1-9d7f-ec71aa0e99dd)

## 4. É muito importante colocar os nomes como mencionado no print abaixo, senão poderá dar erro na hora de criar a instância:
- Clique em `Add new tag` para adicionar novos campos:  
  - **Name**: MySql-CompassCar *(aqui pode ser qualquer nome)*  
  - **CostCenter**: test  
  - **Project**: test  
- Importante selecionar `Instances` e `Volumes` em `Resource types`.  

![4](https://github.com/user-attachments/assets/aa00e9ba-76f7-4144-9dd0-cef842748b51)

## 5. Logo abaixo você poderá selecionar o sistema. Recomendamos que selecione o Ubuntu com as configurações definidas por padrão:

![BD5](https://github.com/user-attachments/assets/67827989-e585-4d86-aa5c-ede511872b63)

## 6. Em 'Instance type', deixe como `t2.micro` (como vem selecionado por padrão):

![6](https://github.com/user-attachments/assets/c5aaecf2-4c6f-4467-860f-180bf21ecd88)

## 7. Em 'Key pair (login)', selecione a **compassCarKey** que criamos anteriormente na EC2 da API:

![bd7 1](https://github.com/user-attachments/assets/bf0dd114-3fa8-4a4e-99d0-21ae2bf3cd47)

## 8. No 'Network Settings', precisamos fazer algumas configurações:
- Deixe selecionado `Create security group` e clique em `Edit`:  

![bd8 1](https://github.com/user-attachments/assets/f93df4a1-723e-423d-ab50-3d901e66de1f)

- Troque o nome em `Security group name` para **mysql-compass-car-security**:  

![bd8 2](https://github.com/user-attachments/assets/f3412755-c0b0-48ab-bb25-fb7a29b1ebf3)

- Clique em `Add security group rule` e depois preencha os campos conforme o print abaixo:  
  - **Type**: MYSQL/AURORA  
  - **Source Type**: Anywhere
    
![bd8 3](https://github.com/user-attachments/assets/1dfac548-e095-4d3d-bb07-1638c061400e)
![bd8 4](https://github.com/user-attachments/assets/e0c70b05-c440-429e-87d7-f495cb7474c9)


## 9. Em 'Configure Storage' e 'Advanced details', não precisa mexer em nada. Por fim, basta clicar em `Launch Instance`:

![9](https://github.com/user-attachments/assets/5c4ab67a-c5ff-434f-85e9-d9a005b2455a)

## 10. Se tudo funcionar corretamente, você verá uma flag escrita `Success`:

![bd10](https://github.com/user-attachments/assets/4cbc7fee-9909-490b-8721-3573dab97481)

## 11. Acessando a máquina virtual via PuTTY:
- Acesse a instância novamente e clique em `Instance state` relacionada à sua EC2 criada para o banco de dados:  

![11](https://github.com/user-attachments/assets/999df683-1fd3-48ef-a169-77659f656602)

- Salve o endereço **Public IPv4 Address** da sua EC2:  

![11 1](https://github.com/user-attachments/assets/b9f7518a-f0c2-46de-9456-f7f902823523)

- Instale o PuTTY compatível com seu computador físico. Abra-o e, em `Hostname`, escreva: **ubuntu@seuIPV4**. O restante pode deixar como está:

![11 2](https://github.com/user-attachments/assets/11c89f9a-7c29-4ed5-8aff-5d26022cdb4d)


- Agora clique em **SSH > Auth > Credentials** e, em `Private key file for authentication`, clique em `Browse`, acesse sua chave e clique em `Open`:  

![11 3](https://github.com/user-attachments/assets/32b361b4-2d30-4abb-a517-21908ac1278f)
![11 4](https://github.com/user-attachments/assets/b0c98df8-75bc-46a7-972a-e89b3a104cd9)
![11 5](https://github.com/user-attachments/assets/1c7527fd-084e-424a-81bb-5fcea431b8e0)


## 12. Após entrar no terminal, atualize todas as dependências do SO e instale o MySQL:
### Atualizar o sistema:
```bash
sudo apt update && sudo apt upgrade -y
```

### Instalar o MySQL:
```bash
sudo apt install mysql-server -y
```

### Inicie e habilite o MySQL:
```bash
sudo systemctl start mysql
```

```bash
sudo systemctl enable mysql
```

### Verifique o status do MySQL:
```bash
sudo systemctl status mysql
```

![bd12](https://github.com/user-attachments/assets/5e37765e-30e4-48cf-a26d-9bd1aecb929e)

- Certifique-se de que o status está **active (running)**. Aperte `Ctrl + C` para voltar à linha de comando.

## 13. Permitir conexão externa no MySQL:
### Editar arquivo de configuração:
```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

- Encontre a linha:
```text
bind-address = 127.0.0.1
```

![13 1](https://github.com/user-attachments/assets/86210699-cbb1-4187-8499-d19397bc04e3)

- Altere para:
```text
bind-address = 0.0.0.0
```

![13 2](https://github.com/user-attachments/assets/08f4fb35-2933-48fa-a262-f45e7ada2bbb)

- Salve e saia pressionando `Ctrl+O`, `Enter`, e `Ctrl+X`.

## 14. Criar usuário e permissões no MySQL:
### Entre no MySQL:
```bash
sudo mysql
```

### Configure o usuário root:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
FLUSH PRIVILEGES;
EXIT;
```

### Conceda acesso externo:
```bash
mysql -u root -p
```

- Digite a senha `root` (ela não será exibida por segurança). Depois, execute:
```sql
UPDATE mysql.user SET host = '%' WHERE user = 'root';
FLUSH PRIVILEGES;
```

```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

### Reinicie o MySQL:
```bash
sudo systemctl restart mysql
```
