FROM golang:alpine as builder
MAINTAINER Jack Murdock <jack_murdock@comcast.com>

WORKDIR /go/src/github.com/comcast/codex-svalinn

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

COPY . .
RUN GO111MODULE=on go build -o svalinn_linux_amd64

FROM alpine

RUN apk --no-cache add ca-certificates
RUN mkdir -p /etc/svalinn
VOLUME /etc/svalinn

EXPOSE 8080

COPY --from=builder /go/src/github.com/comcast/codex-svalinn/svalinn_linux_amd64 /
COPY svalinn.yaml /
ENTRYPOINT ["/svalinn_linux_amd64"]
