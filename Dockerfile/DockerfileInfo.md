# Dockerfiles

## Conceito

- #### As dockerfiles servem como um conjunto de instruções para que possamos criar nossas proprias imagens, podendo nelas serem especificadas um conjunto de instruções que irão ajudar na construção da imagem.

## Comandos

- #### **docker build -f Dockerfile -t matheus/node [DIRETORIO_DOCKERFILE]**: Ira realizar o build e criar a imagem baseada na DockerFile especificada com o parametro -f. A flag -t será utilizada para definir o nome da imagem. Por padrão, para imagens não oficiais é utilizada a notação **NOME_DO_USUARIO/NOME_DA_IMAGEM**.

## Tags DockerFile

- #### **FROM [IMAGEM]**: Ira epecificar uma imagem a ser utilizada como base para a nova imagem.

- #### **MAINTAINER [NOME]**: Ira especificar o usuario responsavel pela manutenção do dockerfile.

- #### **ENV [NOME_VARIAVEL]=[VALOR_VARIAVEL]**: Ira definir uma variavel de ambiente.

- #### **COPY [ENDERECO_ORIGEM] [ENDERECO_DESTINO]**: Ira copiar os arquivos do endereço de origem para o endereço de destino dentro do container.

- #### **WORKDIR [ENDRECO]**: Ira alterar o endereço atual do container para o endereço especificado.

- #### **RUN [COMANDO]**: Ira executar o comando especificado. O comando pode ser informado diretamento ou entre colchetes, separando cada um em uma string(ex: ["comando1", "comando2"]). 

- #### **ENTRYPOINT [COMANDO]**: Ira executar o comando especificado ao iniciar o container com a imagem.

- #### **EXPOSE [PORTA]**: Ira expor uma porta do container para que possa ser acessada pela maquina hospedeira.

## Exemplo

- #### Abaixo temos um exemplo de comando usado para criar e executar um container node, contendo um conjunto de instruções para executar o projeto.

    **docker run -p 8080:3000 -v "$(pwd):/var/www" -w "/var/www" node npm start**

- #### Para que esse processo se torne automazido na construção de uma imagem do projeto, podemos criar um DockerFile contendo as seguitnes instruções.

 ```dockerfile
FROM node:latest
MAINTAINER Matheus Nunes
ENV PORT=3000
COPY . /var/www
WORKDIR /var/www
RUN npm install
ENTRYPOINT ["npm", "start"]
EXPOSE $PORT
 ```