# LABEL

A instrução **LABEL** no Dockerfile é usada para adicionar metadados à imagem Docker. Esses metadados consistem em pares chave-valor e podem ser utilizados para descrever a imagem, especificar informações sobre o mantenedor, fornecer detalhes sobre a versão e outras informações relevantes.

# Sintaxe

A sintaxe básica do comando **LABEL** é a seguinte:

    LABEL <chave>=<valor> <chave2>=<valor2> ...

 - <chave>: A chave do metadado.

 - <valor>: O valor associado à chave.

# Exemplos

**Adicionando Metadados Simples**

Vamos adicionar alguns metadados básicos a uma imagem Docker:

    FROM ubuntu:20.04

    # Adiciona metadados sobre o mantenedor da imagem
    LABEL maintainer="seu-email@exemplo.com"

    # Adiciona metadados sobre a versão da imagem e descrição
    LABEL version="1.0"
    LABEL description="Esta é uma imagem base personalizada para o Ubuntu 20.04"

**Adicionando Vários Metadados**

Você pode adicionar múltiplos metadados em uma única instrução **LABEL** ou em várias instruções:

    FROM node:14

    # Adiciona múltiplos metadados em uma única linha
    LABEL maintainer="seu-email@exemplo.com" \
      version="1.0" \
      description="Imagem base para aplicações Node.js"

    # Ou adiciona múltiplos metadados usando várias instruções
    LABEL maintainer="seu-email@exemplo.com"
    LABEL version="1.0"
    LABEL description="Imagem base para aplicações Node.js"

# Usos Comuns

1. **Informações sobre o Mantenedor**:

 - Facilita a identificação de quem criou ou mantém a imagem.

    LABEL maintainer="seu-email@exemplo.com"

2. **Versão da Imagem**:

 - Ajuda a rastrear diferentes versões da imagem.

    LABEL version="1.0"

3. **Descrição da Imagem**:

 - Proporciona uma breve descrição da imagem e seu propósito.

    LABEL description="Imagem base para aplicações web com Node.js"

4. **Licença da Imagem**:

 - Especifica a licença sob a qual a imagem é distribuída.

    LABEL license="MIT"

5. **Metadados Customizados**:

 - Qualquer outro metadado que possa ser útil para documentar a imagem ou integrá-la em um sistema maior.

    LABEL build_date="2024-05-30"

# Benefícios do LABEL

1. **Documentação Interna**:

 - Ajuda a documentar a imagem diretamente dentro do Dockerfile, facilitando a manutenção e a compreensão por outros desenvolvedores.

2. **Automação e Integração**:

 - Metadados podem ser utilizados por sistemas de CI/CD, orquestradores de contêineres (como Kubernetes), e outras ferramentas para automação e integração.

3. **Busca e Filtragem**:

 - Alguns registries de Docker e plataformas de gerenciamento de contêineres permitem buscar e filtrar imagens com base em seus metadados.

# Acessando Metadados da Imagem

Você pode visualizar os metadados de uma imagem usando o comando **docker inspect**:

    docker inspect <nome_da_imagem>

Isso exibirá um JSON com várias informações sobre a imagem, incluindo os metadados adicionados com **LABEL**.

# Exemplo Completo

Aqui está um Dockerfile completo que utiliza **LABEL** para adicionar metadados:

    FROM python:3.8

    # Define o diretório de trabalho
    WORKDIR /app

    # Copia os requisitos da aplicação
    COPY requirements.txt .

    # Instala as dependências
    RUN pip install --no-cache-dir -r requirements.txt

    # Copia o código-fonte
    COPY . .

    # Adiciona metadados
    LABEL maintainer="seu-email@exemplo.com"
    LABEL version="1.0"
    LABEL description="Imagem base para uma aplicação Python"
    LABEL license="MIT"

    # Define o comando padrão
    CMD ["python", "app.py"]

# Conclusão

A instrução **LABEL** no Dockerfile é uma ferramenta útil para adicionar metadados às imagens Docker. Esses metadados ajudam na documentação, automação, integração e gerenciamento das imagens, tornando-as mais informativas e fáceis de usar em diversos ambientes e sistemas.

Criar o dockerfile

FROM ubuntu
RUN apt update && apt install curl -y
LABEL contato="jmarcelotse@hotmail.com"
WORKDIR /app
COPY arquivo.txt .
ADD https://www.google.com pagina.html
ADD teste.tar.gz ./

     docker build -t ubuntu-curl -f Dockerfile6 .

     docker inspect ubuntu-curl