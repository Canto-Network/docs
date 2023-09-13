# Archive Node

You may wish to archive the entire history of the Canto blockchain in order to index it with a Graph node or to roll your own block explorer. This means spinning up an **archive node**.

Complete step-by-step instructions for launching an archive node are provided below. If you're already comfortable installing and upgrading `cantod`, see step four for archive-specific config details.

As of block 2,500,000, the full archive state of Canto uses approximately 600GB of storage.

## 1. Install Dependencies <a href="#install-dependencies" id="install-dependencies"></a>

Install dependencies (Ubuntu):

```shell
sudo snap install go --classic
sudo apt-get install git
sudo apt-get install gcc
sudo apt-get install make
```

## 2. Install `cantod` <a href="#install-cantod" id="install-cantod"></a>

Clone the official repo and install the v1.0.0 binary:

```shell
git clone https://github.com/Canto-Network/Canto.git
cd Canto
git checkout v1.0.0
make install
sudo mv $HOME/go/bin/cantod /usr/bin/
```

## 3. Initialize `cantod` <a href="#initialize-cantod" id="initialize-cantod"></a>

Initialize the node and download the genesis file:

```shell
cantod init <MONIKER> --chain-id canto_7700-1
cd ~/.cantod/config
rm genesis.json
wget https://github.com/Canto-Network/Canto/raw/genesis/Networks/Mainnet/genesis.json
```

## 4. Edit Config <a href="#edit-config" id="edit-config"></a>

As when setting up a validating node, you'll need to set a seed peer (or persistent peers) as well as minimum gas prices:

```shell
# Add seed peer to config.toml
sed -i 's/seeds = ""/seeds = "ade4d8bc8cbe014af6ebdf3cb7b1e9ad36f412c0@seeds.polkachu.com:15556"/g' $HOME/.cantod/config/config.toml

# Set minimum gas price in app.toml
sed -i 's/minimum-gas-prices = "0acanto"/minimum-gas-prices = "0.0001acanto"/g' $HOME/.cantod/config/app.toml
```

**For an archive node specifically, the most important config setting is the pruning setting, which should be set to `nothing`:**

```shell
# Set pruning in app.toml
sed -i 's/pruning = "default"/pruning = "nothing"/g' $HOME/.cantod/config/app.toml
```

## 5. Create `systemd` Service <a href="#create-systemd-service" id="create-systemd-service"></a>

Create the `systemd` service file:

```shell
sudo nano /etc/systemd/system/cantod.service
```

Copy and paste the following configuration and save:

```shell
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

## 6. Start the Node <a href="#start-node" id="start-node"></a>

```shell
# Reload service files
sudo systemctl daemon-reload

# Create the symlink
sudo systemctl enable cantod.service

# Start the node
sudo systemctl start cantod

# Show logs
journalctl -u cantod -f
```

If your node has issues connecting to the seed peer, you can [manually download an address book](https://polkachu.com/addrbooks/canto).

## 7. Update Binary <a href="#update-binary" id="update-binary"></a>

State breaking software upgrades took place at blocks:

* 218225 (v2.0.0)
* 1231500 (v3.0.0)
* 1274863 (v4.0.0)
* 2669495 (v5.0.0)
* TBD (v6.0.0)
* TBD (v7.0.0)

{% hint style="warning" %}
**Important**: v2.0.0 may cause AppHash errors at blocks that contained governance proposals (e.g. 804212). To avoid this, build from the `thomas/archive-patch` branch instead.
{% endhint %}

Upon reaching these blocks while syncing an archive node, the node will halt and throw an error every time it restarts until you update the binary. To do so, follow these steps:

```shell
# Stop cantod
sudo systemctl stop cantod

# Delete old binary from path and install new binary (run in /Canto/ folder)
git checkout thomas/archive-patch # Replace "thomas/archive-patch" with v3/4/5.0.0 as needed
sudo rm /usr/bin/cantod
make install
sudo mv $HOME/go/bin/cantod /usr/bin/

# Restart
sudo systemctl start cantod
```

For future binary upgrades, you will need to `git pull` to fetch the updated binary before you attempt to install it.
