FROM golang:alpine as build

MAINTAINER David Knezic <davidknezic@gmail.com>

RUN apk add --no-cache git make \
 && git clone -b 'v0.4.2-beta' --depth 1 https://github.com/lightningnetwork/lnd.git /go/src/github.com/lightningnetwork/lnd \
 && cd /go/src/github.com/lightningnetwork/lnd \
 && make \
 && make install

FROM alpine

EXPOSE 9735 10009 8080

WORKDIR /

COPY --from=build /go/bin/lnd /
COPY --from=build /go/bin/lncli /

ENTRYPOINT ["/lnd"]
