.PHONY: all run clean dist_clean

repository:="plainchant/ethereum:golang"

default: all

all:
	docker-compose build 

builder:
	docker build --target builder -t eth_builder:v1 ./

run:
	docker-compose up 

clean:
	docker-compose stop
	docker-compose rm

dist_clean:
	-docker rmi $$(docker images | grep "none" | awk '{print $$3}')
	-docker stop `docker ps -a -q`
	-docker rmi ${repository}
	-docker rmi builder:v1

