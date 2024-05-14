**Formas de criar uma Imagem Docker**

Criar uma imagem Docker envolve basicamente dois métodos principais: usando um Dockerfile ou através do comando docker commit. Vou explicar ambos:

Dockerfile:

Um Dockerfile é um arquivo de texto simples que contém uma lista de instruções que o Docker usa para criar uma imagem.

Comece criando um arquivo chamado Dockerfile em um diretório vazio.

Dentro do Dockerfile, você escreverá as instruções para construir sua imagem. Isso pode incluir coisas como copiar arquivos para dentro da imagem, instalar software, definir variáveis de ambiente, entre outras coisas.

Aqui está um exemplo básico de um Dockerfile:

Aqui está um exemplo básico de um Dockerfile:

    #Use uma imagem base
    FROM ubuntu:latest

    Execute comandos para instalar pacotes ou configurar o ambiente
    RUN apt-get update && apt-get install -y \ nginx \ && rm -rf /var/lib/apt/lists/*

    Copie seus arquivos para dentro da imagem
    COPY ./meu_app /var/www/meu_app

    Defina variáveis de ambiente
    ENV PORT=80

    #Exponha portas
    EXPOSE $PORT

    Comando padrão a ser executado quando o contêiner é iniciado
    CMD ["nginx", "-g", "daemon off;"]

Depois de criar seu Dockerfile, você pode construir sua imagem usando o comando docker build, por exemplo:

    docker build -t nome_da_imagem .
