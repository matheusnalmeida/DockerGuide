# Docker Compose

## Conceitos

- O docker compose é uma tecnologia do docker que atua como um orquestrador de containers, facilitando o processo para que possamos subir uma aplicação que necessite de multiplo containers. Com o docker compose podemos subir diversas aplicações com diversas configurações diferentes, que irão evitar com que sejam esquecidos alguns comandos ou que sejam executados os containers na ordem incorreta por exemplo.

- O docker compose utiliza para sua execução um arquivo no formato **.yml** semelhante a um json. Nesse arquivo estarão todas as intruções necessárias para que possamos subir os containers da aplicação com as configurações necessárias.

## Tags DockerCompose

- ### Os comandos do docker compose são interpretados por identação, ou seja, tudo que estiver identado em um dado comando, pertecenrá a um grupo com menor identação. Abaixo seguem os comandos:
<br>

- #### **version: [numero_versao]**: Ira especificar o número da versão do docker compose.

- #### **services:** : Ira identificar os serviços da aplicação. Geralmente cada container irá representar um serviço da aplicação. A idéia é que todos os serviços estarão dentro dessa tag atráves da identação. Abaixo na seção de exemplos, temos um exemplo de aplicação com 5 serviços.

- #### **build:**: Ira definir o caminho para arquivo dockerfile(flag **dockerfile**) e o contexto(flag **context**) para que sejam criada uma imagem a partir de um dockerfile e executada em um determinado serviço.

- #### **networks**: Ira definir as redes personalizadas a serem criadas. Essas redes irão possuir por padrão o nome e o driver, este especificado atráves do comando **driver:**. As redes podem ser atribuidas para os serviços atráves da flag **networks:** dentro de cada serviço.

- #### **ports**: Ira definir as portas para um determinado serviço.

- #### **depends_on:**: Ira definir quais serviços que um determinado serviço necessita para que seja iniciado. A idéia principal dessa flag é que podemos definir uma ordem para subir os serviços.

## Comandos

- #### **docker-compose build**: Ira buildar as imagens especificadas no arquivo "docker-compose". Somente serão buildadas as imagens que possuirem um dockerfile especificado no docker-compose.

- #### **docker-compose up**: Ira executar todas as configurações especificadas no docker compose, executando os serviços e aplicando as configurações de rede entre outras.

- #### **docker-compose up -d**: Ira subir os serviços sem mostrar os logs.

- #### **docker-compose ps**: Ira listar os serviços em execução por parte do docker compose.

- #### **docker-compose down**: Ira para a execução do serviços em execução por parte do docker compose e irá remove-los após finalizar a execução.

- #### **docker-compose restart**: Ira para a execução e executar novamente os serviços.

### Exemplo

- Abaixo segue um exemplo de arquivo docker compose, que é responsavel por sublir uma aplicação com 5 container(total de 5 serviços). Um serviço para o banco de dados em mongo, outros três para os servidores em node e mais um com o nginx, servindo como load balance para as aplicações.

 ```yml
version: '3'
services:
    nginx:
        build:
            dockerfile: ./docker/nginx.dockerfile
            context: .
        image: matheus/nginx
        container_name: nginx
        ports:
            - "80:80"
        networks: 
            - production-network
        depends_on: 
            - "node1"
            - "node2"
            - "node3"

    mongodb:
        image: mongo
        networks: 
            - production-network

    node1:
        build:
            dockerfile: ./docker/my_node_server.dockerfile
            context: .
        image: matheus/my_node_server
        container_name: my_node_server-1
        ports:
            - "3000"
        networks: 
            - production-network
        depends_on:
            - "mongodb"

    node2:
        build:
            dockerfile: ./docker/my_node_server.dockerfile
            context: .
        image: matheus/my_node_server
        container_name: my_node_server-2
        ports:
            - "3000"
        networks: 
            - production-network
        depends_on:
            - "mongodb"

    node3:
        build:
            dockerfile: ./docker/my_node_server.dockerfile
            context: .
        image: matheus/my_node_server
        container_name: my_node_server-3
        ports:
            - "3000"
        networks: 
            - production-network
        depends_on:
            - "mongodb"

networks: 
    production-network:
        driver: bridge
 ```