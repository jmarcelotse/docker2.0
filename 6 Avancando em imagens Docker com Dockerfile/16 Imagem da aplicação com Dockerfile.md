# Imagem da aplicação com Dockerfile

Criacao do dockerfile

    FROM ubuntu
    ARG NODE_MAJOR=22
    RUN apt-get update && \
    apt-get install curl -y && \
    curl -fsSL https://deb.nodesource.com/setup_current.x | bash - && \
    apt-get update && \
    apt install -y nodejs
    WORKDIR /app
    COPY . .
    RUN npm install
    ENTRYPOINT [ "node", "server.js" ]

/home/jmarcelotse/tse/projetos/conversao-temperatura/src

docker build -t conversao-temperatura-dockerfile -f Dockerfile .

docker container run -d -p 8080:8080 conversao-temperatura-dockerfile

docker container ls
