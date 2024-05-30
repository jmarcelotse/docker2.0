# Criar o dockerfile

exemplo:
    FROM ubuntu
    RUN apt update
    RUN apt upgrade
    RUN apt install curl -y

-  Depois de criado executar o comando:

    docker build -t ubuntu-curl -f Dockerfile

# docker build -t ubuntu-curl -f Dockerfile .

O **comando docker build -t ubuntu-curl -f Dockerfile** é usado para construir uma imagem Docker a partir de um arquivo Dockerfile específico. Vamos analisar cada parte desse comando para entender melhor o que ele faz:

1. **docker build**:

- Este é o comando principal utilizado para construir uma imagem Docker a partir de um Dockerfile.

2. **-t ubuntu-curl**:

- A opção **-t** (tag) é usada para nomear a imagem que está sendo construída. Neste caso, a imagem será chamada de **ubuntu-curl**. Esse nome é útil para identificar a imagem e facilita o uso dela posteriormente, por exemplo, ao executar um contêiner baseado nessa imagem.

3. **-f Dockerfile**:

- A opção **-f** (file) especifica o nome do Dockerfile que deve ser usado. Se não for especificado, o Docker procura por um arquivo chamado **Dockerfile** no diretório atual. Esta opção é útil se o Dockerfile tiver um nome diferente ou estiver localizado em um diretório diferente.

4. **. (ponto)**:

- O ponto **.** no final do comando especifica o contexto de build. O contexto de build é o conjunto de arquivos e diretórios que serão enviados para o daemon do Docker para construir a imagem. O ponto . indica que o contexto é o diretório atual.

# Exemplo de Uso

Vamos supor que você tenha o seguinte Dockerfile no diretório atual:

    # Usa uma imagem base oficial do Ubuntu
    FROM ubuntu:20.04

    # Atualiza a lista de pacotes e instala o curl
    RUN apt-get update && apt-get install -y curl

    # Define um comando padrão (opcional)
    CMD ["curl", "--version"]

Para construir uma imagem a partir deste Dockerfile, você usaria o comando:

    docker build -t ubuntu-curl -f Dockerfile .

# Passos Explicados

1. **Preparação do Dockerfile**:

- Certifique-se de que o Dockerfile está no diretório atual ou especifique o caminho correto no comando **-f**.

2. **Executar o Comando**:

- Execute o comando **docker build** para iniciar o processo de construção da imagem. O Docker lê as instruções no Dockerfile, baixa a imagem base, executa os comandos especificados (como instalação de pacotes) e cria a imagem final.

3. **Resultado**:

- Se o processo for bem-sucedido, você terá uma nova imagem Docker chamada ubuntu-curl. Você pode listar todas as imagens disponíveis no seu sistema com o comando **docker images**.

    docker images ls

4. **Executar um Contêiner a Partir da Imagem:**

- Para testar a nova imagem, você pode executar um contêiner baseado nela:

    docker run --rm ubuntu-curl
    docker container run -it ubuntu-curl /bin/bash

Este comando executará o contêiner e mostrará a versão do **curl** instalada, conforme definido no comando **CMD** do Dockerfile.

# Conclusão

O comando **docker build -t ubuntu-curl -f Dockerfile** . é uma maneira eficiente de criar uma imagem Docker personalizada a partir de um arquivo Dockerfile específico, permitindo que você automatize e padronize o ambiente necessário para sua aplicação ou serviço.
