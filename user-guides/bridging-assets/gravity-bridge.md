# Gravity Bridge <-> Canto

This guide allows you to move ETH, USDC, and USDT from Canto to the Cosmos ecosystem and back using IBC, without having to send funds to Ethereum.

## Gravity Bridge -> Canto <a href="#gravity-bridge-canto" id="gravity-bridge-canto"></a>

{% hint style="danger" %}
**Do not attempt to transfer Gravity toekens to the Canto address in your Keplr wallet. Follow the instructions below.**
{% endhint %}

To bridge assets from Gravity Bridge to the Canto network, follow these steps:

1. Navigate to [**bridge.canto.io**](https://bridge.canto.io) \*\*\*\* and connect your MetaMask wallet

![](<../../.gitbook/assets/image (26).png>)

2\. Copy your Canto native address by clicking on it

3\. Navigate to [**bridge.blockscape.network**](https://bridge.blockscape.network) \*\*\*\* and connect your Keplr wallet

4\. Select Gravity Bridge as the source chain and Canto as the destination.

![](<../../.gitbook/assets/blockscape-gb-canto.png>)

5\. Connect your Gravity Keplr wallet *do not* connect Keplr to Canto instead, click the lock icon under 'transfer address' and paste your Canto native address there.

6\. Select the token you would like to bridge and input the quantity. Quantities less than 1 must include a 0 in the ones place value (e.g. `0.99`).

7\. Sign the message in your wallet to confirm the transfer.

Assets bridged to Canto will arrive on the native Canto blockchain within 60 seconds of the Gravity Bridge transaction being confirmed. If you want to use the Canto Lending Market, Canto DEX, and other DApps, you must [convert your assets to the Canto EVM](../converting-assets.md).

## Canto -> Gravity Bridge <a href="#canto-gravity-bridge" id="canto-gravity-bridge"></a>

You will need the following to bridge from Canto To Gravity Bridge

* An IBC wallet (such as Keplr Wallet)

If your assets are on the Canto EVM, you must [convert them](../converting-assets.md) first.

Once you are ready to bridge from Canto to Gravity Bridge, follow these steps:

1. Navigate to [**bridge.canto.io**](https://bridge.canto.io) \*\*\*\* and connect your MetaMask wallet, making sure you are on the Canto network.
2. Select Canto as the _from_ network and Gravity Bridge as the _to_ network.

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.44.23 AM.png>)

2\. Select the token you wish to bridge and enter an amount.

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.46.51 AM.png>)

3\. Open your Keplr wallet and change the network to Gravity Bridge. Copy your Gravity Bridge address and paste it into the bridge interface:

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.51.28 AM.png>)

4\. Click `send token` and sign the transaction in MetaMask. After about a minute, you should see the tokens in your Keplr wallet at the address you provided.

<img src="../../.gitbook/assets/Screen Shot 2022-08-17 at 4.09.04 AM.png" alt="" data-size="original">

5\. Once the tokens are in your Keplr wallet, bridge from Gravity Bridge to any Cosmos ecosystem destination using the [Gravity Bridge portal](https://bridge.blockscape.network/).

##
