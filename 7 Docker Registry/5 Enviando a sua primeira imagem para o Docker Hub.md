# Enviando a sua primeira imagem para o Docker Hub

Enviar sua primeira imagem Docker para o Docker Hub é um processo relativamente simples. Abaixo está um guia passo a passo para você seguir:

**Passo 1: Criar uma Conta no Docker Hub**

Se você ainda não possui uma conta no Docker Hub, crie uma acessando Docker Hub e registrando-se.

**Passo 2: Fazer Login no Docker Hub pelo Terminal**

Use o comando abaixo para fazer login no Docker Hub a partir do seu terminal:

    sh

    docker login

Você será solicitado a fornecer suas credenciais do Docker Hub (nome de usuário e senha).

**Passo 3: Criar uma Imagem Docker Localmente**

Vamos assumir que você já criou uma imagem Docker localmente usando um Dockerfile. Por exemplo, aqui está um simples Dockerfile:

    Dockerfile

    # Dockerfile exemplo
    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html/
    CMD ["nginx", "-g", "daemon off;"]

Crie um arquivo **index.html** para ser copiado para a imagem:

    html

    <!DOCTYPE html>
    <html>
    <head>
        <title>Bem-vindo ao Nginx</title>
    </head>
    <body>
        <h1>Olá, mundo! O Nginx está funcionando!</h1>
    </body>
    </html>

Construa a imagem usando o comando **docker build**:

    sh

    docker build -t minha-imagem .

**Passo 4: Taguear a Imagem com o Nome Correto**

Para enviar a imagem para o Docker Hub, você precisa taguear a imagem com o seu nome de usuário no Docker Hub e o nome do repositório. A estrutura é **username/repo:tag**.

Suponha que seu nome de usuário no Docker Hub é **meuusuario** e você quer que o repositório seja chamado **meuprimeirorepo** com a tag **v1**:

    sh

    docker tag minha-imagem meuusuario/meuprimeirorepo:v1

**Passo 5: Enviar a Imagem para o Docker Hub**

Agora, você pode enviar a imagem tagueada para o Docker Hub:

    sh

    docker push meuusuario/meuprimeirorepo:v1

**Passo 6: Verificar no Docker Hub**

Depois de enviar a imagem, você pode verificar no Docker Hub, acessando Docker Hub e navegando até o seu repositório. Você deve ver a imagem **meuprimeirorepo** com a tag **v1**.

# Exemplo Completo

Aqui está um exemplo completo que engloba todos os passos:

1. **Criar um Dockerfile**:

    Dockerfile

    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html/
    CMD ["nginx", "-g", "daemon off;"]

2. **Criar um arquivo index.html:**

    html

    <!DOCTYPE html>
    <html>
    <head>
        <title>Bem-vindo ao Nginx</title>
    </head>
    <body>
        <h1>Olá, mundo! O Nginx está funcionando!</h1>
    </body>
    </html>

3. **Construir a Imagem**:

    sh

    docker build -t minha-imagem .

4. **Fazer Login no Docker Hub**:

    sh

    docker login

5. **Taguear a Imagem**:

    sh

    docker tag minha-imagem meuusuario/meuprimeirorepo:v1

6. **Enviar a Imagem**:

    sh

    docker push meuusuario/meuprimeirorepo:v1

7. **Verificar no Docker Hub**:

 - Acesse Docker Hub, faça login e vá para o seu repositório para verificar se a imagem foi enviada corretamente.

# Conclusão

Enviar uma imagem Docker para o Docker Hub envolve criar e taguear a imagem corretamente, fazer login no Docker Hub e usar o comando **docker push**. Seguindo esses passos, você pode compartilhar suas imagens Docker facilmente com outros desenvolvedores e equipes.


###

1. docker login

2. docker push jmarcelotse/conversao-temperatura:v1

3. docker push jmarcelotse/conversao-temperatura:latest

4. docker image rm $(docker image ls -q) Se precisar limpar tudo

5. docker system prune Se precisar limpar tudo

6. docker pull jmarcelotse/conversao-temperatura:v1

7. docker image ls

8. docker container run -d -p 8080:8080 jmarcelotse/conversao-temperatura

9. docker image ls
