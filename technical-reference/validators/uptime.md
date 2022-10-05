# Uptime

To maximize uptime, validators should set up a backup node. To prevent double signing, dedicated Tendermint node signers such as [tmkms](https://github.com/iqlusioninc/tmkms) or [horcrux](https://github.com/strangelove-ventures/horcrux) can be used.

> If you’re new to running a validator, it's recommended to start out with tmkms to get your feet wet then ultimately make the jump to horcrux after you have a better understanding of cosmos infrastructure.

## Monitoring Tools

A popular uptime monitoring tool for Tendermint chains like Canto is [TenderDuty](https://github.com/blockpane/tenderduty). To get started, follow these steps:

1. Install tenderduty per the [official docs](https://github.com/blockpane/tenderduty/blob/main/docs/install.md) based on your preference (Docker or systemd).
2. Edit `config.yml` based on your validator and preferences:
   * Name the chain "Canto"
   * Add chain ID (`canto_7700-1` for mainnet)
   * Add your valoper address (using `cantod keys show <keyname> -a --bech val`)
   * Get relevant API keys (Discord, Telegram, PagerDuty) and set your alert config
3. Finally, start the service per the docs.

An alternative monitoring tool is [PANIC](https://github.com/SimplyVC/panic).

###
