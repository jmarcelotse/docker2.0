# COPY

A instrução **COPY** em um Dockerfile é usada para copiar arquivos e diretórios do sistema de arquivos do host (onde o Dockerfile reside) para o sistema de arquivos de uma imagem Docker durante o processo de construção da imagem. Ela é fundamental para incluir código-fonte, bibliotecas, scripts e outros arquivos necessários na imagem.

# Sintaxe

A sintaxe básica do comando **COPY** é a seguinte:

    COPY [opções] <caminho_origem>... <caminho_destino>

- <caminho_origem>: Especifica o caminho no sistema de arquivos do host para o(s) arquivo(s) ou diretório(s) que você deseja copiar.

- <caminho_destino>: Especifica o caminho dentro do sistema de arquivos do contêiner onde os arquivos serão copiados.

# Exemplo Simples

Vamos considerar um exemplo básico onde copiamos um arquivo chamado **app.py** e um diretório chamado **config** para o contêiner:

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia o arquivo app.py para o diretório de trabalho no contêiner
    COPY app.py .

    # Copia o diretório config para o diretório de trabalho no contêiner
    COPY config/ ./config/

# Detalhes e Boas Práticas

1. **Copiando Arquivos Individuais**:

 - Quando você copia arquivos individuais, você pode especificar o caminho de destino diretamente.

    COPY requirements.txt /app/requirements.txt

2. **Copiando Diretórios**:

 - Ao copiar diretórios, você deve garantir que a estrutura de diretórios seja preservada.

    COPY src/ /app/src/

3. **Usando Padrões Glob**:

 - **COPY** suporta padrões glob, permitindo copiar múltiplos arquivos ou diretórios que correspondem a um padrão.

    COPY *.py /app/

4. **Copiando com Permissões**:

    O **COPY** preserva as permissões dos arquivos e diretórios copiados.

Exemplo Avançado

Vamos ver um exemplo mais avançado que usa várias instruções **COPY** e uma variável de ambiente para organizar melhor o Dockerfile:

    FROM node:14

    # Define uma variável de ambiente para o diretório de trabalho
    ENV APP_HOME /usr/src/app

    # Define o diretório de trabalho
    WORKDIR $APP_HOME

    # Copia o arquivo package.json e package-lock.json para o diretório de trabalho
    COPY package*.json ./

    # Instala as dependências
    RUN npm install

    # Copia todo o código-fonte para o diretório de trabalho
    COPY . .

    # Exponha a porta que a aplicação irá usar
    EXPOSE 8080

    # Define o comando padrão para iniciar a aplicação
    CMD ["node", "server.js"]

# Diferenças entre COPY e ADD

Embora **COPY** e **ADD** possam parecer semelhantes, existem diferenças importantes:

- COPY:

 - Simplesmente copia arquivos e diretórios.
 - Recomendado para a maioria dos casos, pois é mais explícito e previsível.

- ADD:
 - Além de copiar arquivos e diretórios, pode:
   - Descompactar arquivos tar automaticamente.
   - Copiar arquivos de URLs remotos.

 - Pode introduzir comportamento inesperado devido à funcionalidade extra.

 Exemplo de uso de **ADD**:

    ADD https://example.com/file.tar.gz /app/

# Conclusão

A instrução **COPY** no Dockerfile é uma ferramenta essencial para transferir arquivos do host para a imagem Docker durante o processo de construção. Sua simplicidade e previsibilidade a tornam a escolha preferida para a maioria dos casos em que é necessário incluir arquivos e diretórios na imagem.

####

Dockerfile4

FROM ubuntu
RUN apt update && apt install curl -y
WORKDIR /app
COPY arquivo.txt .

    docker build -t ubuntu-curl -f Dockerfile4 .

    docker container run -it ubuntu-curl /bin/bash