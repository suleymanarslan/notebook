# Ethereum

## Setup Node

Install Ethereum:

```bash
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository -y ppa:ethereum/ethereum
$ sudo apt-get update
$ sudo apt-get install ethereum
```

Create a shell script to start the node, save it to `/root/start.sh`:

```sh
#!/bin/sh
geth --datadir=~/.gophersland_ethereum_r1 --port=30304 --cache=2048 --rpc --rpcport=8546 --rpcapi=eth,web3,net,personal --syncmode=fast
```

Create a service and save it as `/etc/systemd/system/geth.service`: 

```systemctl
[Unit]
Description=Geth

[Service]
Type=simple
ExecStart=/root/start.sh
WorkingDirectory=/root
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and run the service:
```bash
$ systemctl enable geth
$ systemctl start geth
```

Check if it's running:

```bash
$ systemctl status geth
```

See logs:

```bash
$ journalctl -xu geth.service --since today
```

## Create a new wallet

```js
const EthWallet = require("ethereumjs-wallet")
const bip39 = require("bip39")
const hdkey = require("ethereumjs-wallet/hdkey")

// Generate mnemonic and seed
const mnemonic = bip39.generateMnemonic()
const seed = bip39.mnemonicToSeed(mnemonic)

console.log(`generated mnemonic: ${mnemonic}\n`)

const hdwallet = hdkey.fromMasterSeed(mnemonic)
const walletHdPath = "m/44'/60'/0'/0/"
const wallet = hdwallet.getWallet()
const privateKey = wallet.getPrivateKey().toString("hex")

console.log("address:", wallet.getAddress().toString("hex"))
console.log("private key", privateKey)
console.log("filename", wallet.getV3Filename(Date.now()))

console.log(wallet.toV3("he-yo"))
```

## Restore Wallet

```js
const EthWallet = require("ethereumjs-wallet")
const hdkey = require("ethereumjs-wallet/hdkey")

// by pk
const wallet = EthWallet.fromPrivateKey(
  Buffer.from(
    `${privateKey}`,
    "hex"
  )
)

console.log("address:", wallet.getAddress().toString("hex"))

// by seed
const hdws = hdkey.fromMasterSeed(
  `${seed}`
)

const ws = hdws.getWallet()

console.log("address:", ws.getAddress().toString("hex"))

// by keystore
const v3 = ""
const pwd = ""
const ksw = EthWallet.fromV3(v3, pwd)
console.log("address:", ksw.getAddress().toString("hex"))

```

### Get Balance

```js
const Web3 = require("web3")
const BN = require("bn.js")

const provider = new Web3.providers.HttpProvider(
  `https://rinkeby.infura.io/v3/${key}`
)

const web3 = new Web3(provider)
const big = n => new BN(n.toString(10))

main()

async function main() {
  const balance = big(
    await web3.eth.getBalance(address)
  )

  console.log("Balance:", balance.toString())
}

```
