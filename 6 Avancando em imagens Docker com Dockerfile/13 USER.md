# USER

A instrução **USER** no Dockerfile é usada para definir o usuário ou UID (User ID) que será utilizado para executar as instruções subsequentes no Dockerfile e os comandos em tempo de execução no contêiner. Por padrão, os contêineres Docker executam como o usuário root, mas isso pode representar um risco de segurança. Usar a instrução **USER** permite que você execute processos como um usuário não privilegiado, aumentando a segurança do contêiner.

# Sintaxe

A sintaxe básica da instrução **USER** é a seguinte:

    dockerfile

    USER <nome_do_usuário>[:<grupo>]

 - <nome_do_usuário>: O nome do usuário ou UID que será usado.

 - <grupo>: Opcionalmente, você pode especificar um grupo ou GID (Group ID).

# Exemplos

**Exemplo Simples**

Vamos criar um Dockerfile que usa a instrução **USER** para definir um usuário:

    dockerfile

    FROM ubuntu:20.04

    # Cria um usuário chamado 'appuser'
    RUN useradd -m appuser

    # Define 'appuser' como o usuário para executar comandos subsequentes
    USER appuser

    # Define o diretório de trabalho
    WORKDIR /home/appuser

    # Comando padrão
    CMD ["sh", "-c", "echo Executando como $(whoami)"]

Neste exemplo:

1. O comando **useradd -m appuser** cria um novo usuário chamado **appuser**.

2. A instrução **USER appuser** define que todos os comandos subsequentes serão executados como **appuser**.

**Exemplo com Grupo**

Você também pode especificar um grupo ao usar a instrução **USER**:

    dockerfile

    FROM ubuntu:20.04

    # Cria um grupo e um usuário
    RUN groupadd appgroup && useradd -m -g appgroup appuser

    # Define 'appuser:appgroup' como o usuário e grupo para executar comandos subsequentes
    USER appuser:appgroup

    # Define o diretório de trabalho
    WORKDIR /home/appuser

    # Comando padrão
    CMD ["sh", "-c", "echo Executando como $(whoami) do grupo $(id -gn)"]

Neste exemplo:

1. O comando **groupadd appgroup** cria um novo grupo chamado **appgroup**.

2. O comando **useradd -m -g appgroup appuser** cria um novo usuário **appuser** e o adiciona ao grupo **appgroup**.

3. A instrução **USER appuser:appgroup** define que todos os comandos subsequentes serão executados como **appuser** pertencendo ao grupo **appgroup**.

# Usos Comuns

1. **Segurança**:

 - Executar processos como um usuário não privilegiado reduz o risco de segurança, especialmente em contêineres que expõem serviços de rede.

    dockerfile

    FROM nginx:latest

    # Cria um usuário e grupo
    RUN groupadd -r nginx && useradd -r -g nginx nginx

    # Define o usuário e grupo
    USER nginx:nginx

    CMD ["nginx", "-g", "daemon off;"]

2.**Separação de Privilégios**:

 - Usar diferentes usuários para diferentes etapas do build pode ajudar a separar privilégios e proteger o sistema de arquivos.

    dockerfile

    FROM python:3.8

    # Cria um usuário para instalar dependências
    RUN useradd -m builder

    # Define o usuário para instalar dependências
    USER builder

    WORKDIR /home/builder/app

    # Copia e instala dependências
    COPY requirements.txt .
    RUN pip install --user -r requirements.txt

    # Troca para um usuário de runtime
    RUN useradd -m appuser
    USER appuser

    COPY . .

    CMD ["python", "app.py"]

3. Conformidade de Segurança:

 - Muitos ambientes de produção e práticas de DevOps recomendam ou exigem que os contêineres não sejam executados como root para aderir às políticas de segurança.

# Exemplo Completo

Aqui está um exemplo completo de um Dockerfile que cria e usa um usuário não privilegiado:

    dockerfile

    FROM node:14

    # Cria um usuário e grupo para a aplicação
    RUN groupadd -r appgroup && useradd -r -g appgroup appuser

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os arquivos necessários
    COPY package*.json ./

    # Instala as dependências do projeto
    RUN npm install

    # Copia o código-fonte
    COPY . .

    # Ajusta as permissões do diretório de trabalho
    RUN chown -R appuser:appgroup /app

    # Define o usuário e grupo para executar a aplicação
    USER appuser:appgroup

    # Exponha a porta que a aplicação irá usar
    EXPOSE 3000

    # Define o comando padrão
    CMD ["node", "server.js"]

Neste exemplo:

1. Um grupo **appgroup** e um usuário **appuser** são criados.

2. As permissões do diretório de trabalho **/app** são ajustadas para o novo usuário e grupo.

3. A aplicação é executada como **appuser**, garantindo que ela não seja executada como root.

# Considerações e Boas Práticas

1. **Segurança**:

 - Sempre que possível, evite executar contêineres como root. Use a instrução **USER** para especificar um usuário não privilegiado.

2. **Permissões**:

 - Certifique-se de ajustar as permissões dos arquivos e diretórios no contêiner para que o usuário especificado tenha acesso adequado.

3. **Documentação**:

 - Documente no Dockerfile a criação e o uso de usuários para ajudar outros desenvolvedores a entenderem a configuração de segurança do contêiner.

# Conclusão

A instrução **USER** no Dockerfile é essencial para aumentar a segurança dos contêineres Docker, permitindo que processos sejam executados como usuários não privilegiados. Isso ajuda a mitigar riscos de segurança e a aderir às melhores práticas de DevOps. Usar **USER** de forma adequada melhora a robustez e a segurança das aplicações contêinerizadas.

Criar o Docker File

FROM ubuntu
RUN apt update && apt install curl -y
RUN useradd noahtse
USER noahtse

    docker build -t ubuntu-curl -f Dockerfile11 .

    docker inspect ubuntu-curl

    docker container run -it  ubuntu-curl /bin/bash