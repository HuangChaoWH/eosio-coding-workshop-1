# Install Docker

- Follow this link: https://www.docker.com/get-started

# Setup development dir (OSX)

```
mkdir contracts
cd contracts
pwd
```

# Setup NODEOS

- Pull docker image
```
docker pull eosio/eos
```
- Run a container for this image
```
docker run --name eosio \
  --publish 7777:7777 \
  --publish 127.0.0.1:5555:5555 \
  --volume CONTRACTS_DIR:CONTRACTS_DIR \
  --detach \
  eosio/eos \
  /bin/bash -c \
  "keosd --http-server-address=0.0.0.0:5555 & exec nodeos -e -p eosio --plugin eosio::producer_plugin --plugin eosio::history_plugin --plugin eosio::chain_api_plugin --plugin eosio::history_plugin --plugin eosio::history_api_plugin --plugin eosio::http_plugin -d /mnt/dev/data --config-dir /mnt/dev/config --http-server-address=0.0.0.0:7777 --access-control-allow-origin=* --contracts-console --http-validate-host=false --filter-on='*'"
```
- Check if this is working
```
docker logs --tail 10 eosio
```

# Create Wallet

```
docker exec -it eosio bash
cleos --wallet-url http://127.0.0.1:5555 wallet list keys

```

# Check if Nodeos endpoints are working

```
curl http://localhost:7777/v1/chain/get_info
```

# Setup Cleos
```
alias cleos='docker exec -it eosio /opt/eosio/bin/cleos --url http://127.0.0.1:7777 --wallet-url http://127.0.0.1:5555'
```

# Start/Stop container
```
docker start eosio
docker stop eosio
```
