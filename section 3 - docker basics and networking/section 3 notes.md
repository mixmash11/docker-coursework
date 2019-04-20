# Section 3 Notes

## basic docker commands

- check docker version
  - docker version
- check docker status
  - docker info
- list all running docker containers
  - docker container ls -a
- start a docker container
  - docker container run -d --name a_container -p 80:80 nginx
- stop a docker container
  - docker container stop a_container
- remove a docker container
  - docker container rm a_container
- force stop/remove docker container
  - docker container rm -f a_container
- process list for a container
  - docker container top a_container
- details of one container configuration
  - docker container inspect a_container
- performance stats for all containers
  - docker container stats
- view logs for a container
  - docker container logs a_container

## get a shell into a container

- start a new container interactively
  - docker container run -it nginx bash
    - will run until you exit, will be stopped (but saved)
    - bash is a command (specifying which shell to open)
- start a new container that removes upon exit
  - docker container run -it --rm nginx bash
- execute command in existing container
  - docker container exec -it a_container bash

## docker network concepts

- check container port
  - docker container port a_container
- view container ip address
  - docker container inspect --format '{{ .NetworkSettings.IPAddress }}' a_container
- defaults:
  - container connected to a private virtual network "bridge"
  - virtual networks route through nat firewall on the host (and host ip)
  - all containers in a single virtual network can talk to each other
  - __best practice:__ each app has its own virtual network
  - you can:
    - attach containers to more or no virtual networks
    - skip virtual networks and use host IP
      - consideration for high-network traffic, performance related issues
    - add custom network drivers
- publish (-p) (manually expose a port)
  - {in}:{route-to}
    - exampe: 8080:80
      - route traffic from port 8080 on localhost
      - send to virtual network port 80
- nginx with ping option:
  - current nginx doesn't have ping command anymore
  - old version can be run with image name nginx:alpine
- there is a none network (not attached to anything)
- a new network gets a bridge network driver by default (simple driver)
- all externally exposed ports closed by default
- link container to other container
  - ddocker container run -d --name a_container --link another_container nginx

## managing virtual networks

- show virtual networks
  - docker network ls
- inspect a network
  - docker network inspect a_network
- create a network
  - docker network create --driver a_network
- attach a network to container
  - docker network connect a_network a_container
- detach network from container
  - docker network disconnect a_network a_container
- create a new container connected to a specific virtual network
  - docker container run --name a_container -p 80:80 -d --network a_network 

## docker network dns

- __best practice:__ don't use IP addresses
- docker uses container names as host names (DNS)
- multiple containers on a created network can respond to the same dns address
