# Comunicação entre Containers

## Conceitos

- Muitas das vezes iremos sentir a necessidade de comunicar diferentes containers, isso pois mutias das vezes, cada partes da aplicação estarão em diferentes containers(como por exemplo o banco de dados em um e a aplicação em outro).

- Quando criamos um container com o comando **run**, automaticamente o docker host irá adicionar os containers em uma mesma rede(rede default do docker), facilitando assim a comunicação dos mesmos. Com esta rede default, não podemos atribuir nomenclaturas para os endereços(hostname), sendo necessário sempre o uso do ip especifico de cada container.

## Comandos

### Listagem

- #### **docker inspect [id_container]** : Com este comando podemos verificar o ip da rede em que o container esta situado, atráves da sessão de network.

- #### **docker network ls** : Lista as redes existentes criadas no docker host.

#### Criação

- #### **docker network create --driver bridge "nome_rede"** : Ira criar uma rede personalizada no docker, onde poderão ser adicionados containers para comunicação. O driver mais utilizado é o bridge, mas existem vários tipos.

- #### **docker run [nome_imagem] --network [nome_rede]** : Ira criar um container na rede especificada. Quando os containers são criados em uma rede diferente da default do docker host, é possivel realizar a comunicação entre os containers atraves do nome.

### Observações:

- Uma imagem não oficial possui uma nomenclatura diferente das oficiais. Par executar um container com uma imagem não oficial, pode ser executado o comando utilizando a nomenclatura **docker run "nome-criador/nome-imagem"**.