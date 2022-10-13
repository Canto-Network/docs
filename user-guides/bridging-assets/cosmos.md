# Cosmos Hub -> Canto

At present, the Cosmos Hub -> Canto bridge only supports $ATOM by means of IBC transfer.

{% hint style="danger" %}
**Do not attempt to transfer $ATOM to the Canto address in your Keplr wallet. Follow the instructions below.**
{% endhint %}

## Cosmos Hub -> Canto <a href="#cosmos-hub-canto" id="cosmos-hub-canto"></a>

To bridge $ATOM from the Cosmos Hub network to the Canto Network, follow these steps:

1. Navigate to [**bridge.canto.io**](https://bridge.canto.io) **** and connect your MetaMask wallet, making sure you are on the Ethereum network.
2. **Before bridging assets to Canto, you will be asked to generate a Canto public key, which is associated with your Ethereum address. You will only need to do this once per wallet. This is so you can sign Cosmos transactions from that Ethereum address. There is no interaction with private keys.**&#x20;

![](<../../.gitbook/assets/image (31).png>)

3\. Add the Canto network to your Keplr wallet.

![](<../../.gitbook/assets/image (26).png>)

4\. Copy your Canto native address.

![](<../../.gitbook/assets/image (8).png>)

5\. Make sure "Show Advanced IBC Transfers" option is toggled on in Keplr wallet settings.

![](<../../.gitbook/assets/Screen Shot 2022-08-19 at 1.34.54 PM.png>)

6\. In Keplr, switch to the Cosmos Hub. Then click IBC Transfer.

![](<../../.gitbook/assets/image (3).png>)



7\. Select “Canto Mainnet” as the destination chain. If bridging for the first time, add Canto by clicking "New IBC Transfer Channel", selecting Canto Mainnet and entering `channel-358.`

![](<../../.gitbook/assets/image (19).png>)![](<../../.gitbook/assets/image (2).png>)

8\. Enter the amount you want to transfer and complete the transaction. Your $ATOM should arrive after a few minutes.

![](../../.gitbook/assets/image.png)

Assets bridged to Canto will arrive on the native Canto blockchain. If you want to use the Canto Lending Market, Canto DEX, and other DApps, you must [convert your assets to the Canto EVM](../converting-assets.md).

