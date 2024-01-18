# Bridging from Canto

With the [**canto.io**](https://canto.io/bridge) frontend, you can bridge from Canto to Ethereum or to Cosmos Hub and other IBC-enabled chains. To ensure smooth bridging, assets can only be bridged to their native chains.

## Bridge ERC20s To Ethereum <a href="#erc20" id="erc20"></a>

{% hint style="info" %}
A Cosmos wallet like Keplr is no longer needed to bridge ERC20s from Canto to Ethereum. However, please make sure your EVM wallet supports custom chains e.g. Metamask.
{% endhint %}

ERC20 tokens like WETH, USDC, and USDT can be bridged from Canto to Ethereum via Gravity Bridge.  To do so, follow these steps:

1. Navigate to [**canto.io/bridge**](https://canto.io/bridge) and select the `BRIDGE OUT` tab.
2. Select the Ethereum-native asset you wish to bridge and input the quantity.
3. Choose a bridging speed and click `BRIDGE OUT`.
4. Sign the messages in your Ethereum wallet.
5. Between signing messages, accept the prompts to switch networks to Gravity Bridge and then back to Canto as they appear.

<figure><img src="../../.gitbook/assets/bridge-out-v3.JPG" alt=""><figcaption></figcaption></figure>

## Bridge Canto/cNOTE to Ethereum (via LayerZero) <a href="#ofts" id="ofts"></a>

CANTO and cNOTE can be bridged directly from Canto to Ethereum via LayerZero. Aside from an Ethereum wallet such as MetaMask, this path requires no additional wallets or tooling.

To bridge CANTO or cNOTE from Canto to Ethereum, follow these steps:

1. Navigate to [**canto.io/bridge**](https://canto.io/bridge) and select the `BRIDGE OUT` tab.
2. Select the asset you wish to bridge and input the quantity.
3. Click `BRIDGE OUT` and confirm the transactions in your Ethereum wallet:

<figure><img src="../../.gitbook/assets/bridge-out.png" alt=""><figcaption></figcaption></figure>

## Bridge IBC Tokens To Cosmos Chains <a href="#ibc" id="ibc"></a>

To bridge from Canto to Cosmos Hub or other IBC chains, you'll need to move your assets to the Canto Bridge first:

1. Navigate to [**canto.io/bridge**](https://canto.io/bridge) and select the `BRIDGE OUT` tab.
2. Select the asset you wish to bridge and input the quantity.
3. Click `BRIDGE OUT` and enter the address for the asset's native chain from your Keplr Wallet.
4. Confirm and sign the messages in your Ethereum wallet.

<figure><img src="../../.gitbook/assets/bridge-out-cosmos.png" alt=""><figcaption></figcaption></figure>
