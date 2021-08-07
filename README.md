# Start private test net
https://geth.ethereum.org/docs/interface/private-network
https://geth.ethereum.org/docs/interface/command-line-options

## Build
```
make geth
```
https://geth.ethereum.org/docs/install-and-build/installing-geth

## Create account
```
./build/bin/geth account new
0xA31E26E525A4108c1FE47E3A794420A8D73Da243
0x6A5A897b080919aafA2E02969c5BfbcCE184a97E
```

## Genesis config
```
./build/bin/geth removedb
```
```
./build/bin/geth init genesis.json
```
```json
{
  "config": {
    "chainId": <YOUR_CHAIN_ID>,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "istanbulBlock": 0,
    "berlinBlock": 0,
    "londonBlock": 0,
    "clique": {
      "period": 5,
      "epoch": 30000
    }
  },
  "difficulty": "1",
  "gasLimit": "8000000",
  "extradata": "0x0000000000000000000000000000000000000000000000000000000000000000a31e26e525a4108c1fe47e3a794420a8d73da2430000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "alloc": {
    "a31e26e525a4108c1fe47e3a794420a8d73da243": { "balance": "300000" },
    "6a5a897b080919aafa2e02969c5bfbcce184a97e": { "balance": "400000" }
  }
}
```
## Start Mining Private Network
```
./geth --unlock 0xa31e26e525a4108c1fe47e3a794420a8d73da243,0x6a5a897b080919aafa2e02969c5bfbcce184a97e --allow-insecure-unlock --http --nodiscover --mine --miner.threads=1 --miner.etherbase=0x0000000000000000000000000000000000000000
```
### get latest block height
```
curl 127.0.0.1:8545 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```