# avalanche-proxy

Reverse Proxy for avalanche/geth nodes


![Overview](images/overview.png)

## Features

- Health check base on last synced block timestamp
- Merge websocket port with http port

## Config

| Flag | Type | Description | Default |
| --- | --- | --- | --- |
| -addr | string | HTTP listening address | :80 |
| -tls.addr | string | HTTPS listening address | :443 |
| -tls.key | string | TLS private key file | |
| -tls.cert | stirng | TLS certificate file | |
| -geth.addr | string | Geth address | 127.0.0.1 |
| -geth.http | string | Geth http port | 8545 |
| -geth.ws | string | Geth websocket port | 8546 |
| -geth.metrics | string | Geth metrics port | 6060 |
| -geth.block-unit | duration | Block timestamp unit | 1s |
| -geth.healthy-duration | duration | Duration from last block that mark as healthy | 1m |

## Running

### Docker

```shell
#!/bin/bash
NAME=geth-proxy
IMAGEmanifoldfinance/avalanche-proxy
TAG=latest
ARGS="-geth.healthy-duration=15s"

docker pull $IMAGE:$TAG
docker stop $NAME
docker rm $NAME
docker run -d --restart=always --name=$NAME --net=host \
  --log-opt max-size=10m \
  $IMAGE:$TAG $ARGS
```

## License

MIT
