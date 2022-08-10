# Cosmos-Exporter

An exporter used to get cosmos based blockchain metrics from a runnning node.
It queries a node to extract informations concerning: 
- The blockchain network in general
- Some specific validators and wallets.

## Common configuration args

- `--node` The gRPC node URL. Defaults to `localhost:9090`
- `--tendermint-rpc` Tendermint RPC URL to query node stats. Defaults to `http://localhost:26657`
- `--denom` The blockchain currency. Defaults to `uxprt`
- `--bech-prefix` the global prefixes for addresses. Defaults to `persistence`

Do not forget to open port 9300 to let prometheus scrape the exporter.

## Kubernetes config example

```yaml
containers:
    - name: exporter
      image: okp4/cosmos-exporter
      imagePullPolicy: Always
      command:
        - "cosmos-exporter"
      args:
        - "--node"
        - "$(NODE_HOST):9090"
        - "--tendermint-rpc"
        - "http://$(NODE_HOST):26657"
        - "--denom"
        - "uknow"
        - "--bech-prefix"
        - "okp4"
      ports:
        - name: cosmos-metrics
          containerPort: 9300
```

## To go further

Based on the following project, you can find an exhaustive configuration list here : <https://github.com/solarlabsteam/cosmos-exporter>

Here you can find the Dockerfile we coded based on the project: <https://github.com/okp4/docker-images/blob/main/dockerfiles/cosmos-exporter/v0.3.0/Dockerfile>
