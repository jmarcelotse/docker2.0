# ARG

A instrução **ARG** no Dockerfile é usada para definir variáveis de build-time que podem ser passadas para o Docker durante o processo de construção da imagem. Essas variáveis permitem a personalização da construção da imagem sem a necessidade de editar o Dockerfile diretamente. As variáveis definidas com **ARG** são acessíveis apenas durante o build da imagem e não estão disponíveis em tempo de execução do contêiner.

# Sintaxe

A sintaxe básica do comando **ARG** é a seguinte:

    dockerfile

    ARG <nome_da_variável>[=<valor_padrão>]

 - <nome_da_variável>: O nome da variável de build-time.

 - <valor_padrão>: Opcionalmente, você pode definir um valor padrão para a variável.

# Exemplos

**Definindo uma Variável ARG**

Vamos criar um Dockerfile que usa a instrução **ARG** para definir uma variável de build-time:

    dockerfile

    FROM ubuntu:20.04

    # Define uma variável de build-time chamada VERSION
    ARG VERSION

    # Usa a variável VERSION em um comando RUN
    RUN echo "Versão: $VERSION"

Para construir essa imagem passando o valor para **VERSION**, você usa a opção **--build-arg**:

    sh

    docker build --build-arg VERSION=1.0 -t minha-imagem .

Definindo um Valor Padrão

Você também pode definir um valor padrão para a variável **ARG**:

    dockerfile

    FROM ubuntu:20.04

    # Define uma variável de build-time com um valor padrão
    ARG VERSION=latest

    # Usa a variável VERSION em um comando RUN
    RUN echo "Versão: $VERSION"

Ao construir a imagem, se você não fornecer um valor para **VERSION**, o valor padrão latest será usado:

    sh

    docker build -t minha-imagem .

# Usos Comuns

1. **Configuração de Parâmetros de Construção**:

 - **ARG** pode ser usado para passar parâmetros de construção, como versões de software ou caminhos de arquivos.

    dockerfile

    FROM python:3.8

    # Define variáveis de build-time
    ARG APP_NAME=myapp
    ARG APP_VERSION=1.0

    # Usa as variáveis ARG para configurar o build
    RUN echo "Construindo $APP_NAME versão $APP_VERSION"

2. **Credenciais Temporárias**:

 - Embora não seja recomendado para informações sensíveis de longo prazo, ARG pode ser usado para passar credenciais temporárias necessárias durante o build.

    dockerfile

    FROM ubuntu:20.04

    ARG GITHUB_TOKEN

    RUN git clone https://$GITHUB_TOKEN@github.com/usuario/repo.git

3. **Parâmetros de Ambiente de Build**:

 - **ARG** pode ser usado para ajustar o ambiente de build, como locais de servidores de pacotes ou modos de depuração.

    dockerfile

    FROM node:14

    ARG NPM_REGISTRY=https://registry.npmjs.org/

    RUN npm config set registry $NPM_REGISTRY

# Exemplo Completo

Aqui está um exemplo completo de um Dockerfile que utiliza **ARG** para personalizar a construção da imagem:

    dockerfile

    FROM node:14

    # Define variáveis de build-time
    ARG APP_HOME=/usr/src/app
    ARG NODE_ENV=production

    # Usa as variáveis ARG para configurar o ambiente de build
    ENV APP_HOME=$APP_HOME
    ENV NODE_ENV=$NODE_ENV

    # Define o diretório de trabalho
    WORKDIR $APP_HOME

    # Copia os arquivos de package.json e package-lock.json
    COPY package*.json ./

    # Instala as dependências do projeto
    RUN npm install

    # Copia todo o código-fonte para o diretório de trabalho
    COPY . .

    # Exponha a porta que a aplicação irá usar
    EXPOSE 8080

    # Define o comando padrão para iniciar a aplicação
    CMD ["node", "server.js"]

Para construir a imagem com valores personalizados para as variáveis **ARG**:

    sh

    docker build --build-arg APP_HOME=/app --build-arg NODE_ENV=development -t minha-app .

**Diferenças entre ARG e ENV**

 - **ARG**:
  - Disponível apenas durante o build da imagem.

  - Não persiste no contêiner em tempo de execução.

  - Pode ser sobrescrito com a opção **--build-arg**.

 - **ENV**:

  - Disponível durante o build da imagem e em tempo de execução do contêiner.

  - Persiste no contêiner, afetando seu comportamento durante a execução.

  - Pode ser sobrescrito em tempo de execução com a opção **-e** no **docker run**.

# Conclusão

A instrução **ARG** no Dockerfile é uma ferramenta poderosa para passar variáveis de build-time e personalizar o processo de construção de imagens Docker. Ela permite configurar a construção sem modificar diretamente o Dockerfile, tornando o processo mais flexível e reutilizável. Usar **ARG** junto com **ENV** pode proporcionar uma configuração robusta e adaptável tanto durante o build quanto em tempo de execução.

Criar o Dockerfile

FROM ubuntu
RUN apt update && apt install curl -y
WORKDIR /app
ARG VAR_TEXTO="Texto XPTO"
RUN echo $VAR_TEXTO > arquivo.txt

    docker build -t ubuntu-curl -f Dockerfile9 .

    docker container run -it ubuntu-curl /bin/bash

    docker build -t ubuntu-curl -f Dockerfile9 --build-arg VAR_TEXTO=Noah .