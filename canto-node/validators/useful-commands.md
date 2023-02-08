# Useful Commands

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
