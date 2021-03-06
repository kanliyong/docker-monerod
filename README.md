
# docker-monerod

## Description

Run a Monero full node.

The blockchain is loaded from the `/bitmonero` volume. This volume should contain a config file like the included `bitmonero.conf`.

## How to run

```sh
# Clone repository
git clone https://github.com/kanliyong/docker-monerod.git
cd docker-monerod
# Build image:
make build
# Create blockchain volume and copy configuration:
mkdir ~/bitmonero && cp wallet.conf ~/bitmonero && cp bitmonero.conf ~/bitmonero
# Run container
docker run -p 18080:18080 -p 18081:18081 -p 8080:8080 --restart=always -v ~/bitmonero:/bitmonero --name=monerod -td kanliyong/monerod:latest
# View logs
docker logs -f monerod
```

## Create wallet
```bash
curl -X POST \
  http://127.0.0.1:30003/json_rpc \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"create_wallet","params":{"filename":"defaultwallet","password":"123456","language":"English"},"id":1}'

```
## RPC Documents https://getmonero.org/resources/developer-guides/wallet-rpc.html
