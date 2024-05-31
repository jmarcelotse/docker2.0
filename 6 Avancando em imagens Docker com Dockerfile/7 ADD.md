# ADD

A instrução **ADD** em um Dockerfile é usada para copiar arquivos e diretórios do sistema de arquivos do host para o sistema de arquivos de uma imagem Docker durante o processo de construção da imagem. Embora seja semelhante ao **COPY**, **ADD** oferece funcionalidades adicionais que podem ser úteis em certos cenários.

# Funcionalidades do ADD

1. **Copiar Arquivos e Diretórios**:

 - Como o **COPY**, o **ADD** pode copiar arquivos e diretórios do host para o contêiner.

2. **Descompactar Arquivos Tar**:

 - Se o caminho de origem for um arquivo tar (e não comprimido), o **ADD** o descompacta automaticamente no contêiner.

3. **Copiar Arquivos de URLs Remotos**:

 - O ADD pode copiar arquivos diretamente de URLs remotos para o contêiner.

# Sintaxe

A sintaxe básica do comando **ADD** é a seguinte:

    ADD [opções] <caminho_origem>... <caminho_destino>

 - <caminho_origem>: Especifica o caminho no sistema de arquivos do host ou URL para o(s) arquivo(s) ou diretório(s) que você deseja adicionar.

 - <caminho_destino>: Especifica o caminho dentro do sistema de arquivos do contêiner onde os arquivos serão adicionados.

# Exemplos

**Copiar Arquivos e Diretórios**

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia o arquivo app.py para o diretório de trabalho no contêiner
    ADD app.py .

    # Copia o diretório config para o diretório de trabalho no contêiner
    ADD config/ ./config/

# Descompactar Arquivos Tar

Se você tiver um arquivo tar no host chamado **archive.tar**, ele será descompactado automaticamente no destino especificado:

    FROM busybox

    # Descompacta o arquivo archive.tar no diretório /app do contêiner
    ADD archive.tar /app/

# Copiar Arquivos de URLs Remotos

Você pode usar **ADD** para baixar e copiar um arquivo diretamente de uma URL:

    FROM busybox

    # Baixa o arquivo e o coloca no diretório /app do contêiner
    ADD https://example.com/file.txt /app/

# Considerações e Boas Práticas

1. **Comportamento Automático de Descompactação**:

 - Embora a descompactação automática de arquivos tar possa ser conveniente, ela pode introduzir comportamento inesperado. Utilize essa funcionalidade com cautela.

2. **URLs Remotas**:

 - Baixar arquivos de URLs remotas durante a construção da imagem pode aumentar o tempo de construção e introduzir dependências de rede. É geralmente recomendado fazer o download de arquivos antes do processo de construção e usar **COPY** para incluí-los na imagem.

3. **Preferência pelo COPY**:

 - A recomendação geral é usar **COPY** quando possível, pois é mais explícito e previsível. Utilize

 **ADD** somente quando suas funcionalidades extras forem realmente necessárias.

# Comparação entre ADD e COPY

**Similaridades**:

 - Ambos copiam arquivos e diretórios do sistema de arquivos do host para o contêiner.

 - Ambos preservam as permissões dos arquivos copiados.

**Diferenças**:

 - **COPY** é mais simples e direto, adequado para a maioria das operações de cópia.

 - **ADD** oferece funcionalidades adicionais, como descompactação automática de arquivos tar e download de arquivos de URLs remotas.

# Exemplo Completo Demonstrando ADD e COPY

Vamos criar um Dockerfile que usa tanto **COPY** quanto **ADD** para ilustrar suas diferenças e funcionalidades.

    # Usa uma imagem base oficial do Node.js
    FROM node:14

    # Define uma variável de ambiente para o diretório de trabalho
    ENV APP_HOME /usr/src/app

    # Define o diretório de trabalho
    WORKDIR $APP_HOME

    # Copia os arquivos de package.json e package-lock.json
    COPY package*.json ./

    # Instala as dependências do projeto
    RUN npm install

    # Copia todo o código-fonte para o diretório de trabalho
    COPY . .

    # Adiciona um arquivo de configuração de um URL remoto
    ADD https://example.com/config.json /app/config.json

    # Adiciona e descompacta um arquivo tar local
    ADD archive.tar /app/

    # Exponha a porta que a aplicação irá usar
    EXPOSE 8080

    # Define o comando padrão para iniciar a aplicação
    CMD ["node", "server.js"]

Neste exemplo:

1. **Definimos a imagem base e o diretório de trabalho**.

2. **Usamos COPY para copiar arquivos locais de configuração e código-fonte**.

3. **Usamos ADD para baixar um arquivo de configuração de uma URL remota e descompactar um arquivo tar local**.

# Conclusão

A instrução **ADD** no Dockerfile é uma ferramenta poderosa com funcionalidades adicionais sobre **COPY**. Embora **ADD** ofereça mais recursos, como a descompactação automática de arquivos tar e a capacidade de copiar arquivos de URLs remotas, é recomendado usar **COPY** para operações de cópia simples devido à sua previsibilidade e simplicidade. Utilize ADD apenas quando suas funcionalidades extras forem realmente necessárias, mantendo sempre em mente as melhores práticas de construção de imagens Docker.

Criar dockerfike

    docker build -t ubuntu-curl -f Dockerfile5 .

    docker container run -it ubuntu-curl /bin/bash