# Containers

## Conceito

- As imagens são um template de criação dos containers. Ela irão conter instruções de como criar o container e executar as aplicações nos containers da maneira correta. É importante citar que as imagens funcionam como um template somente de leitura(read only), não podendo ser alteradas.

## Comandos

### Listagem

- #### **docker ps** : Lista todos os conteiners ativos

- #### **docker ps -a** : Lista todos os containers

- #### **docker port "id-container"** : Lista as portas que estão em uso pelo container

- #### **docker-machine ip"** : Caso o docker esteja sendo executado em uma maquina virtual, irá retornar o ip da maquina onde está sendo executado.

- #### **docker ps -q** : Lista somente os ids dos containers.

- #### **docker inspect "id-container": Irá trazer informações a respeito do container especificado. Uma delas é a "Mount", em que podemos verificar a pasta do container que esta mapeada para uma pasta do host.

### Execução e Criação

- #### **docker run "nome-imagem"**: Ira baixar a imagem especificada(caso ainda não esteja baixada) do dockerhub com o dockerdaemon e irá criar um conteiner executando a imagem

- #### **docker run "nome-imagem" "comando"** : Ira criar e executar o container coma imagem especificada e executar nessa imagem o comando passado

- #### **docker run -it "nome-imagem"**: Ira executar o conteiner atrelando o contexto(terminal nesse caso) de forma iterativa com o terminal do conteiner, trocando o terminal para poder utilizar o terminal do container

- #### **docker run -d "nome-imagem"**: Ira executar o conteiner de forma detached, ou seja, o processo que for executar não irá estar atrelado ao terminal e não irá travalo.

- #### **docker run -P "nome-imagem"**: Ira executar o conteiner mapeando uma porta aleatoria da maquina hospedeira para uma porta do conteiner, permitindo assim o acesso ao conteiner.

- #### **docker run --name "nome-conteiner" "nome-imagem"**: Ira atribuir um nome especifico para o conteiner e executalo.

- #### **docker run -p  "porta1:porta2" "nome-imagem"**: Ira executar o conteiner mapeando a **porta1** da maquina hospedeira para a **porta2** do conteiner, permitindo assim o acesso ao conteiner atraves da porta especificada.

- #### **docker run -e  NOMEVARIAVEL="VALOR-VARIAVEL" "nome-imagem"**: Ira executar o conteiner criando dentro do mesmo uma variavel de ambiente com o nome e valor especificado.
 
- #### **docker run -w  "endereco1" "nome-imagem"**: Ira executar o conteiner e ja iniciar no endereco informado no momento da criação(neste caso "endereco1").
  
### Início e Parada

- #### **docker start "id-conteiner"**: Ira iniciar um conteiner existente

- #### **docker start -a -i "id-conteiner"**: Ira executar o container existente de forma iterativa

- #### **docker stop "id-conteiner"**: Ira para a execução do conteiner

- #### **docker stop -t "tempo" "id-conteiner"**: Ira parar a execução do conteiner de acordo com o tempo passado como parametro. Se não for passado o parametro, o tempo default será 10 segundos.

- #### **docker stop "$(docker ps -q)"**: Ira para a execução de todos os container retornados pelo comando **docker ps -q**(Comando explicado na primeira seção.).

### Remoção

- #### **docker rm "id-conteiner | nome-conteiner"**: Ira remover o container especificado de acordo com o id ou nome especificado.

- #### **docker container prune**: Ira remover todos os containers inativos. 

### Observações:

- Uma imagem não oficial possui uma nomenclatura diferente das oficiais. Par executar um container com uma imagem não oficial, pode ser executado o comando utilizando a nomenclatura **docker run "nome-criador/nome-imagem"**.