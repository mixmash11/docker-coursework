# Section 3-24 Assignment

## The Assignment

### Objective

- Run a nginx, mysql and httpd (apache) server
- all should be run detached and with a custom name
- nginx should listen on port 80:80
- httpd should listen on port 8080:80
- mysql should listen on port 3306:3306

### Notes

- use the -e (environment option) for myqsl to pass in MYSQL_RANDOM_ROOT_PASSWORD=yes

## Solution

### Commands

1. docker container run -d -p 80:80 --name proxy nginx
1. docker container run -d -p 8080:80 --name webhost httpd
1. docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
1. docker container ls -a
1. curl localhost:80
1. docker container stop db
1. docker container stop webhost
1. docker container stop proxy