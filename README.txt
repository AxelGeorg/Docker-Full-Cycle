Situação de teste 1:
Nginx proxy reverso do laravel, rodar esses comandos ou utilizar docker-compose.laravel.yaml.

- Estando na pasta /laravel/ gerar imagem:
docker build -t axelgeorg/laravel -f Dockerfile.prod .

- Estando na pasta /nginx/ gerar imagem:
docker build -t axelgeorg/nginx -f Dockerfile.prod .

- Criar network:
docker network create --driver bridge laranet

- Rodar os containers:
docker run -d --name laravel --network laranet axelgeorg/laravel:prod 
docker run -d --name nginx --network laranet -p 8080:80 axelgeorg/nginx:prod 

Abra seu navegador no http://localhost:8080/




Situação de teste 2:
Para rodar o docker-compose=


- Colocar os containers para rodar(node e mysql):
docker-compose up -d --build

- Entrar no app node e rodar o front:
docker exec -it app bash
node index.js 

- Entrar na tela front:
http://localhost:3000/

- Entrar no app db para verificar se foi gravado no bando de dados conforme index.js:
docker exec -it db bash

mysql -uroot -p
Enter password: root

use nodedb;

select * from people;
