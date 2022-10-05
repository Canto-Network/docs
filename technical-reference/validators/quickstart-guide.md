# Quickstart Guide

This page contains step-by-step instructions for launching a Canto validator node.

#### Quick links:

* [Genesis file](https://raw.githubusercontent.com/Canto-Network/Canto/genesis/Networks/Mainnet/genesis.json)&#x20;
* [Peers list](https://github.com/Canto-Network/Canto/blob/main/Mainnet/peers.txt)

## Hardware Requirements

| Minimum         | Recommended     |
| --------------- | --------------- |
| 16 GB RAM       | 32 GB RAM       |
| 100 GB NVME SSD | 500 GB NVME SSD |
| 3.2 GHz x4 CPU  | 4.2 GHz x6 CPU  |

**Operating System:**

* Linux (x86\_64) or Linux (amd64)
* Recommended Ubuntu or Arch Linux

## Install Dependencies

Follow these steps to install dependencies, depending on your operating system:

### **Ubuntu**

Install all dependencies:

`sudo snap install go --classic && sudo apt-get install git && sudo apt-get install gcc && sudo apt-get install make`

Or install individually:

* go1.18+: `sudo snap install go --classic`
* git: `sudo apt-get install git`
* gcc: `sudo apt-get install gcc`
* make: `sudo apt-get install make`

### **Arch Linux**

* go1.18+: `pacman -S go`
* git: `pacman -S git`
* gcc: `pacman -S gcc`
* make: `pacman -S make`

## Install `cantod`

**Start by cloning the git repository:**

```
git clone https://github.com/Canto-Network/Canto.git
cd Canto/cmd/cantod
go install -tags ledger ./...
sudo mv $HOME/go/bin/cantod /usr/bin/
```

**Then generate and store keys:**

Replace `<keyname>` below with whatever you'd like to name your key.

* `cantod keys add <key_name>`
* `cantod keys add <key_name> --recover` to regenerate keys with your mnemonic
* `cantod keys add <key_name> --ledger` to generate keys with ledger device

Store a backup of your keys and mnemonic securely offline.

Then save the generated public key config in the main Canto directory as `<key_name>.info`. It should look like this:

```
pubkey: {
  "@type":" ethermint.crypto.v1.ethsecp256k1.PubKey",
  "key":"############################################"
}
```

You'll use this file later when creating your validator txn.

## Set Up Validator

Install cantod binary from `Canto` directory:

`sudo make install`

Initialize the node. Replace `<moniker>` with whatever you'd like to name your validator.

`cantod init <moniker> --chain-id canto_7700-1`

If this runs successfully, it should dump a blob of JSON to the terminal.

Download the Genesis file:

`wget https://github.com/Canto-Network/Canto/raw/genesis/Networks/Mainnet/genesis.json -P $HOME/.cantod/config/`

> **Note:** If you later get `Error: couldn't read GenesisDoc file: open /root/.cantod/config/genesis.json: no such file or directory` put the genesis.json file wherever it wants instead, such as:
>
> `sudo wget https://github.com/Canto-Network/Canto/raw/main/Mainnet/genesis.json -P/root/.cantod/config/`

Edit the minimum-gas-prices in `${HOME}/.cantod/config/app.toml`:

`sed -i 's/minimum-gas-prices = "0acanto"/minimum-gas-prices = "0.0001acanto"/g' $HOME/.cantod/config/app.toml`

Add persistent peers to `$HOME/.cantod/config/config.toml`: `sed -i 's/persistent_peers = ""/persistent_peers = "ec770ae4fd0fb4871b9a7c09f61764a0b010b293@164.90.134.106:26656"/g' $HOME/.cantod/config/config.toml`

Set `cantod` to run automatically:

* Start `cantod` by creating a systemd service to run the node in the background:
* Edit the file: `sudo nano /etc/systemd/system/cantod.service`
* Then copy and paste the following text into your service file. Be sure to edit as you see fit.

```
[Unit]
Description=Canto Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=/root/go/bin/cantod start --trace --log_level info --json-rpc.api eth,txpool,personal,net,debug,web3 --api.enable
Restart=on-failure
StartLimitInterval=0
RestartSec=3
LimitNOFILE=65535
LimitMEMLOCK=209715200

[Install]
WantedBy=multi-user.target
```

## Start the Node

Reload the service files:

`sudo systemctl daemon-reload`

Create the symlinlk:

`sudo systemctl enable cantod.service`

Start the node:

`sudo systemctl start cantod && journalctl -u cantod -f`

You should then get several lines of log files and then see: `No addresses to dial. Falling back to seeds module=pex server=node`

This is an indicator things thus far are working and now you need to create your validator txn. `^c` out and follow the next steps.

### Create Validator Transaction

Modify the following items below, removing the `<>`

* `<KEY_NAME>` should be the same as `<key_name>` when you followed the steps above in creating or restoring your key.
* `<VALIDATOR_NAME>` is whatever you'd like to name your node
* `<DESCRIPTION>` is whatever you'd like in the description field for your node
* `<SECURITY_CONTACT_EMAIL>` is the email you want to use in the event of a security incident
* `<YOUR_WEBSITE>` the website you want associated with your node
* `<TOKEN_DELEGATION>` is the amount of tokens staked by your node (`1acanto` should work here, but you'll also need to make sure your address contains tokens.)



```
cantod tx staking create-validator \
--from <KEY_NAME> \
--chain-id canto_7700-1 \
--moniker="<VALIDATOR_NAME>" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.05 \
--details="<DESCRIPTION>" \
--security-contact="<SECURITY_CONTACT_EMAIL>" \
--website="<YOUR_WEBSITE>" \
--pubkey $(cantod tendermint show-validator) \
--min-self-delegation="1" \
--amount <TOKEN_DELEGATION>acanto \
--fees 20acanto
```

## Useful Commands

Here are some useful commands for node operators:

| Command                                                                  | Description                                                                                     |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| `cantod keys list`                                                       | Lists the names of keys created on your machine                                                 |
| `cantod tendermint show-node-id`                                         | Shows your node ID                                                                              |
| `cantod keys show <keyname> -a --bech val`                               | Gets your valoper address                                                                       |
| `curl http://localhost:26657/status \| jq .result.sync_info.catching_up` | Checks if your node is catching up (query via the RPC, default port 26657)                      |
| `query slashing signing-info $(cantod tendermint show-validator)`        | Checks if you are jailed or tombstoned                                                          |
| `cantod query slashing signing-infos`                                    | Shows blocks your node is missing                                                               |
| `cantod tendermint show-address`                                         | Shows your Tendermint consensus address for comparison to the list of validators missing blocks |

## Security

Unless you intend to run a public seed node, you should **keep all ports closed**. If you leave all incoming ports closed, you will still be able to initiate a connection, but others will not be able to initiate a connection with you.

### Public Seeds

For those looking to run a public seed node, we recommend a [sentry node architecture](https://forum.cosmos.network/t/sentry-node-architecture-overview/454). This involves closing all ports on the validator and only exposing it to three sentry nodes which are in turn exposed to the internet.

Exposing open ports directly to the internet can make your validator vulnerable to DDOS attacks and other security risks.

