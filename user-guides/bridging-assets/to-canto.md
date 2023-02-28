# Bridging to Canto

You can natively bridge to Canto from Ethereum, Cosmos Hub, or Gravity Bridge. Once you've bridged, you'll be able to [move assets to the Canto EVM](bridge-vs-evm.md) and begin interacting with Canto's Free Public Infrastructure and DApps.

## From Ethereum

At present, the Ethereum <-> Canto bridge supports ETH, USDC, and USDT transfers. To bridge assets from the Ethereum network to the Canto network, follow these steps:

1. Navigate to [**canto.io/bridge**](https://canto.io/bridge) and connect your MetaMask wallet, making sure you are on the Ethereum network.
2. Before bridging to Canto, **generate a Canto public key** by clicking on the red banner at the top of the page and signing the transaction in your wallet.
3. 3\. Select the token you would like to bridge and input the quantity. Quantities less than 1 must include a 0 in the ones place value (e.g. `0.99`).
4. Confirm the approval transaction in your wallet to approve transfer of the asset to the bridge.
5. Sign the message in your wallet to confirm the transfer.

<figure><img src="../../.gitbook/assets/bridge-to-canto-eth-new.JPG" alt=""><figcaption></figcaption></figure>

Assets bridged to Canto will arrive on the native Canto blockchain 96 ETH blocks (20 minutes) after the Ethereum transfer is confirmed. If you want to use the Canto Lending Market, Canto DEX, and other DApps, you must [bridge your assets to the Canto EVM](bridge-vs-evm.md).

## From Cosmos Hub or other IBC enabled chain

{% hint style="danger" %}
**Do not attempt to transfer $ATOM or any other token to the Canto address in your Keplr wallet. Follow the instructions below.**
{% endhint %}

This section covers bridging to Canto using Keplr, while $ATOM from the Cosmos Hub is used as an example this guide will also work for SOMM, GRAV, AKT, OSMO, INJ, CMDX, KAVA, and CRE

{% hint style="danger" %}
**Do not attempt to transfer any token that is not on the above list to Canto via IBC**
{% endhint %}

To bridge $ATOM from the Cosmos Hub network to the Canto Network, follow these steps:

1. Navigate to [**canto.io/bridge**](https://canto.io/bridge) **** and connect your MetaMask wallet, making sure you are on the Ethereum network.
2. Before bridging to Canto, **generate a Canto public key** by clicking on the red banner at the top of the page and signing the transaction in your wallet.
3. In the sidebar, click the `add to keplr` button:

<figure><img src="../../.gitbook/assets/add-to-keplr-new (1).png" alt=""><figcaption></figcaption></figure>

4\. Copy your Canto native address:

<figure><img src="../../.gitbook/assets/canto-native-address-new.png" alt=""><figcaption></figcaption></figure>

5\. Make sure "Show Advanced IBC Transfers" option is toggled on in Keplr wallet settings.

![](<../../.gitbook/assets/Screen Shot 2022-08-19 at 1.34.54 PM.png>)

6\. In Keplr, switch to the Cosmos Hub, or the chain you are trying to bridge from. Then click IBC Transfer.

![](<../../.gitbook/assets/image (13).png>)

7\. Select “Canto Mainnet” as the destination chain. If bridging for the first time, add Canto by clicking "New IBC Transfer Channel", selecting Canto Mainnet. Then enter the correct channel depending on the chain you are bridging from.

| Source Chain   | Channel     |
| -------------- | ----------- |
| Cosmos Hub     | channel-358 |
| Gravity Bridge | channel-88  |
| Kava           | channel-87  |
| Akash          | channel-59  |
| Osmosis        | channel-550 |
| Injective      | channel-99  |
| Comdex         | channel-58  |
| Crescent       | channel-34  |
| Sommelier      | channel-2   |

![](<../../.gitbook/assets/image (19).png>)![](<../../.gitbook/assets/image (2).png>)

8\. Enter the amount you want to transfer and complete the transaction. Your $ATOM should arrive after a few minutes.

![](<../../.gitbook/assets/image (4).png>)

Assets bridged to Canto will arrive on the Canto Bridge blockchain. If you want to use the Canto Lending Market, Canto DEX, and other DApps, you must [bridge your assets to the Canto EVM](bridge-vs-evm.md).
