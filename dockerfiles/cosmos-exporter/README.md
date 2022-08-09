# Cosmos-Exporter

An exporter used to get blockchain metrics from the validators.
It queries nodes to extract informations concerning validators and wallets.

# Common configuration args

--node blockchain grpc address <br />
--tendermint-rpc tendermint <br />
--denom crypto-currency <br />
--bech-prefix <br />

Do not forget to open port 9300 to let prometheus scrape the exporter.

# Kubernetes config example

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
Based on the following project, you can find an exhaustive configuration list here : <https://github.com/solarlabsteam/cosmos-exporter> 
Here you can find the Dockerfile we coded based on the project: <>