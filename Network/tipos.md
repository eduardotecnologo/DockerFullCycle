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