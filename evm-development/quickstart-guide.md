# Quickstart Guide

Building smart contracts for the Canto EVM is the same as doing so for Ethereum or any other EVM-compatible chain, with the only difference being the network itself.

Smart contracts can be deployed using your Ethereum tooling of choice, including [Hardhat](https://hardhat.org/), [Truffle](https://trufflesuite.com/), [Foundry](https://getfoundry.sh/), [Remix](https://remix.ethereum.org/), and others. To get started, simply configure your environment to use Canto's RPC and chain ID.

### **Mainnet**

**RPC URL**: **** `https://canto.evm.chandrastation.com/`

**Chain ID: 7700**

<details>

<summary><strong>Alternative RPC URLs</strong></summary>

* `https://jsonrpc.canto.nodestake.top/`
* `https://canto.slingshot.finance/`

</details>

### Testnet

**RPC URL**: `https://eth.plexnode.wtf/`

**Chain ID**: 740

## Libraries

When building frontends or other applications that require on-chain data, you'll likely want to use a library to retrieve that data.

Needless to say, you can interact with the Canto EVM using most Ethereum libraries, such as [ethers.js](https://docs.ethers.io/v5/), [web3.js](https://web3js.readthedocs.io/en/v1.8.0/), and [web3.py](https://web3py.readthedocs.io/en/stable/) – just initialize a provider with the Canto RPC using your library of choice. For example:

```javascript
const ethers = require('ethers')

const provider = new ethers.providers.JsonRpcProvider("https://canto.slingshot.finance")

async function printCurrentBlock() {
  console.log(await provider.getBlockNumber())
}

printCurrentBlock()
```

## Beginner's Guide

In case you're new to Solidity development, here are step-by-step instructions on how you can deploy your first contract on Canto using Remix:

### Writing a Smart Contract

The first step in deploying a smart contract on Canto is writing the contract's source code in Solidity. To do this, create a new file in your Remix workspace:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Name the file as desired with the `.sol` extension and begin writing your code. You can also use source code from contracts that are already deployed on Ethereum.

For this example, let's copy and paste the following source code based on the [official Solidity documentation](https://docs.soliditylang.org/en/v0.8.17/introduction-to-smart-contracts.html):

```solidity
pragma solidity 0.8.17;

contract Example {
    uint storedData;
    
    function set(uint x) public {
        storedData = x;
    }
    
    function get() public view returns (uint) {
        return storedData;
    }
}
```

Once your code is ready, hit Ctrl+S to compile your smart contract.

### Deploying a Smart Contract

To deploy your smart contract, start by making sure you have MetaMask installed and [connected to Canto](../user-guides/connecting-to-canto.md). Since this contract is for testing purposes, we'll connect to the Canto testnet.

Returning to Remix, navigate to the deployment tab, which is the fifth icon down on the vertical menu. Click on the environment drop-down box and select _Injected Provider - Metamask_:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

A MetaMask prompt will appear asking you to connect your wallet to Remix. As always, make sure you are comfortable with the permissions that are being requested and click _Connect_.

Once you've connected your wallet, you'll see your account address under _Account_. Make sure this is where you want to deploy your contract from and then hit _Deploy._

{% hint style="info" %}
If your smart contract uses constructor arguments, enter them in the field adjacent to the _Deploy_ button before attempting to deploy your contract.
{% endhint %}

After you hit _Deploy_, a MetaMask prompt will appear with a contract deployment transaction. Confirm the transaction.

As soon as the block is mined, your smart contract will be live on the Canto EVM. You can find the address of your smart contract at the bottom left of the Remix interface under _Deployed Contracts_, or by looking for the recipient of the contract deployment transaction in your wallet or on the block explorer.
