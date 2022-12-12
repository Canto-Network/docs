# FAQ

This page contains frequently asked questions, common errors and their solutions, as well as tips for troubleshooting.

## General

### Is there an active validator set?

Yes, Canto has an active validator set consisting of the 100 largest validators sorted by total stake (including self-delegated tokens).

Only validators in the active set are subject to slashing and earn staking rewards.

### How do I join the active validator set?

After sending the `create-validator` transaction, your validator will be automatically added to the active set if/when it has sufficient total stake to be in the top 100 validators.

If your validator was previously in the active set and has been jailed, use the `cantod tx slashing unjail` command to rejoin the active set.

### **Why is my validator not in the active set, with the `unbonding` status?**

For newly-created validators, there is some delay before showing up in the active set.

## Security

### **What ports should I open?**

Unless you intend to run a public seed node, you should **keep all ports closed**. If you leave all incoming ports closed, you will still be able to initiate a connection, but others will not be able to initiate a connection with you.

### **How do I run a public seed node?**

For those looking to run a public seed node, we recommend a [sentry node architecture](https://forum.cosmos.network/t/sentry-node-architecture-overview/454). This involves closing all ports on the validator and only exposing it to three sentry nodes which are in turn exposed to the internet.

## Other

### Can I use Docker?

Yes, you can use Docker. You can use a package like [Cosmos Omnibus](https://github.com/ovrclk/cosmos-omnibus).

## IBC Denom  Reference

```
ibc/641AA23673D8C7B9D93DF95FCA9E94C374AB1651FC066B976927915A5DEEFD28 - usdc

ibc/71CCCF108C28852D85E5127DD2C6092DBB9F7C786C24E6E462AD901F694ABFDA - Tether

ibc/9117A26BA81E29FA4F78F57DC2BD90CD3D26848101BA880445F119B22A1E254E - Atom 

ibc/CFA1D6C76182040F6B846AE2EF82DB7F8E0879E30CDFD6BFCAF699D29955E47F - Grav

ibc/05AA106DCCDE3E51C3C0694B348A8815D7F4906C968650A765EB2296D912C39F - WETH
```
