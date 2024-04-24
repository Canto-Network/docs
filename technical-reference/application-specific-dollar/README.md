# Application Specific Dollar

[Application Specific Dollar](../../neofinance/application-specific-dollar.md) is a Canto-native protocol that allows teams to earn yield on user deposits by deploying white-label stablecoins backed by [NOTE](https://docs.canto.io/free-public-infrastructure-fpi/note). asD V2 consists of the following contracts:

* [`asdOFT`](asdoft.md) – an asD token. Each asD instance exists as a deployment of this contract.
* [`asdRouter`](asdrouter.md) – enables asD tokens to be minted from other chains with USDC deposits.
* [`asdUSDC`](asdusdc.md) – a wrapper for whitelisted representations of USDC.

## Getting Started

To create an asD token, [deploy the `asdOFT` contract](asdoft.md#deployment) using your development tool of choice.

To enable bridging of an asD token to other networks:

* Deploy a [generic OFT](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/OFT.sol) on each network you wish to support.
* [Call `setPeer` on all OFT deployments](https://docs.layerzero.network/v2/developers/evm/oft/quickstart#setting-trusted-peers) (including the asD token on Canto) to link them.

### Minting

To mint an asD token, call the [mint](asdoft.md#mint) method on the asD token contract.

To mint by depositing USDC from another network, first obtain a whitelisted USDC OFT on the origin network (by wrapping or swapping). Then call the [LayerZero `send` method](https://docs.layerzero.network/v2/developers/evm/oft/composing#sending-token) on the OFT passing the [`composeMsg` paramater](asdrouter.md#minting).

The `asdRouter` contract handles swapping USDC for NOTE, minting the asD token, and bridging it back to the specified network and address.

### Withdrawals

To retrieve an asD token's underlying NOTE, call the [burn](asdoft.md#burn) method on the asD token contract.

If the token was minted with a USDC deposit, the withdrawal must be made manually:

1. If necessary, bridge the asD OFT back to Canto.
2. Unwrap ([burn](asdoft.md#burn)) the asD token to retrieve the underlying NOTE.
3. Swap the NOTE for USDC.
4. Bridge USDC back to the origin chain.
