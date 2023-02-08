# Snapshots

## Creating Snapshot

### Create folder for snapshots

```bash
mkdir -p $HOME/snapshots/canto
```

### Clone github repo

```bash
git clone https://github.com/SiddarthVijay/cosmos-snapshots.git
cd cosmos-snapshots
git checkout patch/v1-canto
```

### Create new snapshot

```bash
./canto_snapshot.sh
```

### Automation

You can add script to the cron

```sh
# start every day at 00:00
0 0 * * * /bin/bash -c '/root/canto_snapshot.sh'
```

***

## Consuming Snapshot

Snapshots also available on [Polkachu](https://polkachu.com/tendermint\_snapshots/canto)

### Use Snapshot

Backup $HOME/.canto/priv\_validator\_state.json (cannot be recovered after following steps)

```bash
sudo systemctl stop cantod
cantod unsafe-reset-all
cd $HOME/.cantod
wget -O <snapshot_file>.tar <host_url>
tar -xvf <snapshot_file>.tar 
```

### Restart Node

```bash
sudo systemctl start cantod
# Watch logs
journalctl -u cantod -f
```

***
