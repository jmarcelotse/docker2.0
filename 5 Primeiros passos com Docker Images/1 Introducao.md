**Docker images**

As "Docker images" são os blocos de construção fundamentais para a criação de contêineres Docker. Elas contêm um sistema de arquivos com tudo o que é necessário para executar uma aplicação, incluindo o código, as bibliotecas, as dependências, as variáveis de ambiente e as configurações. Em termos simples, uma imagem Docker é uma versão executável de um aplicativo, pronta para ser implantada em um contêiner.

Aqui estão alguns pontos-chave sobre as imagens Docker:

1 - Base para os Contêineres: As imagens Docker servem como base para a criação de contêineres. Quando você executa um contêiner a partir de uma imagem, o Docker cria uma instância desse contêiner, que é uma execução isolada e independente da aplicação contida na imagem.

2 - Compartilháveis e Reutilizáveis: As imagens Docker são projetadas para serem compartilháveis e reutilizáveis. Elas podem ser distribuídas e compartilhadas através de repositórios de imagens, como o Docker Hub, permitindo que desenvolvedores, equipes e comunidades compartilhem e colaborem no desenvolvimento de aplicativos.

3 - Imutáveis e Reprodutíveis: As imagens Docker são imutáveis, o que significa que uma vez criadas, elas não podem ser alteradas. Isso garante consistência e previsibilidade, pois você sempre terá a mesma imagem, independentemente do ambiente em que ela é implantada.

4 - Camadas de Construção: As imagens Docker são construídas em camadas. Cada instrução em um Dockerfile (o arquivo de configuração usado para construir imagens Docker) adiciona uma nova camada à imagem. Isso permite a reutilização eficiente de camadas comuns entre diferentes imagens e facilita a atualização e a manutenção das imagens.

5 - Eficientes em Termos de Espaço: O Docker usa um sistema de armazenamento de camadas para gerenciar imagens, o que significa que as imagens compartilham camadas comuns quando possível. Isso torna o armazenamento e o compartilhamento de imagens mais eficientes em termos de espaço.

Em resumo, as imagens Docker são a base para a criação e execução de contêineres, fornecendo uma maneira consistente e reprodutível de empacotar, distribuir e implantar aplicativos em ambientes Docker.