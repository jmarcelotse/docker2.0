/home/marcelotse/tse/docker2.0/4 Executando a sua primeira aplicacao em containers/conversao-temperatura/src

docker container cp . ed0e1ea2ade2:/app

npm install

node server.js

**Rodando a aplicacao dentro do container.**

Essa nao seria a maneira corretada de trabalhar com docker.

Melhor forma seria com imagem.