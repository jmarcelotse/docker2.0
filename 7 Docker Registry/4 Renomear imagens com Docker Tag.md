# Renomear imagens com Docker Tag

Renomear uma imagem Docker essencialmente envolve criar uma nova tag para a imagem existente. O comando **docker tag** é usado para isso. Vamos detalhar os passos necessários para renomear uma imagem Docker.

# Passo a Passo para Renomear uma Imagem Docker

**Passo 1: Listar Imagens Docker**

Primeiro, verifique as imagens Docker existentes no seu sistema:

    sh

    docker images

Isso exibirá uma lista de imagens com as colunas **REPOSITORY**, **TAG**, **IMAGE ID**, **CREATED**, e **SIZE**.

**Passo 2: Identificar a Imagem a Ser Renomeada**

Anote o **IMAGE ID** da imagem que você deseja renomear. Suponha que o **IMAGE ID** seja **abc123**.

**Passo 3: Taguear a Imagem com o Novo Nome**

Use o comando **docker tag** para renomear a imagem. A estrutura básica do comando é:

    sh

    docker tag IMAGE_ID NOVO_REPOSITORIO:NOVA_TAG

Exemplo:

Se você deseja renomear a imagem **abc123** para **meuusuario/novorepo:v2**, o comando seria:

    sh

    docker tag abc123 meuusuario/novorepo:v2

**Passo 4: Verificar a Nova Tag**

Após a execução do comando **docker tag**, liste novamente as imagens Docker para confirmar que a nova tag foi criada corretamente:

    sh

    docker images

Você deve ver a nova imagem **meuusuario/novorepo** com a tag **v2** na lista.

**Passo 5: (Opcional) Remover a Tag Antiga**

Se você não precisar mais da tag antiga, pode removê-la usando o comando **docker rmi**:

    sh

    docker rmi REPOSITORIO:TAG_ANTIGA

Exemplo:

Se a tag antiga era **meuusuario/antigarepo:v1**, o comando seria:

    sh

    docker rmi meuusuario/antigarepo:v1

# Exemplo Completo

Vamos passar por um exemplo completo, renomeando uma imagem Docker:

1. **Listar Imagens Existentes**:

    sh

    docker images

Saída:

    bash

    REPOSITORY            TAG      IMAGE ID       CREATED         SIZE
    meuusuario/antigarepo v1       abc123         2 days ago      128MB

2. **Taguear a Imagem com o Novo Nome**:

    sh

    docker tag abc123 meuusuario/novorepo:v2

3. **Verificar a Nova Tag**:

    sh

    docker images

Saída:

    bash

    REPOSITORY            TAG      IMAGE ID       CREATED         SIZE
    meuusuario/antigarepo v1       abc123         2 days ago      128MB
    meuusuario/novorepo   v2       abc123         2 days ago      128MB

4. **Remover a Tag Antiga (Opcional)**:

    sh

    docker rmi meuusuario/antigarepo:v1

5. **Verificar a Remoção da Tag Antiga**:

    sh

    docker images

Saída:

    bash

    REPOSITORY            TAG      IMAGE ID       CREATED         SIZE
    meuusuario/novorepo   v2       abc123         2 days ago      128MB

# Conclusão

Renomear uma imagem Docker usando o comando **docker tag** é um processo simples e eficaz. Este comando cria uma nova tag para a imagem existente, permitindo que você gerencie suas imagens de forma mais organizada e intuitiva.

###

1. docker image ls

2. docker tag conversao-temperatura-dockerfile jmarcelotse/conversao-temperatura:v1

3. docker image ls

4. docker tag jmarcelotse/conversao-temperatura:v1 jmarcelotse/conversao-temperatura:latest

5. docker inspect jmarcelotse/conversao-temperatura
