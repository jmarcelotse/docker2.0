Os contêineres são unidades de software que encapsulam uma aplicação juntamente com todas as suas dependências, como bibliotecas, ferramentas e arquivos de configuração, permitindo que a aplicação seja executada de forma isolada e consistente em diferentes ambientes.

As variáveis de ambiente são valores dinâmicos que podem afetar o comportamento de processos em um sistema operacional ou em uma aplicação. Elas são usadas para passar informações de configuração ou estado para dentro de programas em execução.

Em contextos de contêineres, as variáveis de ambiente desempenham um papel importante. Elas podem ser usadas para configurar o comportamento de aplicações dentro do contêiner de uma forma flexível e reutilizável, independentemente do ambiente em que o contêiner é executado.

Aqui estão alguns casos de uso comuns para variáveis de ambiente em contêineres:

1 - Configuração de aplicação: As variáveis de ambiente podem ser usadas para configurar parâmetros específicos da aplicação, como URLs de banco de dados, chaves de API, configurações de log, etc.

2 - Passagem de segredos: As variáveis de ambiente podem ser usadas para passar informações sensíveis, como senhas ou tokens de autenticação, de forma segura para dentro do contêiner, sem precisar armazená-las diretamente no código-fonte ou em arquivos de configuração.

3 - Customização de ambiente: As variáveis de ambiente podem ser usadas para fornecer opções de configuração flexíveis que permitem adaptar o comportamento da aplicação a diferentes ambientes, como desenvolvimento, teste e produção.

No Docker, as variáveis de ambiente podem ser definidas de várias maneiras:

    No Dockerfile, usando a instrução ENV.

    Ao executar o contêiner, usando a opção -e ou --env.

    Em arquivos de composição do Docker, como o docker-compose.yml, usando a chave environment.

Em resumo, as variáveis de ambiente são uma ferramenta poderosa para configurar e personalizar o comportamento de aplicações em contêineres, permitindo uma maior flexibilidade e portabilidade entre diferentes ambientes de execução.

**docker container run -p 3306 -d mysql**

O comando docker container run -p 3306 -d mysql faz o seguinte:

1 - docker container run: Esta parte do comando instrui o Docker a criar e executar um novo contêiner.

2 - -p 3306: Esta é uma opção que indica ao Docker para mapear a porta do host para a porta do contêiner. No caso deste comando, está mapeando a porta 3306 do host para a porta do contêiner. A porta 3306 é comumente usada para conexões de banco de dados MySQL.

3 - -d: Esta é uma opção que significa "detach". Quando você usa -d, o Docker executa o contêiner em segundo plano, ou seja, ele não mantém o terminal bloqueado após iniciar o contêiner. Isso permite que você continue usando o terminal para outras tarefas.

4 - mysql: Este é o nome da imagem que será usada para criar o contêiner. No caso deste comando, está usando a imagem do MySQL, que é um popular sistema de gerenciamento de banco de dados relacional.

Portanto, quando você executa docker container run -p 3306 -d mysql, o Docker cria e executa um novo contêiner usando a imagem do MySQL, o executa em segundo plano e mapeia a porta 3306 do host para a porta do contêiner. Isso permite que você acesse o servidor MySQL em seu host usando a porta 3306.

**OBS: Dessa forma nao vai funcionar**

Para verificar o funcionamento utilizar o **docker logs d86be2441802**

**docker logs d86be2441802**

Quando você executa o comando docker logs d86be2441802, está solicitando ao Docker para exibir os logs do contêiner identificado pelo ID d86be2441802. Aqui está o que cada parte do comando faz:

1 - docker logs: Esta parte do comando instrui o Docker a exibir os logs de um contêiner específico.

2 - d86be2441802: Este é o ID do contêiner do qual você deseja ver os logs. Cada contêiner Docker é identificado por um ID único.

Portanto, ao executar docker logs d86be2441802, o Docker exibirá os logs que foram gerados pela aplicação em execução dentro do contêiner identificado pelo ID d86be2441802. Isso é útil para monitorar o comportamento da aplicação, diagnosticar problemas e depurar erros que podem ocorrer durante a execução do contêiner.

docker logs d86be2441802

2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.3.0-1.el8 started.

2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'

2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.3.0-1.el8 started.

2024-05-11 13:23:37+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified

    You need to specify one of the following as an environment variable:

    - MYSQL_ROOT_PASSWORD

    - MYSQL_ALLOW_EMPTY_PASSWORD

O comando docker logs d86be2441802 exibiu os registros (logs) gerados pelo contêiner identificado pelo ID d86be2441802. Vamos analisar cada linha dos registros:

1 - 2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.3.0-1.el8 started.: Esta é uma mensagem informativa indicando que o script de ponto de entrada (entrypoint) para o servidor MySQL está sendo iniciado.

2 - 2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql': Esta é outra mensagem informativa indicando que o script de ponto de entrada está mudando para o usuário dedicado "mysql". Isso geralmente é feito por motivos de segurança para executar o serviço com permissões restritas.

3 - 2024-05-11 13:23:36+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.3.0-1.el8 started.: Esta linha é uma repetição da primeira linha. Parece ser uma duplicata no registro.

4 - 2024-05-11 13:23:37+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified: Este é um erro gerado pelo script de ponto de entrada. Ele indica que o banco de dados está não inicializado e que nenhuma opção de senha foi especificada. Em seguida, são fornecidas instruções sobre como resolver o erro, ou seja, especificar uma das seguintes opções como uma variável de ambiente:

    MYSQL_ROOT_PASSWORD

    MYSQL_ALLOW_EMPTY_PASSWORD

    MYSQL_RANDOM_ROOT_PASSWORD

Essas mensagens são úteis para diagnosticar problemas durante a inicialização do contêiner MySQL, indicando que a configuração inicial necessária não foi fornecida.

Para encontrar com funciona as variaveis na imagem deve acessar o **https://hub.docker.com/**

**Environment Variables**

 **docker container run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD="root1234" -e MYSQL_DATABASE=docker_db -e MYSQL_USER=userdocker -e MYSQL_PASSWORD=dockerpwd mysql**

O comando docker container run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD="root1234" -e MYSQL_DATABASE=docker_db -e MYSQL_USER=userdocker -e MYSQL_PASSWORD=dockerpwd mysql realiza o seguinte:

1 - docker container run: Instrui o Docker a criar e executar um novo contêiner.

2 - -d: Indica ao Docker para executar o contêiner em segundo plano (detach), ou seja, sem bloquear o terminal.

3 - -p 3306:3306: Mapeia a porta 3306 do host para a porta 3306 do contêiner. Isso permite acessar o MySQL no contêiner a partir do host usando a porta padrão do MySQL.

4 - -e MYSQL_ROOT_PASSWORD="root1234": Define uma variável de ambiente chamada MYSQL_ROOT_PASSWORD com o valor "root1234". Esta variável é usada para definir a senha do usuário root do MySQL.

5 - -e MYSQL_DATABASE=docker_db: Define uma variável de ambiente chamada MYSQL_DATABASE com o valor "docker_db". Esta variável é usada para criar um novo banco de dados chamado "docker_db" durante a inicialização do MySQL.

6 - -e MYSQL_USER=userdocker: Define uma variável de ambiente chamada MYSQL_USER com o valor "userdocker". Esta variável é usada para criar um novo usuário chamado "userdocker" no MySQL.

7 - -e MYSQL_PASSWORD=dockerpwd: Define uma variável de ambiente chamada MYSQL_PASSWORD com o valor "dockerpwd". Esta variável é usada para definir a senha do usuário "userdocker" no MySQL.

8 - mysql: Este é o nome da imagem usada para criar o contêiner. No caso deste comando, está usando a imagem do MySQL, que é uma das imagens oficiais do Docker para o MySQL.

Resumidamente, este comando cria e executa um contêiner MySQL com configurações específicas, incluindo a definição de uma senha para o usuário root, a criação de um novo banco de dados, e a definição de um novo usuário com sua respectiva senha. Isso permite que você tenha um ambiente MySQL pronto para uso, com as configurações específicas fornecidas pelas variáveis de ambiente.