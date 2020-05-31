<h1 align="center">
  Criando instancias dos bancos de dados com docker
</h1>

# :bookmark_tabs: Índice

- [Objetivo](#objetivo)
- [Dicionário](#dicionario)
- [Instalação do Docker](#instalação-do-docker)
- [Instalar o Redis](#redis)
- [Instalar o MongoDb](#mongodb)
- [Instalar o Sql Server](#sqlserver)

<a id="objetivo"></a>
## :dart: Objetivo

- Mostrar de maneira simples como experimentar diferentes tecnologias de bancos de dados em qualquer sistema operacional, assim facilitando o seu processo de estudo.

<a id="dicionario"></a>
## :closed_book: Dicionário

- flag <b>--name</b> define o nome da instancia do container.
- flag <b>-p porta:porta</b> define a porta que fora do container que vai ser usada e depois dos dois pontos define a porta dentro do container que vai se conectar com o banco.
- `docker pull nome-imagem:versão` baixa uma imagem de um container.
- `docker exec -it nome-container bash` diz ao docker que nós queremos acesso ao terminal do container.
- `docker ps` Lista os containers que estão rodando no momento.
- `docker ps -a` Lista todas os containers mesmo que eles estejam parados.
- `docker rm nome-container` remove o container não a imagem.
- `docker start nome-container` Inicia um container.
- `docker stop nome-container` Pausa um container.

<a id="instalação-do-docker"></a>
## :key: Instalação do Docker

- Para instalar o docker siga a [Documentação](https://docs.docker.com/get-docker/), ele está disponivel para todas as plataformas windows, mac e linux.

<a id="redis"></a>
## Redis

- Esse banco funciona em cache na memoria para controlar filas de processos como envios de email ou filas de escrita no banco de dados.

- Primeiro vamos baixar a imagem => `docker pull redis:alpine`.
- Agora vamos criar uma instância do banco => `docker run --name redisDb -p 6379:6379 -d -t redis:alpine`.

<a id="mongodb"></a>
## MongoDb

- O mongoDb é um banco não relacional de documentos no padrão <b>JSON</b>, que possui drivers para quase todas as linguagens e o seu gerenciador o <b>mongodb compass</b> está disponível para todos os sistemas operacionais.

- Primeiro vamos baixar a imagem => `docker pull mongo`.
- Agora vamos criar uma instância do banco => `docker run --name mongoDb -p 27017:27017 -d -t mongo`.
- Agora dentro do gerenciador você pode se conectar sem problemas ele não precisa de senha ou usuário.

<a id="sqlserver"></a>
## Sql Server
- O Sql Server é o banco de dados relacional desenvolvido e mantido pela microsoft.

- Primeiro vamos baixar a imagem => `docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04`.
- Agora vamos criar uma instância do banco => `docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=suasenhacomLetraMaiusculaENumeros" -p 1433:1433 --name sql1 -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04`.
- Vamos entrar no bash no container para dar o acesso externo ao banco de dados, com o comando => `sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "suasenhacomLetraMaiusculaENumeros" -Q 'ALTER LOGIN SA WITH PASSWORD="suasenhacomLetraMaiusculaENumeros"'`

- Agora você pode acessar o banco com o usuário <b>SA</b> de system administration com a senha que você definiu.
