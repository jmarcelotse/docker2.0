# WORKDIR

A instrução **WORKDIR** em um Dockerfile define o diretório de trabalho para qualquer instrução **RUN**, **CMD**, **ENTRYPOINT**, **COPY**, e **ADD** subsequentes. Simplificando, **WORKDIR** estabelece um diretório padrão dentro do contêiner onde comandos e operações serão executados.

# Como o **WORKDIR** Funciona

    1. **Estabelece um Contexto de Diretório**:
        - Quando você define um diretório de trabalho usando **WORKDIR**, qualquer instrução que segue esse comando será executada a partir desse diretório.

        - Se o diretório especificado não existir, o Docker o criará automaticamente.

# Exemplo Simples

Vamos considerar um exemplo simples para ilustrar o uso de **WORKDIR**:

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os arquivos para o diretório de trabalho
    COPY . .

    # Executa a aplicação Python
    CMD ["python", "app.py"]

Neste exemplo:

1. **FROM python:3.8** define a imagem base.

2. **WORKDIR /app** define **/app** como o diretório de trabalho.

3. **COPY . .** copia todos os arquivos do diretório atual no host para o diretório /app no contêiner.

4. **CMD ["python", "app.py"]** executa o comando **python app.py** dentro do diretório /app.

# Benefícios do WORKDIR

1. **Clareza e Organização**:

    - **WORKDIR** ajuda a manter o Dockerfile organizado e claro, evitando a necessidade de comandos longos e caminhos relativos em cada instrução.

2. **Reutilização de Código**:

    - Definir um diretório de trabalho permite que você reutilize o mesmo caminho de diretório em várias instruções sem repetir o caminho completo.

3. **Criação Automática de Diretórios**:

    - Se o diretório especificado no **WORKDIR** não existir, o Docker o criará automaticamente, o que simplifica o processo de configuração do ambiente.

# Exemplos Avançados

Usando Múltiplos **WORKDIR**

Você pode usar múltiplos **WORKDIR** em um Dockerfile para mudar o diretório de trabalho ao longo da construção da imagem:

    FROM node:14

    # Define o diretório de trabalho para o código-fonte
    WORKDIR /app/src

    # Copia os arquivos de código-fonte
    COPY src/ .

    # Instala as dependências
    WORKDIR /app
    COPY package.json .
    RUN npm install

    # Volta ao diretório de código-fonte para a execução
    WORKDIR /app/src
    CMD ["node", "index.js"]

Neste exemplo:

1. **WORKDIR /app/src** define **/app/src** como o diretório de trabalho.

2. **COPY src/ .** copia os arquivos do diretório src do host para /app/src no contêiner.

3. **WORKDIR /app** muda o diretório de trabalho para **/app**.

4. **COPY package.json .** copia package.json para **/app**.

5. **RUN npm install** instala as dependências no diretório **/app**.

6.  **WORKDIR /app/src** muda de volta o diretório de trabalho para **/app/src** para executar o comando **CMD**.

# Combinação com Variáveis de Ambiente

Você pode usar variáveis de ambiente com **WORKDIR** para maior flexibilidade:

    FROM python:3.8

    # Define uma variável de ambiente
    ENV APP_HOME /usr/src/app

    # Usa a variável de ambiente para definir o diretório de trabalho
    WORKDIR $APP_HOME

    # Copia os arquivos para o diretório de trabalho
    COPY . .

    # Executa a aplicação Python
    CMD ["python", "app.py"]

Neste exemplo:

1. **ENV APP_HOME /usr/src/app** define uma variável de ambiente chamada APP_HOME.

2. **WORKDIR $APP_HOME** usa essa variável para definir o diretório de trabalho.

# Conclusão

A instrução **WORKDIR** no Dockerfile é uma ferramenta essencial para definir e organizar o diretório de trabalho dentro de um contêiner Docker. Ela facilita a construção de imagens mais limpas e organizadas, melhora a legibilidade do Dockerfile e simplifica a gestão de caminhos de diretórios, garantindo que comandos e operações subsequentes sejam executados no contexto correto.

##

Dockerfile3

    FROM ubuntu
    RUN apt update && apt install curl -y
    WORKDIR /app

Construir imagem

    docker build -t ubuntu-curl -f Dockerfile3 .

    docker container run -it ubuntu-curl /bin/bash