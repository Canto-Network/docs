# Application Specific Dollar

[Application Specific Dollar](../../neofinance/application-specific-dollar.md) is a Canto-native protocol that allows teams to earn yield on user deposits by deploying white-label stablecoins backed by [NOTE](https://docs.canto.io/free-public-infrastructure-fpi/note). asD V2 consists of the following contracts:

* [`asdOFT`](asdoft.md) – an asD token. Each asD instance exists as a deployment of this contract.
* [`asdRouter`](asdrouter.md) – enables asD tokens to be minted from other chains with USDC deposits.
* [`asdUSDC`](asdusdc.md) – a wrapper for whitelisted representations of USDC.

## Getting Started

To create an asD token, [deploy the `asdOFT` contract](asdoft.md#deployment) using your development tool of choice.

### Minting

To mint an asD token, call the [mint](asdoft.md#mint) method on the asD token contract.

To mint by depositing USDC from another network, [send USDC to the LayerZero endpoint](asdrouter.md#minting) on that network with the correct message.

### Withdrawals

To retrieve an asD token's underlying NOTE, call the [burn](asdoft.md#burn) method on the asD token contract.

If the token was minted with a USDC deposit, the withdrawal must be made manually:

1. If necessary, bridge the asD OFT back to Canto.
2. Unwrap ([burn](asdoft.md#burn)) the asD token to retrieve the underlying NOTE.
3. Swap the NOTE for USDC.
4. Bridge USDC back to the origin chain.
