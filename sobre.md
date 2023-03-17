## Entendendo tipos de Networks
docker - bridge - host - overlay - maclan - none 

## Trabalhando com Bridge
❯ docker network
Usage:  docker network COMMAND

-- Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.

❯ sudo docker run -d -it --name ubuntu1 bash
❯ sudo docker run -d -it --name ubuntu2 bash
❯ sudo docker network inspect bridge
❯ sudo docker attach ubuntu1
bash-5.2# ip addr show
bash-5.2# ping

## Create Network
❯ docker network create --driver bridge mynetwork
❯ sudo docker network ls
❯ sudo docker run -dit --name ubuntu1 --network mynetwork bash
❯ sudo docker run -dit --name ubuntu2 --network mynetwork bash
❯ sudo docker run -dit --name ubuntu3 bash

❯ sudo docker exec -it ubuntu1 bash
bash-5.2# ping ubuntu2

## Connecr network external
❯ docker network connect mynetwork ubuntu3

## Instalando framework em um container
❯ docker run -it --name php php:7.4-cli bash

## Criando a partir da nossa imagem com Dockerfile
❯ docker build -t eduardodeveloper/laravel:latest . 
❯ docker run --rm --name laravel -p 8000:8000 eduardodeveloper/laravel

## Substituindo o CMD
❯ docker run --rm --name laravel -p 8000:8000 eduardodeveloper/laravel --host=0.0.0.0 --port=8001

## Login Docker Hub
❯ docker login -u "username" -p "password" docker.io
## Docker Hub
❯ docker push eduardodeveloper/laravel

## Node Image
❯ docker run --rm -it -v $(pwd):/usr/src/app -p 3000:3000 node:15 bash
❯ npm init -y
❯ npm install express --save

## Criando a partir da nossa imagem com Dockerfile
❯ docker build -t eduardodeveloper/hello-express .
❯ docker run -p 3000:3000 eduardodeveloper/hello-express:latest                ─╯
App rodando na porta: 3000

## Build Prod
❯ docker build -t eduardodeveloper/hello-express . -f Dockerfile.prod

## Multstage Build | Otimização
❯ docker build -t eduardodeveloper/laravel:prod . -f Dockerfile.prod
❯ docker images | grep laravel

## Nginx como proxy reverso
❯ docker network list
❯ docker network create laranet
❯ docker run -d --network laranet --name laravel eduardodeveloper/laravel:prod
❯ docker run -d --network laranet --name nginx -p 8080:80 eduardodeveloper/nginx:prod

## Up
❯ docker build -t eduardodeveloper/nginx:prod . -f Dockerfile.prod 
❯ docker build -t eduardodeveloper/laravel:prod . -f Dockerfile.prod 
❯ docker run -d --network laranet --name laravel eduardodeveloper/laravel:prod
❯ docker run -d --network laranet --name nginx -p 8080:80 eduardodeveloper/nginx:prod

## Remove all container

❯ docker rm $(docker ps -a -q) -f                                             ─╯
d2495852b505
ade74e8c034e
ea6409a11239
e4aa463b8841
793e3ff5ac6b
b2f64352eb96