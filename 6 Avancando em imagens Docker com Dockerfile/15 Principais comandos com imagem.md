# Principais comandos com imagem

Ao trabalhar com Docker, há uma série de comandos fundamentais que você usará para gerenciar imagens. Esses comandos permitem construir, listar, inspecionar, remover, exportar e manipular imagens Docker de diversas maneiras. Aqui estão alguns dos principais comandos relacionados a imagens Docker:

1. **Construir uma Imagem (docker build)**

O comando **docker build** é usado para criar uma imagem a partir de um Dockerfile.

    sh

    docker build -t <nome-da-imagem>:<tag> <caminho-do-dockerfile>

    Exemplo:

    sh

    docker build -t minha-imagem:latest .

2. **Listar Imagens (docker images)**

O comando **docker images** lista todas as imagens Docker armazenadas localmente.

    sh

    docker images

3. **Remover Imagens (docker rmi)**

O comando **docker rmi** é usado para remover uma ou mais imagens.

    sh

    docker rmi <imagem_id> | <nome-da-imagem>:<tag>

    exemplo:

    sh

    docker rmi minha-imagem:latest

4. **Inspecionar Imagens (docker inspect)**

O comando **docker inspect** retorna informações detalhadas sobre uma imagem.

    sh

    docker inspect <imagem_id> | <nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker inspect minha-imagem:latest

5. **Taguear Imagens (docker tag)**

O comando **docker tag** é usado para criar uma nova tag para uma imagem existente.

    sh

    docker tag <imagem_id> <novo-nome-da-imagem>:<nova-tag>

    Exemplo:

    sh

    docker tag minha-imagem:latest meu-repositorio/minha-imagem:1.0

6. **Fazer Push de Imagens (docker push)**

O comando **docker push** é usado para enviar uma imagem para um repositório Docker Registry, como o Docker Hub.

    sh

    docker push <nome-do-repositorio>/<nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker push meu-repositorio/minha-imagem:1.0

7. **Fazer Pull de Imagens (docker pull)**

O comando **docker pull** é usado para baixar uma imagem de um repositório Docker Registry.

    sh

    docker pull <nome-do-repositorio>/<nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker pull ubuntu:20.04

8. **Executar um Contêiner (docker run)**

O comando **docker run** é usado para criar e iniciar um contêiner a partir de uma imagem.

    sh

    docker run -d --name <nome-do-container> <nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker run -d --name meu-container ubuntu:20.04

9. **Salvar uma Imagem em um Arquivo (docker save)**

O comando **docker save** salva uma imagem em um arquivo tar, que pode ser transferido ou armazenado.

    sh

    docker save -o <arquivo.tar> <nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker save -o minha-imagem.tar minha-imagem:latest

10. **Carregar uma Imagem de um Arquivo (docker load)**

O comando **docker load** carrega uma imagem a partir de um arquivo tar.

    sh

    docker load -i <arquivo.tar>

    Exemplo:

    sh

    docker load -i minha-imagem.tar

11. **Exibir Histórico de uma Imagem (docker history)**

O comando **docker history** exibe o histórico de camadas de uma imagem.

    sh

    docker history <nome-da-imagem>:<tag>

    Exemplo:

    sh

    docker history ubuntu:20.04

12. **Mostrar Diferenças de uma Imagem (docker diff)**

O comando **docker diff** mostra as alterações feitas em um contêiner em relação à sua imagem de base.

    sh

    docker diff <container_id>

13. **Verificar Camadas de uma Imagem (docker image ls)**

O comando **docker image ls** lista todas as camadas de uma imagem.

    sh

    docker image ls

# Conclusão

Estes são alguns dos comandos mais utilizados para gerenciar imagens Docker. Eles permitem construir, manipular, compartilhar e inspecionar imagens, facilitando o fluxo de trabalho de desenvolvimento e implantação com Docker. A prática com esses comandos ajudará a entender melhor como as imagens Docker funcionam e como integrá-las eficientemente em seus processos.

docker commit

docker build

docker image rm

docker container rm -f $(docker container ls -qa)

docker image ls

docker image prune