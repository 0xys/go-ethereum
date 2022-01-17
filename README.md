# Start private test net
https://geth.ethereum.org/docs/interface/private-network
https://geth.ethereum.org/docs/interface/command-line-options

## Build
```
make geth
```
https://geth.ethereum.org/docs/install-and-build/installing-geth

## Create account
```bash
# if password is forgotten, delete existing accounts
./build/bin/geth account list

# create account if none exists
./build/bin/geth account new
# e.g. 0xA31E26E525A4108c1FE47E3A794420A8D73Da243
```

## Genesis config
```
./build/bin/geth removedb
```
```
./build/bin/geth init genesis.json
```

1. Add configured addresses to `alloc` section.
2. in `0x0000000000000000000000000000000000000000000000000000000000000000xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000`, replace `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` with your account.

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
  "extradata": "0x0000000000000000000000000000000000000000000000000000000000000000xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "alloc": {
    "a31e26e525a4108c1fe47e3a794420a8d73da243": { "balance": "300000000000000000000" },
    "6a5a897b080919aafa2e02969c5bfbcce184a97e": { "balance": "500000000000000000000" }
  }
}
```
## Start Mining Private Network
- fill `<0x...>` with the addresses generated.
```bash
./build/bin/geth --unlock 0x5623594223fD9eEbA2EBBf8739Cc898c1a5c6b6c,0x9758Bf155af369dAE439803039f3E682653eBd3E --allow-insecure-unlock --http --nodiscover --mine --miner.threads=1 --miner.etherbase=0x0000000000000000000000000000000000000000
```

### get latest block height
```
curl 127.0.0.1:8545 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```
### balance and send
```
geth attach
```
- https://web3js.readthedocs.io/en/v1.2.11/web3-eth.html
```
eth.getBalance("0x5623594223fD9eEbA2EBBf8739Cc898c1a5c6b6c")
```
```
eth.sendTransaction({from: "0x5623594223fD9eEbA2EBBf8739Cc898c1a5c6b6c", to: "0x9758Bf155af369dAE439803039f3E682653eBd3E", value: 1})
```

## errors
> `authentication needed: password or unlock`
- reset accounts
- https://ethereum.stackexchange.com/questions/19122/authentication-needed-password-or-unlock-error-when-trying-to-call-smart-cont

> `err="unauthorized signer"`
- https://ethereum.stackexchange.com/questions/68249/block-sealing-failed-err-unauthorized-signer
- in genesis.json, replace `5623594223fD9eEbA2EBBf8739Cc898c1a5c6b6c` with you account address in the property `"extradata": "0x00000000000000000000000000000000000000000000000000000000000000005623594223fD9eEbA2EBBf8739Cc898c1a5c6b6c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"`.