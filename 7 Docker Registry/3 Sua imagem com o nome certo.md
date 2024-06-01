# Sua imagem com o nome certo

Para subir (push) uma imagem Docker para o Docker Hub com o nome correto, siga estes passos detalhados:

**Passo 1: Criar uma Conta no Docker Hub**

Se você ainda não possui uma conta, crie uma acessando Docker Hub e registrando-se.

**Passo 2: Fazer Login no Docker Hub pelo Terminal**

Use o comando abaixo para fazer login no Docker Hub a partir do seu terminal:

    sh

    docker login

Você será solicitado a fornecer suas credenciais do Docker Hub (nome de usuário e senha).

**Passo 3: Criar uma Imagem Docker Localmente**

Vamos assumir que você já criou uma imagem Docker localmente usando um Dockerfile. Por exemplo:

    Dockerfile

    # Dockerfile exemplo
    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html/
    CMD ["nginx", "-g", "daemon off;"]

Construa a imagem usando o comando **docker build**:

    sh

    docker build -t minha-imagem .

**Passo 4: Taguear a Imagem com o Nome Correto**

Para enviar a imagem para o Docker Hub, você precisa taguear a imagem com o seu nome de usuário no Docker Hub e o nome do repositório. A estrutura é **username/repo:tag**.

Suponha que seu nome de usuário no Docker Hub é **meuusuario** e você quer que o repositório seja chamado **minharepo** com a tag **v1**:

    sh

    docker tag minha-imagem meuusuario/minharepo:v1

**Passo 5: Enviar a Imagem para o Docker Hub**

Agora, você pode enviar a imagem tagueada para o Docker Hub:

    sh

    docker push meuusuario/minharepo:v1

**Passo 6: Verificar no Docker Hub**

Depois do push, você pode verificar no Docker Hub, acessando o Docker Hub e navegando até o seu repositório. Você deve ver a imagem **minharepo** com a tag **v1**.

# Exemplo Completo

Aqui está um exemplo completo que engloba todos os passos:

1. **Dockerfile**:

    Dockerfile

    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html/
    CMD ["nginx", "-g", "daemon off;"]

2. **Construir a Imagem**:

    sh

    docker build -t minha-imagem .

3. **Taguear a Imagem**:

    sh

    docker tag minha-imagem meuusuario/minharepo:v1

4. **Enviar a Imagem**:

    sh

    docker push meuusuario/minharepo:v1

Ao seguir esses passos, você garante que a imagem Docker seja corretamente nomeada e enviada para o Docker Hub, onde pode ser acessada e usada por você e sua equipe.

###
