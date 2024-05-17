 **Docker Commit**

 O comando docker commit é utilizado para criar uma nova imagem Docker a partir das mudanças feitas em um contêiner existente. Aqui está uma explicação detalhada de como ele funciona e como usá-lo:

**Funcionamento do Docker Commit**

1 - Inicialização do Contêiner:

Primeiro, você precisa iniciar um contêiner a partir de uma imagem existente. Isso pode ser feito com o comando docker run. Por exemplo:

    docker run -it ubuntu:latest /bin/bash

O comando acima inicia um contêiner interativo (-it) da imagem ubuntu:latest e abre um shell bash dentro do contêiner.

2 - Modificações no Contêiner:

Dentro do contêiner, você pode fazer as modificações desejadas. Isso pode incluir instalar pacotes, modificar arquivos de configuração, adicionar novos arquivos, etc.

Por exemplo:

    apt-get update

    apt-get install -y nginx

3 - Cometer as Mudanças:

Depois de realizar as mudanças necessárias no contêiner, você pode criar uma nova imagem que inclui essas mudanças usando o comando docker commit.

Primeiro, saia do contêiner ou, em outro terminal, obtenha o ID ou nome do contêiner em execução com:

    docker ps

Depois, use o comando docker commit para criar uma nova imagem:

    docker commit <container_id> nome_da_nova_imagem

Substitua <container_id> pelo ID ou nome do contêiner e nome_da_nova_imagem pelo nome que você deseja dar à nova imagem.

4 - Uso da Nova Imagem:

Agora, você pode usar a nova imagem como qualquer outra imagem Docker. Por exemplo, para iniciar um novo contêiner a partir da imagem recém-criada:

docker run -it nome_da_nova_imagem /bin/bash

**Exemplo Prático**

Vamos seguir um exemplo prático para consolidar o entendimento:

1 - Inicie um Contêiner:

        docker run -it ubuntu:latest /bin/bash

2 - Realize Modificações:

Dentro do contêiner:

    apt-get update

    apt-get install -y curl

3 - Saia do Contêiner:

    exit

4 - Cometa as Mudanças:

Suponha que o ID do contêiner é abcd1234 (você pode obter isso com docker ps)

    docker commit abcd1234 meu_ubuntu_com_curl

5 - Verifique a Nova Imagem:

Liste as imagens Docker disponíveis:

    docker images

Você deverá ver meu_ubuntu_com_curl na lista de imagens.

6 - Use a Nova Imagem:

Inicie um novo contêiner a partir da imagem criada:

    docker run -it meu_ubuntu_com_curl /bin/bash

Verifique se o curl está instalado:

    curl --version

**Considerações Importantes**

**Persistência:** O comando docker commit cria uma nova imagem que persiste no seu sistema Docker local, mas não modifica a imagem base original.

**Camadas:** Docker armazena imagens em camadas. Cada docker commit cria uma nova camada sobre a imagem base.

**Automação:** Embora o docker commit seja útil para criar rapidamente uma imagem a partir de um contêiner em execução, para automação e reprodutibilidade, é preferível usar um Dockerfile.

O **docker commit** é útil para criar imagens rapidamente a partir de um estado atual de um contêiner, mas para ambientes de produção e desenvolvimento contínuo, o uso de Dockerfiles é geralmente mais recomendado.

O comando **docker commit** no Docker é utilizado para criar uma nova imagem a partir de um contêiner existente. Isso é útil quando você fez mudanças em um contêiner em execução e deseja preservar essas mudanças em uma nova imagem. Vamos detalhar como ele funciona e como utilizá-lo.

**O que é o Docker Commit?**

O **docker commit** cria uma imagem Docker nova a partir de um contêiner em execução ou parado, incluindo todas as modificações feitas nesse contêiner, como instalações de pacotes, alterações em arquivos de configuração e outros ajustes.
