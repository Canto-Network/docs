# Contract Secured Revenue (CSR)

Canto implements a fee split model called Contract Secured Revenue, or CSR, by means of the [`x/CSR`](https://github.com/Canto-Network/Canto/tree/csr/x/csr) module. CSR allows you to claim a percentage of all transaction fees paid by users when interacting with your smart contracts.

CSR was added in the Canto v5.0.0 chain upgrade with an initial fee split of 20%, following a successful [governance proposal](https://canto.io/governance/proposal/41).

## Overview

To earn CSR fees, you must register your contracts with the CSR **Turnstile** smart contract deployed on Canto mainnet at [0xEcf044C5B4b867CFda001101c617eCd347095B44](https://evm.explorer.canto.io/address/0xEcf044C5B4b867CFda001101c617eCd347095B44). The source code for Turnstile can be found [here](https://github.com/Canto-Network/Canto/blob/csr/contracts/turnstile.sol).

Upon registering a contract, a transferrable NFT representing the right to claim that contract's revenue is minted to an address of your choice. Alternatively, you can assign a contract's revenue to an existing CSR NFT.

CSR fees for all registered contracts accrue in the Turnstile contract. To withdraw fees from the Turnstile contract, you must specify the token ID of a CSR NFT you hold.

## Registering a Contract <a href="#registering-a-contract" id="registering-a-contract"></a>

To register a smart contract for CSR, call the `register` method on the [Turnstile contract](https://evm.explorer.canto.io/address/0xEcf044C5B4b867CFda001101c617eCd347095B44) **from the contract you wish to register.**

This method takes one parameter: the `address` to which the CSR NFT should be minted. This can be an address that does not exist (i.e. an address that has never transacted before).

You can register a contract in the constructor or otherwise; however, CSR fees will only begin accruing once the contract is registered.

```solidity
interface Turnstile {
    function register(address) external returns(uint256);
}
    
contract Example {
    Turnstile turnstile = Turnstile(0xabc...);
    
    constructor() {
        //Registers the smart contract with Turnstile
        //Mints the CSR NFT to the contract creator
        turnstile.register(msg.sender);
    }
}
```

The `register` method returns the token ID of the CSR NFT that was minted.

### Assignment <a href="#assignment" id="assignment"></a>

You can register a smart contract for CSR while assigning its fees to an existing CSR NFT by calling the `assign` method on the [Turnstile contract](https://evm.explorer.canto.io/address/0xEcf044C5B4b867CFda001101c617eCd347095B44). This method also takes one parameter: the `uint256` token ID of the CSR NFT to which fees should be assigned.

The same constraints apply:

* You must call this method from the contract you wish to register.
* CSR fees will only begin accruing once the contract is registered.

```solidity
interface Turnstile {
    function assign(uint256) external returns(uint256);
}

contract Example {
    Turnstile turnstile = Turnstile(0xabc...);

    constructor() {
        //Registers the smart contract with Turnstile
        //Assigns this contract's fee revenue to CSR NFT #1
        turnstile.assign(1);
    }
}
```

The `assign` method returns the token ID of the CSR NFT that was passed to it.

## Withdrawing Fees <a href="#withdrawing-fees" id="withdrawing-fees"></a>

You can check the amount of fees that have accrued for a CSR NFT by reading the value stored in the `balances` mapping for the NFT's token ID.

To withdraw CSR fees, call the `withdraw` method on the Turnstile contract **from the address that holds the CSR NFT**. This method takes three parameters: the token ID of the CSR NFT, the address that should receive the fees, and the amount of fees to withdraw.

## Factory Contracts

You can implement the `register` and `assign` methods in factory contracts, such that child contracts are automatically registered for CSR when they are created.
