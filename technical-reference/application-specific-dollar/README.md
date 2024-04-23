# Application Specific Dollar

[Application Specific Dollar](../../neofinance/application-specific-dollar.md) is a Canto-native protocol that allows teams to earn yield on user deposits by deploying white-label stablecoins backed by [NOTE](https://docs.canto.io/free-public-infrastructure-fpi/note). asD V2 consists of the following contracts:

* `asdOFT` – an asD token. Each asD instance exists as a deployment of this contract.
* `asdRouter` – enables asD tokens to be minted from other chains with USDC deposits.
* `asdUSDC` – a wrapper for whitelisted representations of USDC.
