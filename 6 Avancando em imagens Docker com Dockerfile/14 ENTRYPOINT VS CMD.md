# ENTRYPOINT VS CMD

**ENTRYPOINT** e **CMD** são instruções no Dockerfile usadas para especificar o comando que será executado quando um contêiner é iniciado. Embora possam parecer semelhantes, elas têm propósitos e comportamentos diferentes. Compreender a diferença entre elas é crucial para criar contêineres Docker que funcionem conforme esperado.

**CMD**

A instrução **CMD** é usada para fornecer comandos padrão que serão executados quando um contêiner é iniciado. A principal característica do **CMD** é que ele pode ser sobrescrito ao iniciar o contêiner.

Existem três formas principais de usar **CMD**:

1. **Exec Form** (Forma preferida):

    dockerfile

    CMD ["executable", "param1", "param2"]

2. **Shell Form**:

    dockerfile

    CMD command param1 param2

3. **Default Parameters for ENTRYPOINT**:

    dockerfile

    CMD ["param1", "param2"]

**Exemplo**

    dockerfile

    FROM ubuntu:20.04

    # Comando padrão
    CMD ["echo", "Hello, World!"]

Ao iniciar o contêiner, ele executará **echo Hello, World!**. Esse comando pode ser sobrescrito ao iniciar o contêiner:

    sh

    docker run minha-imagem echo "Sobrescrevendo o comando"

**ENTRYPOINT**

A instrução **ENTRYPOINT** é usada para definir o comando que sempre será executado quando o contêiner é iniciado. Diferente do **CMD**, **ENTRYPOINT** não pode ser facilmente sobrescrito, mas pode ter argumentos adicionais passados durante a execução do contêiner.

**Sintaxe**

Existem duas formas principais de usar **ENTRYPOINT**:

1. **Exec Form** (Forma preferida):

    dockerfile

    ENTRYPOINT ["executable", "param1", "param2"]

2. **Shell Form**:

    dockerfile

    ENTRYPOINT command param1 param2

**Exemplo**

    dockerfile

    FROM ubuntu:20.04

    # Comando de entrada
    ENTRYPOINT ["echo"]

Ao iniciar o contêiner, ele executará **echo**. Você pode passar argumentos adicionais:

    sh

    docker run minha-imagem "Hello, World!"

Isso resultará em **echo Hello, World!**.

# Usando ENTRYPOINT e CMD Juntos

É comum usar **ENTRYPOINT** e **CMD** juntos para definir um comando base (**ENTRYPOINT**) e seus argumentos padrão (**CMD**). Nesse caso, **CMD** fornece os parâmetros padrão que podem ser sobrescritos.

**Exemplo**

    dockerfile

    FROM ubuntu:20.04

    # Define o comando de entrada
    ENTRYPOINT ["echo"]

    # Define os argumentos padrão
    CMD ["Hello, World!"]

Ao iniciar o contêiner, ele executará **echo Hello, World!**. Você pode sobrescrever os argumentos padrão:

    sh

    docker run minha-imagem "Sobrescrevendo os argumentos"

Isso resultará em **echo Sobrescrevendo os argumentos**.

# Diferenças e Quando Usar

1. **Sobrescrição**:

 - **CMD**: Pode ser facilmente sobrescrito ao iniciar o contêiner.

 - **ENTRYPOINT**: Não pode ser facilmente sobrescrito, mas aceita argumentos adicionais.

2. **Propósito**:

 - **CMD**: Ideal para definir comandos ou parâmetros padrão que podem ser alterados conforme necessário.

 - **ENTRYPOINT**: Ideal para garantir que um comando específico sempre seja executado quando o contêiner inicia.

3. **Combinação**:

 - Usar **ENTRYPOINT** com **CMD** permite definir um comando obrigatório (**ENTRYPOINT**) e fornecer parâmetros padrão que podem ser sobrescritos (**CMD**).

# Exemplo Completo com ENTRYPOINT e CMD

Aqui está um exemplo mais completo combinando **ENTRYPOINT** e **CMD**:

    dockerfile

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os requisitos e instala as dependências
    COPY requirements.txt .
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código-fonte
    COPY . .

    # Define o comando de entrada
    ENTRYPOINT ["python"]

    # Define os argumentos padrão
    CMD ["app.py"]

Ao construir e executar a imagem:

    sh

    docker build -t minha-app .
    docker run minha-app

Isso executará **python app.py**. Se você quiser passar um argumento diferente, pode fazer isso:

    sh

    docker run minha-app other_script.py

Isso executará **python other_script.py**.

# Conclusão

 - **Use CMD** para fornecer um comando padrão que pode ser facilmente sobrescrito ao iniciar o contêiner.

 - **Use ENTRYPOINT** para definir um comando obrigatório que sempre será executado quando o contêiner iniciar.

 - **Combine ENTRYPOINT e CMD** para definir um comando obrigatório com argumentos padrão que podem ser sobrescritos conforme necessário.

Essas instruções ajudam a controlar como seus contêineres se comportam, proporcionando flexibilidade e segurança ao mesmo tempo.

Criar o dockerfile

FROM ubuntu
RUN apt update && apt install curl -y
ENTRYPOINT ["echo", "Hello World!!"]

     docker build -t ubuntu-curl -f Dockerfile12 .

     docker inspect ubuntu-curl

     docker container run ubuntu-curl

FROM ubuntu
RUN apt update && apt install curl -y
ENTRYPOINT ["echo", "Hello World!!"]
CMD ["combinado com o entrypoint"]

    docker build -t ubuntu-curl -f Dockerfile12 .

    docker inspect ubuntu-curl

    docker container run ubuntu-curl teste

    docker container run --entrypoint echo ubuntu-curl teste

FROM ubuntu
RUN apt update && apt install curl -y
WORKDIR /app
COPY --chown=root:root --chmod=100 ./entrypoint.sh .
ENTRYPOINT ["./entrypoint.sh"]
#CMD ["combinado com o entrypoint"]

Cria o entrypoint.sh

#!/bin/bash
if [ -z $1 ]
then
	echo "Iniciando o container sem parametro"
else
	echo "Iniciando o container com o parametro $1"
fi

    docker build -t ubuntu-curl -f Dockerfile12 .

    docker container run ubuntu-curl

    docker container run ubuntu-curl teste

 https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact
