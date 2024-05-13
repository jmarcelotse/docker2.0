**Banco de Dados Postgresql**

Você está dando os primeiros passos no uso de containers. E a melhor forma de iniciar no mundo de containers é usar em ambiente de desenvolvimento.

Sua missão é ajudar a equipe de desenvolvimento a ter mais autonomia no desenvolvimento de projetos. E uma das reclamações da equipe é o setup local.

Crie um comando para criar um banco de dados PostgreSQL no ambiente do desenvolvedor de uma forma que cumpra os seguintes requisitos:

1 - O nome do banco de dados deve ser postgresdb

2 - O usuário de acesso ao banco deve ser dockertuser

3 - A senha do usuário deve ser postgrespwd

Lembrando que a execução em container deve ser transparente pra quem está desenvolvendo. E que aqui você não precisa se preocupar com a perda dos dados do banco e nem nada disso, é apenas para desenvolvimento pontual.

Coloque aqui embaixo o comando que a equipe deve usar pra criar um banco de dados PostgreSQL com esses requisitos.

**Environment Variables**

https://hub.docker.com/_/postgres

POSTGRES_DB

POSTGRES_USER

POSTGRES_PASSWORD

**docker container run -d -p 5432:5432 -e POSTGRES_DB=postgresdb -e POSTGRES_USER=dockertuser -e POSTGRES_PASSWORD="postgrespwd" postgres**

O comando docker container run -d -p 5432:5432 -e POSTGRES_DB=postgresdb -e POSTGRES_USER=dockertuser -e POSTGRES_PASSWORD="postgrespwd" postgres faz o seguinte:

1 - docker container run: Instrui o Docker a criar e executar um novo contêiner.

2 - -d: Indica ao Docker para executar o contêiner em segundo plano (detach), ou seja, sem bloquear o terminal.

3 - -p 5432:5432: Mapeia a porta 5432 do host para a porta 5432 do contêiner. Isso permite acessar o PostgreSQL no contêiner a partir do host usando a porta padrão do PostgreSQL.

4 - -e POSTGRES_DB=postgresdb: Define uma variável de ambiente chamada POSTGRES_DB com o valor "postgresdb". Esta variável é usada para criar um novo banco de dados chamado "postgresdb" durante a inicialização do PostgreSQL.

5 - -e POSTGRES_USER=dockertuser: Define uma variável de ambiente chamada POSTGRES_USER com o valor "dockertuser". Esta variável é usada para criar um novo usuário chamado "dockertuser" no PostgreSQL.

6 - -e POSTGRES_PASSWORD="postgrespwd": Define uma variável de ambiente chamada POSTGRES_PASSWORD com o valor "postgrespwd". Esta variável é usada para definir a senha do usuário "dockertuser" no PostgreSQL.

7 - postgres: Este é o nome da imagem usada para criar o contêiner. No caso deste comando, está usando a imagem do PostgreSQL, que é uma das imagens oficiais do Docker para o PostgreSQL.

Resumidamente, este comando cria e executa um contêiner PostgreSQL com configurações específicas, incluindo a definição de um banco de dados, a criação de um novo usuário e a definição da senha desse usuário. Isso permite que você tenha um ambiente PostgreSQL pronto para uso, com as configurações específicas fornecidas pelas variáveis de ambiente.