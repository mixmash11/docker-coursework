# Section 4 Notes

## images

- an image contains:
  - app binaries and dependencies
  - metadata about the image and how to run the image

## docker hub

- official images don't have a slash (/)

## image layers

- images start as blank layers
- every change is a new layer
- view history of image:
  - docker image history a_container
- view configuration of image:
  - docker image inspect a_container

## image tagging / pushing to docker hub

- images don't have a name
- tags are not quite versions or tags
  - pointer to a specific image commit
- retag an image
  - docker image tag a_container a_docker_user/a_container
- log into docker
  - docker login
- push docker image
  - docker image push a_docker_user/a_container

## docker files

- Order matters
- Each line is a layer
- FROM (required command)
  - usually a linux distro
  - ex: 
    - FROM debian:stretch-slim
- ENV (environment variables)
  - how we set keys and values
  - any other lines will be able to use
  - ex:
    - ENV NGINX_VERSION 1.13.6-1~stretch
- RUN (command)
  - can run commands / shell scripts
  - __Best Pratice:__
    - && - use to combine multiple commands into a single run call
      - ex:
        - && apt-get update \
    - ln - log (__Best Practice:__ to standard out)
      - ex:
        - ln -sf /dev/stdout /var/log/nginx/access.log
- EXPOSE (expose image ports)
  - by default no ports are exposed to the docker virtual network
  - you still need to use -p (publish) to open/forward the ports on the host
- CMD (command to run when the container is launched)
  - only one CMD is allowed
    - if multiple, last one wins

## building images

- code to build an image:
  - docker image build -t customnginx .
    - -t (tag) - tag given to image
    - . (build using the file in the directory)
- gives you a hash at the end
- order matters
  - everything before a change is cached
  - everything after a change has to be re-built
- __Best Practice:__: Keep the things you change the least at the top of the file, the things you change the most at the bottom
- 