# Architecture & Design

The Canto network is a sovereign chain built using the [Cosmos SDK](https://docs.cosmos.network/main/intro/overview.html) and custom modules. Cosmos SDK chains can be scaffolded, built and interacted with using the [Ignite CLI.](https://docs.ignite.com/)&#x20;

Canto is EVM-enabled, utilizing a module called [Ethermint](https://github.com/tharsis/ethermint/tree/main/x) which deploys an EVM execution environment enabling Solidity code to be deployed directly from the Ethereum network. Canto enables a native bridge between CosmWasm tokens and ERC-20 standard tokens using the [ERC-20 module](https://github.com/tharsis/evmos/blob/main/x/erc20/spec/README.md).

This is it how it works:

1. The `x/erc20`module maintains a canonical one-to-one mapping of native Cosmos Coin denomination to ERC20 Token contract addresses (i.e `sdk.Coin`  ←→ ERC20), called `TokenPair.` The conversion of the ERC20 tokens ←→ Coin of a given pair can be enabled or disabled via governance.
2. A native Cosmos Coin corresponds to an `sdk.Coin` that is native to the [bank module](https://docs.cosmos.network/master/modules/bank/) (which controls account balances and token supply in Cosmos SDK). It can be either the native staking/gas denomination (eg: EVMOS, ATOM, etc) or an IBC fungible token voucher (i.e with denom format of `ibc/{hash}`). When a proposal is initiated for an existing native Cosmos Coin, the erc20 module will deploy a factory ERC20 contract, representing the ERC20 token for the token pair, giving the module ownership of that contract.
3. During the registration of a Cosmos Coin the following bank `Metadata` is used to deploy a ERC20 contract:
4. Holders of native Cosmos coins and IBC vouchers on the Canto chain can convert their Coin into ERC20 Tokens, which can then be used in the ethermint EVM, by creating a[`ConvertCoin`Tx](https://github.com/tharsis/evmos/blob/main/x/erc20/spec/04\_transactions.md). Vice versa, the [`ConvertERC20`Tx](https://github.com/tharsis/evmos/blob/main/x/erc20/spec/04\_transactions.md) allows holders of ERC20 tokens on the Canto chain to convert ERC-20 tokens back to their native Cosmos Coin representation.
5. The [EVM hooks](https://github.com/tharsis/evmos/blob/main/x/erc20/spec/05\_hooks.md) allows users to convert ERC20s to Cosmos Coins by sending an Ethereum tx transfer to the module account address. This enables native conversion of tokens via Metamask and EVM-enabled wallets for both token pairs that have been registered through a native Cosmos coin or an ERC20 token.

To learn more about the Ethermint module, click [here](https://github.com/evmos/ethermint) (Credit to Tharsis).
