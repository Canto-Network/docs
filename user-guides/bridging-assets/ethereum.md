# Ethereum <-> Canto

At present, the Ethereum <-> Canto bridge supports ETH, USDC, and USDT transfers.

## Ethereum -> Canto

To bridge assets from the Ethereum network to the Canto network, follow these steps:

1. Navigate to [**bridge.canto.io**](https://bridge.canto.io) **** and connect your MetaMask wallet, making sure you are on the Ethereum network.
2. **Before bridging assets to Canto, you will be asked to generate a Canto public key, which is associated with your Ethereum address. You will only need to do this once per wallet. This is so you can sign Canto transactions from that Ethereum address. There is no interaction with private keys.**&#x20;

![](<../../.gitbook/assets/image (30).png>)

3\. Select the token you would like to bridge and input the quantity. Quantities less than 1 must include a 0 in the ones place value (e.g. `0.99`).

4\. Confirm the approval transaction in your wallet to approve transfer of the asset to the bridge.

5\. Sign the message in your wallet to confirm the transfer.

![](<../../.gitbook/assets/Screen Shot 2022-08-11 at 8.45.08 PM.png>)

Assets bridged to Canto will arrive on the native Canto blockchain 96 ETH blocks (20 minutes) after the Ethereum transfer is confirmed. If you want to use the Canto Lending Market, Canto DEX, and other DApps, you must [convert your assets to the Canto EVM](../converting-assets.md).

## Canto -> Ethereum

Bridging from Canto to Ethereum is possible via Gravity Bridge. To bridge assets on Canto back to Ethereum, you must have:

* An IBC wallet (such as Keplr Wallet)
* An Ethereum wallet such as MetaMask

You can only bridge assets on the native Canto blockchain back to Ethereum. If your assets are on the Canto EVM, you must [convert them](https://app.gitbook.com/o/UXyuOCE75UxaFcpPBpJt/s/K4o1JDSaOKhM0C8tixAv/\~/changes/K5AJJ9jKUxXrZzGka0gq/user-guides/converting-assets) first.

Once you are ready to bridge from Canto to Ethereum, follow these steps:

1. Navigate to [**bridge.canto.io**](https://bridge.canto.io) **** and connect your MetaMask wallet, making sure you are on the Canto network.
2. Select Canto as the _from_ network and Gravity Bridge as the _to_ network.

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.44.23 AM.png>)

2\. Select the token you wish to bridge and enter an amount.

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.46.51 AM.png>)

3\. Open your Keplr wallet and change the network to Gravity Bridge. Copy your Gravity Bridge address and paste it into the bridge interface:

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.51.28 AM.png>)

4\. Click `send token` and sign the transaction in MetaMask. After a few minutes, you should see the tokens in your Keplr wallet at the address you provided.

<img src="../../.gitbook/assets/Screen Shot 2022-08-17 at 4.09.04 AM.png" alt="" data-size="original">



5\. Once the tokens are in your Keplr wallet, bridge from Gravity Bridge to Ethereum using the [Gravity Bridge portal](https://bridge.blockscape.network/).

{% hint style="info" %}
To bridge assets from Gravity Bridge to Ethereum, you no longer need $GRAV tokens to pay gas. Fees are paid in whatever token you are bridging. Select your fee option in the Gravity Bridge portal carefully, the 24 hour fee level for example will take about 24 hours.
{% endhint %}

![](<../../.gitbook/assets/Screen Shot 2022-08-17 at 3.59.58 AM.png>)

##
