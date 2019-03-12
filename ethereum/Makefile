.PHONY: all run clean dist_clean

repository:="plainchant/ethereum:golang"
name:=ethereum_private

default: all

all:
	docker build  -t repository ./

builder:
	docker build --target builder -t eth_builder:v1 ./

run:
	docker run -d -name $name -port 8555:8545 geth --networkid 13141 --datadir /ethereum --rpc --rpcapi db,eth,net,web3,personal

clean:
	docker stop $name
	docker rm $name

dist_clean:
	-docker stop `docker ps -a -q`
	-docker rm `docker ps -a -q`
	-docker rmi $$(docker images | grep "none" | awk '{print $$3}')
	-docker rmi ${repository}
	#-docker rmi eth_builder:v1

