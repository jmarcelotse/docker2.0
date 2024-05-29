# docker image ls

O comando **docker image ls** é utilizado no Docker para listar todas as imagens que estão armazenadas localmente na sua máquina. Essas imagens podem ser usadas para criar contêineres Docker. A seguir, explico em detalhe o uso e as opções do comando **docker image ls**:

# Uso Básico

    docker image ls

# Saída Típica

A saída do comando **docker image ls** inclui várias colunas de informações sobre as imagens disponíveis:

- **REPOSITORY**: O nome do repositório ao qual a imagem pertence. Pode ser um nome de imagem personalizado ou um obtido do Docker Hub.

- **TAG**: A tag (etiqueta) da imagem, que geralmente é usada para versionar as imagens.

- **IMAGE ID**: O identificador único da imagem.

- **CREATED**: A data em que a imagem foi criada.

- **SIZE**: O tamanho da imagem no disco.

Exemplo de saída:

    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    nginx               latest              4bb46517cac3        2 days ago          133MB
    ubuntu              18.04               93fd78260bd1        2 weeks ago         64.2MB
    mysql               5.7                 f0f2e0f5ff5d        3 weeks ago         372MB

# Opções Comuns

- **-a, --all**: Mostra todas as imagens (não apenas as mais recentes).

- **-q, --quiet**: Mostra apenas os IDs das imagens.

- **--filter, -f**: Filtra a lista de imagens de acordo com um critério específico.

# Exemplos de Uso

1. Listar todas as imagens (incluindo as intermediárias):

    docker image ls -a

2. Mostrar apenas os IDs das imagens:

    docker image ls -q

3. Filtrar as imagens pelo nome do repositório:

    docker image ls -f reference=nginx

4. Filtrar as imagens pelo tamanho:

    docker image ls -f "dangling=true"

# Explicação dos Filtros

 - **reference**: Filtra as imagens de acordo com o nome do repositório e a tag.

 - **dangling**: Filtra as imagens que não têm nenhuma tag associada.

 - **label**: Filtra as imagens de acordo com as etiquetas de metadados.

# Combinação de Filtros

Você pode combinar múltiplos filtros para refinar ainda mais a lista de imagens. Por exemplo:

    docker image ls -f reference=ubuntu -f before=nginx:latest

Isso lista as imagens do Ubuntu criadas antes da imagem mais recente do Nginx.

# Resumo

O comando **docker image ls** é uma ferramenta essencial para gerenciar e visualizar as imagens Docker no seu sistema local. Ele permite que você tenha uma visão clara das imagens disponíveis, seu tamanho e quando foram criadas, e oferece uma variedade de opções para filtrar e personalizar a saída de acordo com suas necessidades.

# docker image history conversao-temperatura

O comando **docker image history** é utilizado para exibir o histórico de camadas de uma imagem Docker. Cada camada representa uma instrução no Dockerfile que foi utilizada para construir a imagem. Esse comando é útil para entender como uma imagem foi construída e para depurar problemas relacionados ao processo de build.

#Uso Básico

Para usar o comando **docker image history**, você precisa especificar o nome ou o ID da imagem da qual deseja ver o histórico. Por exemplo, se você tem uma imagem chamada **conversao-temperatura**, o comando seria:

    docker image history conversao-temperatura

# Saída Típica

A saída do comando **docker image history** inclui várias colunas de informações sobre as camadas da imagem:

- **IMAGE**: O ID da imagem ou camada.

- **CREATED**: Quanto tempo atrás a camada foi criada.

- **CREATED BY**: O comando que foi executado para criar essa camada.

- **SIZE**: O tamanho da camada.

- **COMMENT**: Comentários adicionados durante o build (geralmente vazio).

Exemplo de saída:

    IMAGE          CREATED        CREATED BY                                      SIZE       COMMENT
    <missing>      2 days ago     /bin/sh -c #(nop)  CMD ["python3" "app.py"]     0B         buildkit.dockerfile.v0
    <missing>      2 days ago     /bin/sh -c #(nop) COPY file:abc123 in /app/     5MB        buildkit.dockerfile.v0
    <missing>      2 days ago     /bin/sh -c pip install -r requirements.txt      89MB       buildkit.dockerfile.v0
    <missing>      2 days ago     /bin/sh -c #(nop)  WORKDIR /app                 0B         buildkit.dockerfile.v0
    <missing>      2 days ago     /bin/sh -c #(nop)  FROM python:3.8              98MB       buildkit.dockerfile.v0

# Explicação das Colunas

- **IMAGE**: Se a imagem foi "squashed" (comprimida) em builds anteriores, o ID da camada pode estar ausente e mostrado como <missing>.

- **CREATED**: Mostra quanto tempo atrás a camada foi criada.

- **CREATED BY**: O comando do Dockerfile que gerou a camada. Instruções como RUN, COPY, ADD, etc., aparecem aqui.

- **SIZE**: O tamanho da camada adicionada pela instrução correspondente.

- **COMMENT**: Comentários sobre a camada, muitas vezes deixado em branco.

# Exemplos de Uso

1. Visualizar o histórico de uma imagem específica:

    docker image history conversao-temperatura

2. Exibir o histórico de uma imagem usando o ID:

    docker image history 4bb46517cac3

# Resumo

O comando **docker image history** fornece uma visão detalhada das camadas que compõem uma imagem Docker. Isso inclui informações sobre os comandos do Dockerfile que foram executados para construir a imagem, quando cada camada foi criada e o tamanho de cada camada. Esse comando é útil para depurar problemas no build da imagem e para entender melhor o processo de construção da mesma.

# docker image inspect conversao-temperatura

O comando **docker image inspect** é utilizado para obter detalhes completos sobre uma imagem Docker específica. Ele retorna informações detalhadas em formato JSON, o que pode ser útil para depuração e compreensão detalhada das propriedades e configuração da imagem.

# Uso Básico

Para usar o comando **docker image inspect**, você precisa especificar o nome ou o ID da imagem que deseja inspecionar. Por exemplo, se você tem uma imagem chamada **conversao-temperatura**, o comando seria:

    docker image inspect conversao-temperatura

# Saída Típica

A saída do comando **docker image inspect** é um bloco de dados JSON que contém várias informações sobre a imagem. Abaixo estão algumas das principais seções e campos encontrados na saída:

    [
        {
            "Id": "sha256:4bb46517cac3...",
            "RepoTags": [
                "conversao-temperatura:latest"
            ],
            "Created": "2023-05-28T12:34:56.789Z",
            "DockerVersion": "20.10.7",
            "Architecture": "amd64",
            "Os": "linux",
            "Size": 133000000,
            "VirtualSize": 133000000,
            "Author": "",
            "Config": {
                "User": "",
                "ExposedPorts": {
                    "8080/tcp": {}
                },
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
                ],
                "Cmd": [
                    "python3",
                    "app.py"
                ],
                "Volumes": null,
                "WorkingDir": "/app",
                "Entrypoint": null,
                "OnBuild": null,
                "Labels": {}
            },
            "RootFS": {
                "Type": "layers",
                "Layers": [
                    "sha256:abc123...",
                    "sha256:def456...",
                    "sha256:ghi789..."
                ]
            }
        }
    ]

# Explicação das Principais Seções e Campos

- **Id**: O identificador SHA256 único da imagem.

- **RepoTags**: As tags associadas à imagem, geralmente incluindo o nome do repositório e a tag (por exemplo, conversao-temperatura:latest).

- **Created**: A data e hora em que a imagem foi criada.

- **DockerVersion**: A versão do Docker usada para criar a imagem.

- **Architecture**: A arquitetura da CPU para a qual a imagem foi construída (por exemplo, amd64).

- **Os**: O sistema operacional para o qual a imagem foi construída (por exemplo, **linux**).

- **Size**: O tamanho total da imagem em bytes.

- **VirtualSize**: O tamanho virtual da imagem em bytes.

- **Author**: O autor da imagem, se especificado.

- **Config**: Um objeto contendo várias configurações da imagem:

 - **User**: O usuário padrão que a imagem usa.

 - **ExposedPorts**: As portas expostas pela imagem.

 - **Env**: As variáveis de ambiente definidas na imagem.

 - **Cmd**: O comando padrão que é executado quando um contêiner é iniciado a partir da imagem.

 - **Volumes**: Os volumes definidos na imagem.

 - **WorkingDir**: O diretório de trabalho padrão.

 - **Entrypoint**: O ponto de entrada da imagem, se definido.

 - **Labels**: As etiquetas associadas à imagem.

- **RootFS**: Informações sobre o sistema de arquivos raiz da imagem:

 - **Type**: O tipo de sistema de arquivos (geralmente layers).

 - **Layers**: Uma lista das camadas da imagem, representadas por seus identificadores SHA256.

# Exemplos de Uso

1. Inspecionar uma imagem específica:

    docker image inspect conversao-temperatura

2. Inspecionar uma imagem usando o ID:

    docker image inspect 4bb46517cac3

3. Formatar a saída para mostrar apenas campos específicos:

Por exemplo, para mostrar apenas o ID e o tamanho da imagem:

    docker image inspect --format='{{.Id}}: {{.Size}}' conversao-temperatura

# Resumo

O comando **docker image inspect** fornece uma visão detalhada das propriedades e configurações de uma imagem Docker em formato JSON. Isso inclui informações sobre a criação da imagem, arquitetura, sistema operacional, tamanho, configuração de execução, variáveis de ambiente, portas expostas e muito mais. Essa ferramenta é extremamente útil para depuração e para obter uma compreensão completa da estrutura e configuração de uma imagem Docker.