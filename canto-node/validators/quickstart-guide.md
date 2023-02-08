# Quickstart Guide

This page contains step-by-step instructions for launching a Canto validator node.

Once you've set up your node, join the [Canto Network Validator Announcements channel](https://discord.com/channels/993968517906960445/995469213080752159/1071089114503462982) on Telegram to stay up-to-date with chain upgrades and other governance proposals.

<details>

<summary>Hardware Requirements</summary>

**Minimum:** 16GB RAM, 100GB NVME SSD, 3.2 GHz x 4 CPU

**Recommended:** 32GB RAM, 500GB NVME SSD, 4.2 GHz x 6 CPU

**Operating System:** Linux (x86\_64 or amd64) e.g. Ubuntu or Arch Linux

</details>

## 1. Install Dependencies

Install dependencies (Ubuntu):

```sh
sudo snap install go --classic
sudo apt-get install git
sudo apt-get install gcc
sudo apt-get install make
```

## 2. Install `cantod`

Clone the official repo and install the current binary:

```sh
git clone https://github.com/Canto-Network/Canto.git
cd Canto
git checkout v5.0.0
make install
sudo mv $HOME/go/bin/cantod /usr/bin/
```

Generate and store keys:

```sh
cantod keys add <key_name>
```

To recover keys from an existing mnemonic, use the `--recover` flag.

## 3. Initialize Validator

Initialize the node and download the genesis file:

```sh
cantod init <MONIKER> --chain-id canto_7700-1
cd ~/.cantod/config
rm genesis.json
wget https://github.com/Canto-Network/Canto/raw/genesis/Networks/Mainnet/genesis.json
```

Replace `<moniker>` with whatever you'd like to name your validator.

## 4. Edit Config

```sh
# Add seed peer to config.toml
sed -i 's/seeds = ""/seeds = "ade4d8bc8cbe014af6ebdf3cb7b1e9ad36f412c0@seeds.polkachu.com:15556"/g' $HOME/.cantod/config/config.toml

# Set minimum gas price in app.toml
sed -i 's/minimum-gas-prices = "0acanto"/minimum-gas-prices = "0.0001acanto"/g' $HOME/.cantod/config/app.toml
```

## 5. Create systemd Service

Create the systemd service file:

```sh
sudo nano /etc/systemd/system/cantod.service
```

Copy and paste the following configuration and save:

```sh
[Unit]
Description=Canto Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=/usr/bin/cantod start --trace --log_level info --json-rpc.api eth,txpool,personal,net,debug,web3 --api.enable
Restart=on-failure
StartLimitInterval=0
RestartSec=3
LimitNOFILE=65535
LimitMEMLOCK=209715200

[Install]
WantedBy=multi-user.target
```

## 6. Start Node

```sh
# Reload service files
sudo systemctl daemon-reload

# Create the symlink
sudo systemctl enable cantod.service

# Start the node
sudo systemctl start cantod

# Show logs
journalctl -u cantod -f
```

You should then get several lines of log files. This is an indicator things thus far are working and now you need to create your validator txn. `^c` out and follow the next steps.

## 7. Sync Node

Unless you wish to run an [archive node](../archive-node.md), you should sync your node to the current block using [manual snapshots](node-snapshots.md) or state-sync snapshots.

To use state-sync:

<pre class="language-sh"><code class="lang-sh"><strong># Set vars
</strong><strong>SNAP_RPC="https://canto-rpc.polkachu.com:443"
</strong>LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height)
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000))
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

# Stop node
sudo systemctl stop cantod

# Reset cantod
cantod tendermint unsafe-reset-all --home $CANTO_HOME --keep-addr-book

# Add state-sync settings
sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $CANTO_HOME/config/config.toml

# Restart
sudo systemctl start cantod
</code></pre>

## 8. Create Validator Transaction

Modify the following items below, removing the `<>`

* `<KEY_NAME>` should be the same as `<key_name>` when you followed the steps above in creating or restoring your key.
* `<VALIDATOR_NAME>` is whatever you'd like to name your node
* `<DESCRIPTION>` is whatever you'd like in the description field for your node
* `<SECURITY_CONTACT_EMAIL>` is the email you want to use in the event of a security incident
* `<YOUR_WEBSITE>` the website you want associated with your node
* `<TOKEN_DELEGATION>` is the amount of tokens staked by your node (minimum `1acanto`)

```sh
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

## 9. Update Binary

Once your validating node is up-and-running, join the [Canto Network Validator Announcements channel](https://discord.com/channels/993968517906960445/995469213080752159/1071089114503462982) on Telegram to stay up-to-date with chain upgrades and other governance proposals.

In case of a binary upgrade, you will need to re-fetch the Canto repository and install the new binary before restarting your node:

```sh
git pull

git checkout v5.0.0
make install

# Don't forget to move the installed binary to your path
sudo mv $HOME/go/bin/cantod /usr/bin/

# Restart
sudo systemctl stop cantod.service
sudo systemctl start cantod.service
```
