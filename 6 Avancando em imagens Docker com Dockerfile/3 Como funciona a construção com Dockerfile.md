# Como funciona a construção com Dockerfile

A construção de uma imagem Docker a partir de um Dockerfile envolve uma série de passos automatizados, definidos por instruções no próprio Dockerfile. Aqui está um passo a passo detalhado de como funciona esse processo:

1. **Criação do Dockerfile**

O Dockerfile é um arquivo de texto simples que contém instruções sobre como criar uma imagem Docker. Cada linha ou bloco de linhas no Dockerfile define uma etapa no processo de construção da imagem.

2. **Comando docker build**

Para construir uma imagem Docker, você usa o comando **docker build** e especifica o caminho para o Dockerfile e o contexto de construção (os arquivos e diretórios que podem ser necessários para construir a imagem).

3. **Instruções no Dockerfile**

Cada instrução no Dockerfile corresponde a uma camada na imagem final. As instruções comuns incluem:

- **FROM**: Define a imagem base a partir da qual a nova imagem será construída. Esta é a primeira instrução em quase todos os Dockerfiles.

    FROM ubuntu:20.04

- **RUN**: Executa um comando no contêiner durante o processo de construção e cria uma nova camada na imagem. Usado frequentemente para instalar pacotes e dependências.

    RUN apt-get update && apt-get install -y python3

- **COPY** e **ADD**: Copiam arquivos e diretórios do sistema de arquivos do host para o sistema de arquivos do contêiner. **ADD** também pode extrair arquivos de um URL ou de um arquivo tar.

    COPY . /app

- **WORKDIR**: Define o diretório de trabalho para qualquer instrução **RUN**, **CMD**, **ENTRYPOINT**, **COPY** e **ADD** subsequentes.

    WORKDIR /app

- **CMD** e **ENTRYPOINT**: Especificam o comando que será executado quando um contêiner é iniciado a partir da imagem. **CMD** fornece parâmetros padrão para o comando especificado em **ENTRYPOINT** ou define um comando padrão.

    CMD ["python3", "app.py"]

4. **Execução das Instruções**

O Docker processa cada instrução no Dockerfile sequencialmente:

 1. **FROM**: Docker baixa a imagem base, se ainda não estiver no cache local.

 2. **RUN**: Cada comando é executado no contexto da imagem base ou da camada anterior, criando uma nova camada para cada comando. Por exemplo, **RUN apt-get update** e **RUN apt-get install -y python3** criarão duas camadas separadas.

 3. **COPY/ADD**: Arquivos são copiados para o contêiner, criando novas camadas.

 4. **WORKDIR**: Define o diretório de trabalho para as próximas instruções.

 5. **CMD/ENTRYPOINT**: Define o comando que será executado quando o contêiner iniciar.

5. **Camadas de Cache**

O Docker usa um sistema de cache para acelerar o processo de construção. Se uma camada não foi alterada desde a última construção, o Docker reutiliza a camada do cache em vez de reconstruí-la.

6. **Criação da Imagem Final**

Após processar todas as instruções, o Docker cria a imagem final. Cada camada é empilhada para formar a imagem completa, que pode ser executada em um contêiner.

7. **Exemplo Completo de Processo de Construção**

Vamos considerar um Dockerfile simples:

    # Define a imagem base
    FROM python:3.8-slim

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia o arquivo de requisitos para o diretório de trabalho
    COPY requirements.txt .

    # Instala as dependências
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código da aplicação
    COPY . .

    # Exponha a porta que a aplicação irá usar
    EXPOSE 5000

    # Define o comando padrão para rodar a aplicação
    CMD ["python", "app.py"]

Para construir a imagem a partir desse Dockerfile:

    docker build -t minha-aplicacao .

Neste comando:

- **-t minha-aplicacao**: Nomeia a imagem como "minha-aplicacao".
- **.**: Especifica que o contexto de construção é o diretório atual.

# Conclusão

A construção de uma imagem Docker a partir de um Dockerfile é um processo sistemático que segue as instruções definidas no arquivo. Cada instrução adiciona uma camada à imagem, resultando em um ambiente encapsulado e reproduzível que pode ser facilmente distribuído e executado em diferentes ambientes.
