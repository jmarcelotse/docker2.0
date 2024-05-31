# EXPOSE

A instrução **EXPOSE** no Dockerfile é usada para documentar quais portas o contêiner escutará em tempo de execução. Embora essa instrução não abra realmente as portas, ela serve como uma indicação para outros desenvolvedores sobre quais portas o contêiner espera receber tráfego. Essa informação pode ser utilizada por ferramentas de orquestração de contêineres e sistemas de rede para configurar automaticamente as regras de rede apropriadas.

# Sintaxe

A sintaxe básica da instrução **EXPOSE** é a seguinte:

    dockerfile

    EXPOSE <porta> [<porta>/<protocolo>...]

 - <porta>: O número da porta que o contêiner irá escutar.

 - <protocolo>: Opcionalmente, você pode especificar o protocolo (tcp ou udp). Se nenhum protocolo for especificado, o Docker assume tcp.

# Exemplos

**Exemplo Simples**

Vamos criar um Dockerfile que usa a instrução **EXPOSE** para documentar uma porta:

    dockerfile

    FROM node:14

    # Define o diretório de trabalho
    WORKDIR /usr/src/app

    # Copia os arquivos necessários
    COPY package*.json ./

    # Instala as dependências
    RUN npm install

    # Copia o código-fonte
    COPY . .

    # Expõe a porta 8080
    EXPOSE 8080

    # Define o comando padrão
    CMD ["node", "server.js"]

Neste exemplo, a porta **8080** é exposta, indicando que a aplicação Node.js escutará nessa porta.

**Especificando o Protocolo**

Você também pode especificar o protocolo:

    dockerfile

    FROM ubuntu:20.04

    # Instala o Netcat
    RUN apt-get update && apt-get install -y netcat

    # Expõe a porta 12345 usando UDP
    EXPOSE 12345/udp

    # Mantém o contêiner em execução
    CMD ["sh", "-c", "while true; do echo 'Ouvindo na porta 12345/udp'; sleep 60; done"]

# Usos Comuns

1. **Documentação**:

 - A principal função da instrução **EXPOSE** é documentar quais portas o contêiner espera receber tráfego. Isso é útil para desenvolvedores e para ferramentas de orquestração que podem usar essa informação para configurar automaticamente as regras de rede.

2. **Configuração de Portas em Sistemas de Orquestração**:

 - Em sistemas como Kubernetes, a instrução EXPOSE pode ser utilizada para configurar automaticamente serviços e mapeamentos de portas.

3. **Facilitação do Uso de -P e -p no docker run**:

 - Quando você usa **docker run -P**, o Docker publica todas as portas expostas com **EXPOSE** automaticamente. Se você usar **-p**, pode mapear essas portas explicitamente.

# Mapeamento de Portas em Tempo de Execução

Para realmente tornar a porta acessível fora do contêiner, você precisa mapear a porta ao iniciar o contêiner com **docker run**:

    sh

    docker run -p 8080:8080 minha-imagem

Neste comando:

 - A primeira **8080** refere-se à porta no host.

 - A segunda **8080** refere-se à porta no contêiner que foi exposta usando a instrução **EXPOSE**.

# Exemplo Completo com Mapeamento de Porta

Aqui está um exemplo completo de um Dockerfile que usa **EXPOSE** e como mapear a porta ao iniciar o contêiner:

    dockerfile

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os requisitos da aplicação
    COPY requirements.txt .

    # Instala as dependências
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código-fonte
    COPY . .

    # Expõe a porta 5000
    EXPOSE 5000

    # Define o comando padrão
    CMD ["python", "app.py"]

Para construir e executar a imagem:

    sh

    docker build -t minha-app .
    docker run -p 5000:5000 minha-app

Neste exemplo:

1. A aplicação Python é configurada para escutar na porta **5000**.

2. A instrução **EXPOSE 5000** documenta que a aplicação escuta nessa porta.

3. O comando **docker run -p 5000:5000 minha-app** mapeia a porta **5000** do contêiner para a porta **5000** no host, tornando a aplicação acessível externamente.

# Considerações e Boas Práticas

1. **Documentação de Intenção**:

 - Use **EXPOSE** para documentar a intenção de quais portas o contêiner usa. Isso é particularmente útil em equipes ou projetos grandes onde vários desenvolvedores trabalham juntos.

2. **Não Abre Portas por Si Só**:

 - Lembre-se de que **EXPOSE** não abre a porta para o tráfego externo. Para fazer isso, você precisa mapear a porta em tempo de execução usando **docker run -p**.

3. **Melhor Prática em Imagens Públicas**:

 - Ao criar imagens que serão distribuídas publicamente, expor as portas corretas pode ajudar os usuários a entender rapidamente como interagir com o contêiner.

# Conclusão

A instrução **EXPOSE** no Dockerfile é uma ferramenta útil para documentar quais portas um contêiner escutará, facilitando a configuração e uso de contêineres em diversos ambientes. Embora **EXPOSE** não abra as portas diretamente, ele serve como uma dica valiosa para desenvolvedores e ferramentas de orquestração sobre como configurar a rede para o contêiner.

Criar o dockerfile

FROM ubuntu
EXPOSE 80
RUN apt update && apt install nginx -y

    docker build -t ubuntu-curl -f Dockerfile10 .

    docker container run -it ubuntu-curl /bin/bash

     docker container run -it -P ubuntu-curl /bin/bash

     /usr/sbin/nginx -g "daemon off;"

     docker container run -it  -p 8080:80 ubuntu-curl /bin/bash