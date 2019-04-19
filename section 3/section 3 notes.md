# Section 3 Notes

## basic docker commands

- check docker version
  - docker version
- check docker status
  - docker info
- list all running docker containers
  - docker container ls -a
- start a docker container
  - docker container run -d --name given_name -p 80:80 nginx
- stop a docker container
  - docker container stop given_name
- remove a docker container
  - docker container rm given_name
- force stop/remove docker container
  - docker container rm -f given_name
- process list for a container
  - docker container top given_name
- details of one container configuration
  - docker container inspect given_name
- performance stats for all containers
  - docker container stats
- view logs for a container
  - docker container logs given_name