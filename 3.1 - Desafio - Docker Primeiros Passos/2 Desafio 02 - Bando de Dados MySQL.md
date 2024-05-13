**Banco de Dados MySQL**

Agora que a equipe tem como criar o banco de dados Postgre, crie o comando pra criar o banco de dados MySQL usando os requisitos abaixo:

1 - O nome do banco de dados deve ser docker_db

2 - O usuário de acesso ao banco deve ser docker_usr

3 - A senha do usuário deve ser docker_pwd

Lembrando que a execução em container deve ser transparente pra quem está desenvolvendo. E que aqui você não precisa se preocupar com a perda dos dados do banco e nem nada disso, é apenas para desenvolvimento pontual.

Coloque aqui embaixo o comando que a equipe deve usar pra criar um banco de dados MySQL com esses requisitos:

 **Environment Variables**

https://hub.docker.com/_/mysql

MYSQL_DATABASE

MYSQL_USER

MYSQL_PASSWORD

MYSQL_ROOT_PASSWORD

**docker container run -d -p 3306:3306 -e MYSQL_DATABASE=docker_db -e MYSQL_USER=docker_usr -e MYSQL_PASSWORD=docker_pwd -e MYSQL_ROOT_PASSWORD="root1234" mysql**

O comando docker container run -d -p 3306:3306 -e MYSQL_DATABASE=docker_db -e MYSQL_USER=docker_usr -e MYSQL_PASSWORD=docker_pwd -e MYSQL_ROOT_PASSWORD="root1234" mysql realiza o seguinte:

1 - docker container run: Instrui o Docker a criar e executar um novo contêiner.

2 - -d: Indica ao Docker para executar o contêiner em segundo plano (detach), ou seja, sem bloquear o terminal.

3 - -p 3306:3306: Mapeia a porta 3306 do host para a porta 3306 do contêiner. Isso permite acessar o MySQL no contêiner a partir do host usando a porta padrão do MySQL.

4 - -e MYSQL_DATABASE=docker_db: Define uma variável de ambiente chamada MYSQL_DATABASE com o valor "docker_db". Esta variável é usada para criar um novo banco de dados chamado "docker_db" durante a inicialização do MySQL.

5 - -e MYSQL_USER=docker_usr: Define uma variável de ambiente chamada MYSQL_USER com o valor "docker_usr". Esta variável é usada para criar um novo usuário chamado "docker_usr" no MySQL.

6 - -e MYSQL_PASSWORD=docker_pwd: Define uma variável de ambiente chamada MYSQL_PASSWORD com o valor "docker_pwd". Esta variável é usada para definir a senha do usuário "docker_usr" no MySQL.

7 - -e MYSQL_ROOT_PASSWORD="root1234": Define uma variável de ambiente chamada MYSQL_ROOT_PASSWORD com o valor "root1234". Esta variável é usada para definir a senha do usuário root do MySQL.

8 - mysql: Este é o nome da imagem usada para criar o contêiner. No caso deste comando, está usando a imagem oficial do MySQL.

Resumidamente, este comando cria e executa um contêiner MySQL com configurações específicas, incluindo a definição de um banco de dados, a criação de um novo usuário, e a definição das senhas tanto do usuário "docker_usr" quanto do usuário root. Isso permite que você tenha um ambiente MySQL pronto para uso, com as configurações específicas fornecidas pelas variáveis de ambiente.
