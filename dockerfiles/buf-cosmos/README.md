# buf-cosmos

A [buf.build CLI](https://buf.build/product/cli/) image with necessary `protoc` plugins to generate sources from [Cosmos SDK](https://github.com/cosmos/cosmos-sdk) based protobufs.

## Usage

```sh
docker run -ti --rm \
    -v ${HOME}/.cache:/root/.cache \
    -v `pwd`:/proto \
    -w /proto \
    okp4/buf-cosmos \
    generate proto --template buf.gen.proto.yaml -v
```
