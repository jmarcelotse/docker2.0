# WORKDIR

A instrução **WORKDIR** em um Dockerfile define o diretório de trabalho para qualquer instrução **RUN**, **CMD**, **ENTRYPOINT**, **COPY**, e **ADD** subsequentes. Simplificando, **WORKDIR** estabelece um diretório padrão dentro do contêiner onde comandos e operações serão executados.

1. Como o **WORKDIR** Funciona

    1. **Estabelece um Contexto de Diretório**:
        - Quando você define um diretório de trabalho usando **WORKDIR**, qualquer instrução que segue esse comando será executada a partir desse diretório.

        - Se o diretório especificado não existir, o Docker o criará automaticamente.