Para gerar imagens, network e rodar os containers=
Descrição: Imagens laravel e nginx, network bridge e containers de Multistage Building, sendo nginx utilizado como proxy reverso. 
É possível verificar Dockerfile de testes e Dockerfile.prod aonde para ambas as imagens houve otimização. 

Diferença de tamanho das imagens geradas:
- Laravel:
axelgeorg/laravel    prod      66506401d237   About a minute ago   141MB
axelgeorg/laravel    latest    635a627e0e9f   31 minutes ago       555MB
- Nginx:
axelgeorg/nginx      prod      fc5488d4b131   10 hours ago     18MB
axelgeorg/nginx      latest    3c59b3c209bc   18 seconds ago   187MB



Para começar a fazer isso funcionar basta seguir:

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
