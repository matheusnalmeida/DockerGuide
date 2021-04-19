# Imagens

## Conceito

- O container é a representação concreta de uma image. Ele será responsável por *hostear* uma determinada aplicação para que possamos utilizala. Nele irão ficar definidas as configurações, dependencias, entre outros dados necessários para a correta execução da aplicação. Outro interessante ponto é que como as imagens são ditas *read-only*, para que possamos gravar arquivos e alterar dados nos containers, no momento da criação do container é gerada uma camada fina de *read-write*, possibilitando que sejam gravados e salvos novos dados.

## Comandos

### Listagem

- #### **docker images** : Lista todas as imagens

### Execução e Criação

- As imagens podem ser baixadas manualmente na docker store ou ao executar o comando docker run, em que nesse caso serão puxadas automaticamente caso não existam na maquina host. 

### Remoção

- #### **docker rmi "nome-imagem"**: Ira remover a imagem com o nome especificado

- #### **docker images prune**: Ira remover todas as imagens que não estão sendo utilizadas. 