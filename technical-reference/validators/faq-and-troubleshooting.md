# FAQ & Troubleshooting

This page contains frequently asked questions, common errors and their solutions, as well as tips for troubleshooting.

## Frequently Asked Questions

#### Can I use Docker?

Yes, you can use Docker. You can use a package like [Cosmos Omnibus](https://github.com/ovrclk/cosmos-omnibus).

**Do I need to have $CANTO in my wallet for the validator to work?**

You need $CANTO to send the `create-validator` transaction, but you do not need $CANTO to sync your node.

**Why is my validator inactive in the validator set, with the `unbonding` status?**

There is some delay before validators show up in the validator set.

**What ports should I open?**

Unless you intend to run a public seed node, you should **keep all ports closed**. If you leave all incoming ports closed, you will still be able to initiate a connection, but others will not be able to initiate a connection with you.

**How do I run a public seed node?**

For those looking to run a public seed node, we recommend a [sentry node architecture](https://forum.cosmos.network/t/sentry-node-architecture-overview/454). This involves closing all ports on the validator and only exposing it to three sentry nodes which are in turn exposed to the internet.

## Common Errors and Solutions

Here are a list of common errors when launching a node and their recommended solutions:

| Error Description                                                                                                     | Recommended Solution(s)                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Default gas fails when staking                                                                                        | Use `--gas auto`                                                                                                                                                                                            |
| `Error: couldn't read GenesisDoc file: open /root/.cantod/config/genesis.json: no such file or directory`             | <p>Put the <code>genesis.json</code> file in the specified location, such as:</p><p><code>sudo wget https://github.com/Canto-Network/Canto/raw/main/Mainnet/genesis.json -P/root/.cantod/config/</code></p> |
| `Error during handshake: error on replay: validator set is nil in genesis and still empty after InitChain`            | <p>Local: Remove <code>datadir</code> and restart<br><br>Cloud: Start a new instance</p>                                                                                                                    |
| `Failed to execute message; message index: 0: failed to delegate; acanto is smaller than acanto: insufficient funds"` | Decrease the amount to less than your total $CANTO balance                                                                                                                                                  |
| `Stopping peer for error`                                                                                             | No action required                                                                                                                                                                                          |

## Tip: Rebuild from Scratch

If you run into unexpected issues when launching your node, it's worth rebuilding from scratch prior to any troubleshooting efforts. Follow these steps:

1. Delete `addressbook.json` in the config
2. Remove all old peers
3. Update persistent peers and seeds to newly shared
4. Fetch the new genesis file
5. Ensure binary is up to date
6. Start your node

## Tip: Consult EVMOS Docs

If you get stuck with something that isn't explained here, a good place to look for more information about your issue is the EVMOS community and docs .

## IBC Denom  Reference

```
ibc/641AA23673D8C7B9D93DF95FCA9E94C374AB1651FC066B976927915A5DEEFD28 - usdc

ibc/71CCCF108C28852D85E5127DD2C6092DBB9F7C786C24E6E462AD901F694ABFDA - Tether

ibc/9117A26BA81E29FA4F78F57DC2BD90CD3D26848101BA880445F119B22A1E254E - Atom 

ibc/CFA1D6C76182040F6B846AE2EF82DB7F8E0879E30CDFD6BFCAF699D29955E47F - Grav

ibc/05AA106DCCDE3E51C3C0694B348A8815D7F4906C968650A765EB2296D912C39F - WETH
```
