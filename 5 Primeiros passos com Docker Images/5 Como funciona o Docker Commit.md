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
