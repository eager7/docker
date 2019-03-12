# Build Geth in a stock Go builder container
FROM golang:1.12-alpine as eth_builder

RUN apk add --no-cache make gcc musl-dev linux-headers git

WORKDIR /go/src/github.com/ethereum/

RUN git clone -v https://github.com/ethereum/go-ethereum && cd /go/src/github.com/ethereum/go-ethereum && make all

RUN wget https://gist.githubusercontent.com/eager7/f766c7f8e2c0a69a0badb8769ab79cd8/raw/d229eacd65df8255a9faf43c3889126aece9b289/genesis.json

ENTRYPOINT [""]

# Pull all binaries into a second stage deploy alpine container
FROM alpine:latest

WORKDIR /ethereum/

RUN apk add --no-cache ca-certificates \
    && chmod 777 /ethereum/ -R

COPY --from=eth_builder /go/src/github.com/ethereum/genesis.json /ethereum/

COPY --from=eth_builder /go/src/github.com/ethereum/go-ethereum/build/bin/* /usr/local/bin/

EXPOSE 8545 8546 30303 30303/udp

ENTRYPOINT [""]
