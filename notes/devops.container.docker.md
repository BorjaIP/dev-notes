---
id: gul7kdqpha5yep9wzvnmsrn
title: Docker
desc: ''
updated: 1655318118134
created: 1655318081175
---

- [Docker](#docker)
  - [Instalation](#instalation)
  - [Apps](#apps)
  - [Configuration](#configuration)
  - [Commands](#commands)
    - [Stop all containers](#stop-all-containers)
    - [Show process machine](#show-process-machine)
    - [Show volume information](#show-volume-information)
    - [Logging](#logging)
    - [System](#system)
    - [Stats](#stats)
    - [Delete](#delete)
      - [Delete all](#delete-all)
      - [Delete unused or dangling](#delete-unused-or-dangling)
      - [Delete unused containers](#delete-unused-containers)
      - [Delete build cache](#delete-build-cache)
      - [Delete images dangling](#delete-images-dangling)
  - [Docker networking](#docker-networking)
  - [Docker logging](#docker-logging)
  - [Docker Inspect](#docker-inspect)
  - [Docker Registry](#docker-registry)
- [Docker Compose](#docker-compose)
- [Docker Swarm](#docker-swarm)

## Instalation

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
## Apps

- [Lazydocker](https://github.com/jesseduffield/lazydocker)
- [Dive](https://github.com/wagoodman/dive)

## Configuration

```bash
# modify for builtkit
vim /etc/docker/daemon.json

{
    "features": {"buildkit": true}
}
# for docker-compose add
export COMPOSE_DOCKER_CLI_BUILD=1
# Show docker configuration for Registries
cat $HOME/.docker/config.json
# SYSTEMD
systemctl daemon-reload
systemctl restart docker
systemctl show docker --property Environment
```

## Commands

### Run

```bash
docker run -it --entrypoint /bin/bash image:latest
```

### Stop all containers

```bash
docker stop $(docker ps -q)
```

### Show process machine

```bash
docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged ubuntu top

docker exec -it CONTAINER_ID bash top
```

### Show volume information

```bash
docker run -it --rm -v /path/on/host:/vol busybox ls -l /vol
```

### Logging

```bash
docker logs ID
```

### System 

```bash
# Show information about space used for Docker
docker system df
```

### Stats

```bash
docker stats
```

---

### Delete

#### Delete all

```bash
docker system prune -a
```

#### Delete unused or dangling

> Images, Containers, Volumes, and Networks

```bash
docker system prune
docker volume prune
```

#### Delete unused containers

```bash
docker rm $(docker ps -aq)
```

#### Delete build cache

```bash
docker builder prune
```

#### Delete images dangling

```bash
docker rmi $(docker images -qf "dangling=true")
docker rmi $(docker images | grep "<none>" | awk '{print $3}')

# remove last 5 images
docker rm $(docker images -q | tail -n 5)
```
---

## Docker networking

```bash
# Attach a running container to a network
docker network connect [network] [container]
```

---

## Docker logging

```bash
docker logs ID_CONTAINER -f
```

---

## Docker Inspect

```bash
# show IP Docker
docker inspect -f '{{.NetworkSettings.IPAddress}}' ID or Name
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ID or Name
# list all containers belonging to a network by name
docker inspect -f '{{range $key, $value := .NetworkSettings.Networks}}{{$key}} {{end}}' ID or Name
#show volumes
docker inspect -f '{{json .Mounts}}' ID | jq .
```

---

## Docker Registry

Add docker **Registry** [insecure](https://docs.docker.com/registry/insecure/)

Create registry

```bash
docker run -d -p 5000:5000 --name registry registry:2
docker image tag ubuntu localhost:5000/myfirstimage
docker push localhost:5000/myfirstimage
```

Push image to Docker Registry

```bash
docker login -u <user> -p <pass> https://url
docker tag image:latest url/image:latest
docker push url/image:latest
```

---

# Docker Compose

Build with and env file

```bash
docker-compose build --build-args $(cat envfile)
```

# Docker Swarm

```bash
# docker nodes 
docker node ps
docker node ls

# docker services
docker service ls
docker service ps promesa_nifi
docker service logs 

# docker stack
docker stack ls
docker stack ps promesa
docker stack services promesa
docker stack rm down promesa
docker stack deploy -c docker-stack.yml promesa

# remove all services in docker swarm
docker service rm $(docker service ls -q)
```

