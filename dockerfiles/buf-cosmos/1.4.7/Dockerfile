FROM golang:1.19-alpine3.16 AS protoc-builder

# hadolint ignore=DL4006,DL3003
RUN apk update \
    && apk add --no-cache curl=7.83.1-r6 make=4.3-r0 git=2.36.5-r0

ENV GOLANG_PROTOBUF_VERSION=1.28.1
ENV GOGOPROTO_VERSION=1.4.7

RUN go install github.com/cosmos/cosmos-proto/cmd/protoc-gen-go-pulsar@760914ff5b20d0420b15c6ce66be8c8808ae40c2 && \
  go install google.golang.org/protobuf/cmd/protoc-gen-go@v${GOLANG_PROTOBUF_VERSION}

RUN git clone https://github.com/cosmos/gogoproto.git

WORKDIR /go/gogoproto

RUN git checkout v${GOGOPROTO_VERSION} && \
  go mod download && \
  make install

RUN go install github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@v1.5.1

FROM bufbuild/buf:1.16.0

RUN wget -q https://github.com/grpc-ecosystem/grpc-gateway/releases/download/v1.16.0/protoc-gen-grpc-gateway-v1.16.0-linux-x86_64 -O /usr/bin/protoc-gen-grpc-gateway \
    && chmod +x /usr/bin/protoc-gen-grpc-gateway

COPY --from=protoc-builder /go/bin/protoc-* /usr/bin/
