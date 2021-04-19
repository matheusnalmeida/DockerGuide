# Volumes

## Conceito

- Os volumes nada mais são que uma pasta criada com dados que irá ficar armazenada no docker host(aplicação que é responsavel por hostear os containers, sendo geralmente a docker engine). Com os volumes, conseguimos criar novos containers e deletar containers sem perder os dados, pois os mesmos estarão salvos no volume, sendo que o container somente irá apontar para os mesmos. 

## Listagem

### Execução e Criação

- #### **docker -v "endereco" run "imagem"** : Ira criar um container com uma pasta no endereco especificado(neste caso "endereco"), em que todos os dados salvos nesta pasta, na verdade estarão sendo salvos em uma pasta externa no computador(Podemos verificar a pasta ao executar o comando docker inspect e verificarmos a sessão mount).
![doccker_inspect_mount](../images/doccker_inspect_mount.png)

- #### **docker -v "C:\Users\Desktop:var/wwww" run "imagem"** : Ira criar um container com uma pasta no endereco especificado(neste caso "var/wwww"), em que todos os dados salvos nesta pasta, na verdade estarão sendo salvos em uma pasta externa no computador(neste caso "C:\Users\Desktop").