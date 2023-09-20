# Onboarding Module

The `x/onboarding` module is a custom Canto module that automatically swaps a small amount of bridged IBC tokens for $CANTO, and converts the remaining IBC tokens into their corresponding ERC20 tokens on the Canto EVM.

It was proposed in [CPIP-002](https://github.com/Canto-Network/CIPs/blob/main/CPIPS/CPIP-002.md) in order to improve the Canto onboarding UX from Ethereum, and later implemented in [Canto v7.0.0](https://canto.io/governance/proposal/113).

### Overview

The `x/onboarding` module consists of two components, which are both executed in the `Keeper.OnRecvPacket` callback:

* The **swap** component checks the recipient's $CANTO balance on the Canto EVM, and automatically swaps a a small amount of bridged IBC tokens for $CANTO if it is below the governance-controlled threshold (`AutoSwapThreshold`).
* The **convert** component automatically converts the remaining bridged IBC tokens into their corresponding ERC20 tokens on the Canto EVM.

The behavior of the module is non-atomic, meaning that IBC transfers are still processed even if one or both of the components fail.

### Swap

The swap component is a fork of IRISNET's [Coinswap module v1.6](https://github.com/irisnet/irismod/tree/v1.6.0/modules/coinswap), an AMM. Changes in the forked implementation include:

* Only token pairs on the whitelist can be created as a pool.
  * Pool creation fails if the token pair is not on the whitelist.
  * Initial whitelist: `Canto/USDC.grv`, `Canto/USDT.grv`, `Canto/ETH.grv`
* There is a limit on the number of $CANTO tokens for each pool.
  * Deposits will fail if the amount of $CANTO for the pool exceeds 10,000 Canto.
* Double swaps are disabled.

For risk management purposes, a swap will fail if the input coin amount exceeds a pre-defined limit (10 USDC, 10 USDT, 0.01 ETH) or if the swap amount limit is not defined.

### Convert

The convert component auto-converts the bridged IBC token into an ERC20 token on the Canto EVM, as in the [Evmos implementation](https://github.com/evmos/evmos/blob/fc612fc22846c00e7b8ae296215eea33cef09270/x/erc20/keeper/ibc\_callbacks.go#L36) of this feature.

### Governance Parameters

The module has three parameters which are controlled by governance:

* **`EnableOnboarding`:** Enables or disables the module (default value: `true`)
* **`AutoSwapThreshold`:** The threshold balance of $CANTO below which the swap component is triggered (default value: `4 canto`)
* **`WhitelistedChannels`:** The list of IBC channels the module is enabled for. (default value: `["channel-0"]` – Gravity Bridge)
