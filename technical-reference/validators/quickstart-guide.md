# Quickstart

This page contains step-by-step instructions for launching a Canto validator node.

<details>

<summary>Hardware Requirements</summary>

**Minimum:** 16GB RAM, 100GB NVME SSD, 3.2 GHz x 4 CPU

**Recommended:** 32GB RAM, 500GB NVME SSD, 4.2 GHz x 6 CPU

**Operating System:** Linux (x86\_64 or amd64) e.g. Ubuntu or Arch Linux

</details>

## 1. Install Dependencies

Follow these steps to install dependencies, depending on your operating system:

#### **Ubuntu**

```
sudo snap install go --classic
sudo apt-get install git
sudo apt-get install gcc
sudo apt-get install make
```

#### **Arch Linux**

```
pacman -S go
pacman -S git
pacman -S gcc
pacman -S make
```

## 2. Install `cantod`

Clone the official repo and install:

```
git clone https://github.com/Canto-Network/Canto.git
cd Canto
git checkout genesis
make install
sudo mv $HOME/go/bin/cantod /usr/bin/
```

Generate and store keys:

```
cantod keys add <key_name>
```

To generate keys using a Ledger hardware wallet, use the `--ledger` flag. To recover keys from an existing mnemonic, use the `--recover` flag.

Store a backup of your keys and mnemonic securely offline.

Save the generated public key config in the main Canto directory as `<key_name>.info`:

```
sudo nano <key_name>.info
```

It should look like this:

```
pubkey: {
  "@type":" ethermint.crypto.v1.ethsecp256k1.PubKey",
  "key":"############################################"
}
```

You'll use this file later when creating your validator transaction.

## 3. Initialize Validator

Initialize the node and download the genesis file:

```
cantod init <MONIKER> --chain-id canto_7700-1
cd ~/.cantod/config
rm genesis.json
wget https://github.com/Canto-Network/Canto/raw/genesis/Networks/Mainnet/genesis.json
```

Replace `<moniker>` with whatever you'd like to name your validator.

## 4. Edit Config

```
# Add persistent peers to config.toml
sed -i 's/persistent_peers = ""/persistent_peers = "ec770ae4fd0fb4871b9a7c09f61764a0b010b293@164.90.134.106:26656"/g' $HOME/.cantod/config/config.toml

# Set minimum gas price in app.toml
sed -i 's/minimum-gas-prices = "0acanto"/minimum-gas-prices = "0.0001acanto"/g' $HOME/.cantod/config/app.toml
```

## 5. Create systemd Service

Create the systemd service file:

```
sudo nano /etc/systemd/system/cantod.service
```

Copy and paste the following configuration and save:

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

## 6. Start the Node

```
# Reload service files
sudo systemctl daemon-reload

# Create the symlink
sudo systemctl enable cantod.service

# Start the node
sudo systemtl start

# Show logs
journalctl -u cantod -f
```

You should then get several lines of log files and then see: `No addresses to dial. Falling back to seeds module=pex server=node`

This is an indicator things thus far are working and now you need to create your validator txn. `^c` out and follow the next steps.

## 7. Create Validator Transaction

Modify the following items below, removing the `<>`

* `<KEY_NAME>` should be the same as `<key_name>` when you followed the steps above in creating or restoring your key.
* `<VALIDATOR_NAME>` is whatever you'd like to name your node
* `<DESCRIPTION>` is whatever you'd like in the description field for your node
* `<SECURITY_CONTACT_EMAIL>` is the email you want to use in the event of a security incident
* `<YOUR_WEBSITE>` the website you want associated with your node
* `<TOKEN_DELEGATION>` is the amount of tokens staked by your node (minimum `1acanto`)

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
--fees 30000000000000000acanto \
--gas 300000
```

Your validator wallet must contain a non-zero amount of native $CANTO in order to send the validator transaction. To get some, follow these steps:

1. Run `cantod debug addr $(cantod keys show <key_name> -a)` to see your validator's Bech32 and 0x addresses.
2. Send funds from a Canto EVM wallet to the 0x address shown, or request funds to that address from a faucet such as the #social-faucet in the [Canto Discord](https://discord.gg/canto).
3. Alternatively, ask a validator who already has native $CANTO to send funds to the Bech32 Acc address.

## 8. Update Binary

State breaking software upgrades took place at blocks:

* 218225 (v2.0.0)
* 1231500 (v3.0.0)
* 1274863 (v4.0.0)

Upon reaching these blocks while syncing a validator node, you will need to update the `cantod` binary.

To do so, checkout the correct branch and re-install the binary. For example:

```
git checkout v4.0.0
make install
```

Then, restart the node:

```
sudo systemctl stop cantod.service
sudo systemctl start cantod.service
```

For future binary upgrades, you will need to `git pull` to fetch the updated binary before you attempt to install it.
