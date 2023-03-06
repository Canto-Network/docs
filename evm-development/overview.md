# Overview

The Canto EVM runs [Geth](https://geth.ethereum.org/) and is fully EVM-compatible. This means that building on Canto's execution layer is just like building on Ethereum in that developers can:

* Connect with the same wallets,
* Deploy the same smart contract source code,
* Use the same tooling, and more.

## Canto vs Ethereum

At launch, Canto's execution layer is EVM-equivalent. Its differences from Ethereum include a shorter block time and modified gas fee model.

### Block time

Following the merge, Ethereum's block time is 12 seconds, whereas Canto EVM's block time is approximately 6 seconds.

### Gas fees

Canto EVM uses a modified EIP-1559 gas model _without_ priority fees. The minimum base fee is 1000 acanto (the equivalent of gwei) and self-adjusts based on how full blocks are.
