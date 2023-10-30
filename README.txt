Para gerar imagens, network e rodar os containers=


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