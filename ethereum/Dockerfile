# Build Geth in a stock Go builder container
FROM golang:1.12-alpine as eth_builder

RUN apk add --no-cache make gcc musl-dev linux-headers git

WORKDIR /go/src/github.com/ethereum/

RUN git clone -v https://github.com/ethereum/go-ethereum && cd /go/src/github.com/ethereum/go-ethereum && make all

ENTRYPOINT [""]

# Pull all binaries into a second stage deploy alpine container
FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=eth_builder /go/src/github.com/ethereum/go-ethereum/build/bin/* /usr/local/bin/

EXPOSE 8545 8546 30303 30303/udp

ENTRYPOINT ["geth", "--rpc", "--rpcapi \"db,eth,net,web3,personal\""]