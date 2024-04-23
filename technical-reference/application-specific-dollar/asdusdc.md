# asdUSDC

[`asdUSDC` ](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/asdUSDC.sol)is a wrapper contract for whitelisted representations of USDC. This enables compatibility with various representations of USDC, such as USDC.e.

Users do not need to interact with the asdUDC contract directly when depositing USDC into an asD token from another chain, as wrapping is performed by the asdRouter.

## Methods

### **`deposit`**

The `deposit(address _usdcVersion, uint256 _amount)` method allows users to wrap whitelisted USDC tokens, minting asdUSDC to their address.

Before calling this method, a user must approve the contract to spend their USDC.

### **`withdraw`**

The `withdraw(address _usdcVersion, uint256 _amount)` method enables users to unwrap asdUSDC, burning tokens to receive the specified USDC token.

### **`recover`**

The `recover(address _usdcVersion)` method is used to recover USDC that was sent to the contract by mistake, minting asdUSDC to the user. Optionally, this asdUSDC can then be withdrawn.
