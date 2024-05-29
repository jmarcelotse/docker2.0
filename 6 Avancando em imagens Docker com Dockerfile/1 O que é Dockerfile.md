# O que é Dockerfile

O Dockerfile é um arquivo de texto contendo uma série de instruções que definem como criar uma imagem Docker. Uma imagem Docker é um pacote executável leve que inclui tudo o que é necessário para executar uma aplicação: código, runtime, bibliotecas, variáveis de ambiente e arquivos de configuração.

Aqui estão alguns pontos principais para entender o que é e como funciona um Dockerfile:

1. **Base Image**: A maioria dos Dockerfiles começa com uma linha **FROM**, que especifica a imagem base a ser utilizada. Esta imagem base pode ser um sistema operacional como **ubuntu** ou uma imagem de aplicação como **node** para aplicações Node.js.

    FROM ubuntu:20.04

2. **Instruções de Execução**: Estas instruções são comandos que serão executados na imagem base. Comandos comuns incluem **RUN** para executar comandos durante a construção da imagem, **COPY** ou **ADD** para adicionar arquivos ao sistema de arquivos da imagem, **WORKDIR** para definir o diretório de trabalho e **EXPOSE** para expor portas de rede.

    RUN apt-get update && apt-get install -y python3

3. **Definição de Variáveis**: A instrução **ENV** define variáveis de ambiente que estarão disponíveis durante a construção da imagem e no contêiner em execução.

    ENV APP_HOME /app
    WORKDIR $APP_HOME

4. **Comando de Inicialização**: A instrução **CMD** ou **ENTRYPOINT** define o comando a ser executado quando um contêiner é iniciado a partir da imagem. **CMD** é usado para fornecer argumentos padrão para o **ENTRYPOINT** ou para definir um comando padrão se **ENTRYPOINT** não for especificado.

    CMD ["python3", "app.py"]

# Exemplo Completo de Dockerfile

Aqui está um exemplo de um Dockerfile para uma aplicação Python simples:

    # Usa uma imagem base oficial do Python
    FROM python:3.8-slim

    # Define o diretório de trabalho no contêiner
    WORKDIR /app

    # Copia o arquivo de requisitos da aplicação para o diretório de trabalho
    COPY requirements.txt .

    # Instala as dependências da aplicação
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código da aplicação para o diretório de trabalho
    COPY . .

    # Exponha a porta que a aplicação vai usar
    EXPOSE 5000

    # Define o comando padrão a ser executado quando o contêiner iniciar
    CMD ["python", "app.py"]

# Passos para Usar um Dockerfile

1. **Criar o Dockerfile**: Escreva as instruções necessárias em um arquivo chamado **Dockerfile**.

2. **Construir a Imagem**: Use o comando **docker build** para criar uma imagem Docker a partir do Dockerfile.

    docker build -t minha-aplicacao .

3. **Executar o Contêiner**: Use o comando **docker run** para executar um contêiner a partir da imagem criada.

    docker run -p 5000:5000 minha-aplicacao

O Dockerfile é uma parte crucial do Docker, permitindo automatizar e padronizar a construção de ambientes de desenvolvimento, teste e produção, garantindo que a aplicação se comporte da mesma maneira em qualquer lugar onde a imagem seja executada.