# Section 3-33 Assignment

## The Assignment

### Objective

- DNS round robin test
- create a virtual network (using bridge driver)
- create two containers from elasticsearch:2 image
- research and use --network-alias search when creating them an additional DNS name to respond to
- run alpine nslookup search with --net to see the two containers list for the same DNS name
- run centos curl -s search:9200 with --net multiple times until you see both "name" fields show

### Notes

- network-alias gives us a second DNS name that can be shared by multiple containers.
  - this is distribution sharing
  - it is not load balancing

## Solution

### Commands

- create a virtual network
  - docker network create a_network
- create 2 containers from elasticsearch:2 image
  - docker container run -d --name search1 --network a_network --network-alias search elasticsearch:2
  - docker container run -d --name search2 --network a_network --network-alias search elasticsearch:2
- run alpine nslookup
  - docker container run -it --rm --net a_network alpine nslookup search
- run centos curl
  - docker container run -it --rm --net a_network centos curl -s search:9200
