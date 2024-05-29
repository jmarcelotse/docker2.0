    docker container run -it -p 8080:8080 ubuntu /bin/bash

1 - Dentro da imagem instalar o nodejs

    apt update

    apt upgrade

    apt install curl

    curl -fsSL https://deb.nodesource.com/setup_current.x |  bash

    apt install -y nodejs

    node -v

    npm -v

 2 - Fazer a copia do diretorio do sistema e jogas na imagem docker

 de: /home/marcelotse/tse/docker2.0/4 Executando a sua primeira aplicacao em containers/conversao-temperatura/src
 para:/app

    docker container cp . 058de600c6bd:/app

    cd /app

    npm install

     node server.js

3 - Criar a imagem

    docker commit 058de600c6bd conversao-temperatura

    docker image ls

4 - Testar

    docker container ls -a

    docker container rm 058de600c6bd

    docker container run -it -p 8080:8080 conversao-temperatura /bin/bash

    docker container run -d -p 8080:8080 conversao-temperatura node /app/server.js

    docker container ls
