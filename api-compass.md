# Como criar uma instância EC2 para sua aplicação

## 1. Acesse o console da AWS e procure por EC2:

![1](https://github.com/user-attachments/assets/777ce660-643f-4b43-af7c-06bf1613653d)

## 2. Vá em 'Instance' e clique em 'Launch Instances':

![2](https://github.com/user-attachments/assets/1843d695-19f2-4309-98a2-44dd62cb22f0)

## 3. Clique em Add additional tags:

![3](https://github.com/user-attachments/assets/36c2941f-75e7-4800-a721-9b01434927f8)

## 4. É muito importante colocar os nomes como mencionado no print abaixo, senão poderá dar erro na hora de criar a instância:
- Clique em `Add new tag` para adicionar novos campos:  
  - **Name**: CompassCarApi *(aqui pode ser qualquer nome)*  
  - **CostCenter**: test  
  - **Project**: test  
- Importante selecionar `Instances` e `Volumes` em `Resource types`.

![4](https://github.com/user-attachments/assets/79caec5f-ce29-4756-8867-c5070765add3)

## 5. Logo abaixo você poderá selecionar o sistema. Recomendamos que selecione o Amazon Linux com as configurações definidas por padrão:

![5](https://github.com/user-attachments/assets/2fa32138-e720-423d-b341-f10cf78b6188)

## 6. Em 'Instance type', deixe como `t2.micro` (como vem selecionado por padrão):

![6](https://github.com/user-attachments/assets/b8b41c31-7e82-4b2f-a008-fafac1bf7c96)

## 7. Em 'Key pair (login)':
- Clique em `Create new key pair`.
- Em `Enter key pair name`, escreva: **compassCarKey**.
- Selecione a opção `.ppk`.
- Clique em `Create key pair`.

![7 1](https://github.com/user-attachments/assets/9759e9ac-324f-4483-94e0-a93181473c11)
![7 2](https://github.com/user-attachments/assets/555059ae-ea6c-4d05-ac00-7dd40e3a2933)


- É importante guardar esse arquivo em um local seguro, pois será necessário para abrir a instância que estamos criando:  

![7 3](https://github.com/user-attachments/assets/8a63fcd0-0a02-45c9-abcc-9f3978144061)


## 8. No 'Network Settings', precisamos fazer algumas configurações:
- Deixe selecionado `Create security group`, habilite `Allow HTTPS` e `Allow HTTP` e clique em `Edit`:  

![8 1](https://github.com/user-attachments/assets/fb12b759-4df5-4601-b2d9-9d6f8513ae05)

- Troque o nome em `Security group name` para **compass-car-security**:  

![8 2](https://github.com/user-attachments/assets/fc8b9c86-1a69-4147-98fd-f4eea3620d14)

- Clique em `Add security group rule` e depois preencha os campos conforme o print abaixo:  
  - **Type**: Custom TCP  
  - **Source Type**: Anywhere  
  - **Port Range**: 3000  

![8 3](https://github.com/user-attachments/assets/5f3cfa2a-6ab5-4e2c-a0b0-e5defa915244)
![8 4](https://github.com/user-attachments/assets/a9c1611a-d30c-4793-9b55-920dffa007e1)

## 9. Em 'Configure Storage' e 'Advanced details', não precisa mexer em nada. Por fim, basta clicar em `Launch Instance`:

![9](https://github.com/user-attachments/assets/b0f4670e-2565-45a7-8676-1d68da2eb94e)

## 10. Se tudo funcionar corretamente, você verá uma flag escrita `Success`:

![10](https://github.com/user-attachments/assets/bfb2358d-ef8c-4d32-9099-b6863ad0de40)

