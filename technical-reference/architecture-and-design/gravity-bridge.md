# Gravity Bridge

Canto utilizes Gravity Bridge as its bridge provider and has fully integrated Gravity into the Canto native UI for a seamless user experience. The audit report can be viewed on [Code4rena](https://code4rena.com/reports/2021-08-gravitybridge).

For step-by-step directions on bridging assets to Canto, see [Getting Started](../../user-guides/connecting-to-canto.md#bridging-assets-to-canto).

## What is Gravity Bridge?

Gravity Bridge is a trustless, neutral bridge between the Ethereum and Cosmos ecosystems built using the Cosmos SDK.&#x20;

Gravity Bridge operates similarly to how many cross-chain bridges work, i.e. locking up a native tokens on one side of the bridge and minting a representation of that token on the other, with a critical difference: Gravity Bridge uses the validator set to sign transactions instead of a multi-sig or permissioned set of actors. \
\
The Gravity Bridge has two components. A Solidity contract on Ethereum (Gravity.sol) and a CosmosSDK module on the Gravity Bridge blockchain.

### Gravity.sol

Gravity.sol is the Solidity contract that holds funds for Gravity Bridge on Ethereum. In contrast to the prevailing trend in other bridge designs, **Gravity.sol** a mere 580 lines of code, compact, and easy to review. It has been audited by three independent teams (Certik, Least Authority, and Code4rena) and it is not upgradable. It does not contain any trusted parties, of any kind.

Gravity.sol is fully controlled by the validators of the Gravity Bridge blockchain in proportion to their stake. This means that the security and decentralization of the bridge is the same as the Gravity Bridge blockchain itself.

For more details on Gravity Bridge, visit: [gravitybridge.net.](https://gravitybridge.net)
