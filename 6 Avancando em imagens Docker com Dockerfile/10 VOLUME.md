# VOLUME

A instrução **VOLUME** no Dockerfile é usada para criar um ponto de montagem no contêiner. Um volume em Docker é uma maneira de persistir dados gerados e usados por contêineres. Eles existem fora do ciclo de vida do contêiner, o que significa que você pode parar, remover ou recriar contêineres sem perder dados armazenados em volumes.

# Sintaxe

A sintaxe básica do comando **VOLUME** é a seguinte:

    dockerfile

    VOLUME ["<ponto_de_montagem>"]

 - <ponto_de_montagem>: O caminho dentro do contêiner onde o volume será montado.

# Exemplos

**Exemplo Simples**

Vamos criar um Dockerfile que usa a instrução **VOLUME** para definir um ponto de montagem para dados:

    dockerfile

    FROM ubuntu:20.04

    # Cria um volume no contêiner no diretório /data
    VOLUME ["/data"]

    # Comando padrão que será executado
    CMD ["sh", "-c", "echo 'Dados persistidos em /data' && sleep infinity"]

Neste exemplo, o diretório **/data** no contêiner é definido como um volume. Isso significa que quaisquer dados gravados nesse diretório serão armazenados fora do sistema de arquivos do contêiner.

# Usos Comuns

1. **Persistência de Dados**:

 - Volumes são usados para persistir dados que precisam sobreviver à recriação de contêineres, como bancos de dados ou arquivos de configuração.

    dockerfile

    FROM mysql:5.7
    VOLUME ["/var/lib/mysql"]

2. **Compartilhamento de Dados entre Contêineres**:

 - Volumes podem ser compartilhados entre vários contêineres, facilitando o compartilhamento de dados.

    dockerfile

    FROM ubuntu:20.04
    VOLUME ["/shared-data"]

3. **Isolamento de Dados**:

 - Volumes ajudam a isolar dados gerados por contêineres, permitindo uma melhor organização e gerenciamento dos dados.

    dockerfile

    FROM nginx:latest
    VOLUME ["/var/log/nginx"]

# Montagem de Volumes em Tempo de Execução

Você pode montar volumes em tempo de execução usando a opção **-v** com **docker run**:

    sh

    docker run -v /meu/diretorio/no/host:/data minha-imagem

Neste comando, o diretório **/meu/diretorio/no/host** no host é montado como **/data** no contêiner.

# Exemplo Completo com Montagem de Volume

Vamos criar um Dockerfile que define um volume e demonstra como montá-lo em tempo de execução:

    dockerfile

    FROM node:14

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os arquivos necessários
    COPY . .

    # Instala as dependências do projeto
    RUN npm install

    # Cria um volume para armazenar logs
    VOLUME ["/app/logs"]

    # Define o comando padrão
    CMD ["node", "server.js"]

Para montar o volume em tempo de execução:

    sh

    docker build -t minha-app .

    docker run -v /meu/diretorio/de/logs:/app/logs minha-app

Neste exemplo:

1. O Dockerfile define **/app/logs** como um volume.

2. Em tempo de execução, o diretório **/meu/diretorio/de/logs** no host é montado como **/app/logs** no contêiner, permitindo persistir logs fora do contêiner.

# Vantagens dos Volumes

1. **Persistência de Dados**:

 - Os volumes permitem que os dados sejam mantidos mesmo que o contêiner seja removido.

2. **Desempenho**:

 - Volumes são gerenciados diretamente pelo Docker e geralmente oferecem melhor desempenho do que bind mounts.

3. **Backup e Restauração**:

 - Volumes facilitam o backup e a restauração de dados.

4. **Compartilhamento de Dados**:

 - Volumes podem ser compartilhados entre vários contêineres, facilitando a colaboração e o compartilhamento de dados.

# Conclusão

A instrução **VOLUME** no Dockerfile é uma ferramenta poderosa para a gestão de dados em contêineres Docker. Ela permite a persistência de dados, o compartilhamento de dados entre contêineres e o isolamento de dados, tornando a gestão de dados em contêineres mais eficiente e segura. Usar volumes corretamente pode melhorar significativamente a durabilidade e a flexibilidade das suas aplicações Docker.

Criar o dockerfile

FROM ubuntu
RUN apt update && apt install curl -y
VOLUME /app
ENV VALOR_DOCKER_ENV="Valor XPTO"

     docker build -t ubuntu-curl -f Dockerfile8 .

      docker inspect ubuntu-curl
