# ENV

A instrução **ENV** no Dockerfile é usada para definir variáveis de ambiente que serão disponíveis no contêiner durante a sua execução. As variáveis de ambiente são úteis para configurar o comportamento da aplicação e armazenar informações que podem variar entre diferentes ambientes, como desenvolvimento, teste e produção.

# Sintaxe

A sintaxe básica do comando **ENV** é a seguinte:

    ENV <nome_da_variável> <valor>

 - <nome_da_variável>: O nome da variável de ambiente.

 - <valor>: O valor atribuído à variável de ambiente.

# Exemplo Simples

Vamos considerar um exemplo simples onde definimos algumas variáveis de ambiente:

    FROM ubuntu:20.04

    # Define variáveis de ambiente
    ENV APP_NAME=myapp
    ENV APP_ENV=production
    ENV APP_VERSION=1.0

    # Exibe as variáveis de ambiente
    CMD ["sh", "-c", "echo Nome da aplicação: $APP_NAME, Ambiente: $APP_ENV, Versão: $APP_VERSION"]

Neste exemplo:

1. **ENV APP_NAME=myapp** define a variável **APP_NAME** com o valor **myapp**.

2. **ENV APP_ENV=production** define a variável **APP_ENV** com o valor **production**.

3. **ENV APP_VERSION=1.0** define a variável **APP_VERSION** com o valor **1.0**.

4. O comando **CMD** exibe os valores das variáveis de ambiente quando o contêiner é executado.

# Usos Comuns

1. **Configurar a Aplicação**:

 - Variáveis de ambiente são frequentemente usadas para configurar a aplicação com valores que podem variar entre diferentes ambientes (desenvolvimento, teste, produção).

    dockerfile

    ENV DATABASE_URL=mysql://user:password@db:3306/mydatabase

2. **Armazenar Informações Sensíveis**:

 - Embora não seja a prática mais segura, variáveis de ambiente podem ser usadas para armazenar informações sensíveis, como chaves de API e senhas.

    dockerfile

    ENV API_KEY=your_api_key_here

3. **Passar Parâmetros para o Comando de Inicialização**:

 - Variáveis de ambiente podem ser usadas para modificar o comportamento do comando de inicialização do contêiner.

    dockerfile

    ENV PORT=8080
    CMD ["node", "server.js"]

4. **Definir Caminhos de Diretório**:

 - Definir caminhos de diretório que serão usados em várias instruções subsequentes no Dockerfile.

    dockerfile

    ENV APP_HOME=/usr/src/app
    WORKDIR $APP_HOME

# Exemplo Avançado

Aqui está um exemplo mais avançado usando variáveis de ambiente para configurar uma aplicação Node.js:

    FROM node:14

    # Define variáveis de ambiente
    ENV APP_HOME=/usr/src/app
    ENV NODE_ENV=production
    ENV PORT=3000

    # Define o diretório de trabalho
    WORKDIR $APP_HOME

    # Copia os arquivos de package.json e package-lock.json
    COPY package*.json ./

    # Instala as dependências do projeto
    RUN npm install

    # Copia todo o código-fonte para o diretório de trabalho
    COPY . .

    # Exponha a porta que a aplicação irá usar
    EXPOSE $PORT

    # Define o comando padrão para iniciar a aplicação
    CMD ["node", "server.js"]

# Considerações e Boas Práticas

1. **Segurança**:

 - Evite colocar informações sensíveis diretamente no Dockerfile, especialmente se ele for armazenado em um repositório público. Use ferramentas de gestão de segredos ou passe essas informações em tempo de execução.

2. **Persistência**:

 - Variáveis definidas com **ENV** no Dockerfile são persistentes e estarão disponíveis em qualquer shell que você iniciar no contêiner.

3. **Substituição em Tempo de Execução**:

 - Você pode substituir as variáveis de ambiente definidas no Dockerfile em tempo de execução usando a opção **-e** com **docker run**.

    sh

    docker run -e APP_ENV=staging myimage

# Exemplo Completo com Substituição em Tempo de Execução

Vamos criar um Dockerfile que define variáveis de ambiente e mostra como substituí-las em tempo de execução:

    dockerfile

    FROM python:3.8

    # Define variáveis de ambiente
    ENV APP_ENV=production
    ENV DEBUG=False

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os requisitos da aplicação
    COPY requirements.txt .

    # Instala as dependências
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código-fonte
    COPY . .

    # Define o comando padrão
    CMD ["sh", "-c", "echo Ambiente: $APP_ENV, Debug: $DEBUG"]

Para substituir as variáveis de ambiente em tempo de execução:

    sh

    docker build -t mypythonapp .

    docker run -e APP_ENV=development -e DEBUG=True mypythonapp

# Conclusão

A instrução **ENV** no Dockerfile é uma ferramenta poderosa para definir variáveis de ambiente que configuram e personalizam o comportamento dos contêineres Docker. Ela ajuda a tornar suas imagens mais flexíveis e adaptáveis a diferentes ambientes, além de facilitar a configuração e o gerenciamento da aplicação.

Criar o Dockerfile

FROM ubuntu
RUN apt update && apt install curl -y
WORKDIR /app
ENV VALOR_DOCKER_ENV="Valor XPTO"

    docker build -t ubuntu-curl -f Dockerfile7 .

    docker container run -it ubuntu-curl /bin/bash

    env

    docker container run -it --env VALOR_DOCKER_ENV="Outro Valor" ubuntu-curl /bin/bash

    env