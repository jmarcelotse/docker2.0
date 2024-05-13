**Banco de Dados MongoDB**

Pra finalizar essa etapa, crie o comando pra criar o banco de dados MongoDB usando os requisitos abaixo:

1 - O usuário root do banco deve ser mongo_usr

2 - A senha do usuário root deve ser mongo_pwd

Lembrando que a execução em container deve ser transparente pra quem está desenvolvendo. E que aqui você não precisa se preocupar com a perda dos dados do banco e nem nada disso, é apenas para desenvolvimento pontual.

Coloque aqui embaixo o comando que a equipe deve usar pra criar um banco de dados MongoDB com esses requisitos:

**Environment Variables**

https://hub.docker.com/_/mongo

MONGO_INITDB_ROOT_USERNAME

MONGO_INITDB_ROOT_PASSWORD

**docker container run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongo_usr -e MONGO_INITDB_ROOT_PASSWORD=mongo_pwd mongo**

O comando docker container run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongo_usr -e MONGO_INITDB_ROOT_PASSWORD=mongo_pwd mongo realiza o seguinte:

1 - docker container run: Instrui o Docker a criar e executar um novo contêiner.

2- -d: Indica ao Docker para executar o contêiner em segundo plano (detach), ou seja, sem bloquear o terminal.

3 - -p 27017:27017: Mapeia a porta 27017 do host para a porta 27017 do contêiner. Isso permite acessar o MongoDB no contêiner a partir do host usando a porta padrão do MongoDB.

4 - -e MONGO_INITDB_ROOT_USERNAME=mongo_usr: Define uma variável de ambiente chamada MONGO_INITDB_ROOT_USERNAME com o valor "mongo_usr". Esta variável é usada para definir o nome de usuário root do MongoDB durante a inicialização.

5 - -e MONGO_INITDB_ROOT_PASSWORD=mongo_pwd: Define uma variável de ambiente chamada MONGO_INITDB_ROOT_PASSWORD com o valor "mongo_pwd". Esta variável é usada para definir a senha do usuário root do MongoDB durante a inicialização.

6 - mongo: Este é o nome da imagem usada para criar o contêiner. No caso deste comando, está usando a imagem oficial do MongoDB.

Resumidamente, este comando cria e executa um contêiner MongoDB com configurações específicas, incluindo a definição do nome de usuário e da senha do usuário root do MongoDB. Isso permite que você tenha um ambiente MongoDB pronto para uso, com as configurações específicas fornecidas pelas variáveis de ambiente.