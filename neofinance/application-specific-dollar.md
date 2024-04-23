# Application Specific Dollar

Application Specific Dollar (asD) is a Canto-native protocol that allows teams to earn yield on user deposits by deploying white-label stablecoins backed by [NOTE](https://docs.canto.io/free-public-infrastructure-fpi/note). **With asD V2, Application Specific Dollars can be minted from and bridged to other LayerZero-enabled networks.**

Anyone can permissionlessly deploy an asD token. Likewise, anyone can permissionlessly mint an asD token by depositing NOTE. In turn, the asD smart contract deposits NOTE into the Canto Lending Market, with lending yield claimable only by the asD token's deployer.

asD tokens are always backed 1:1 by NOTE.

## asD V2

asD V2 is the second iteration of Application Specific Dollar, utilizing LayerZero's Omnichain Fungible Token (OFT) standard to enable the bridging of asD tokens across supported networks.

The [`asdOFT` ](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/asdOFT.sol)contract is a standard contract for all asD tokens. When deploying this contract, the token deployer can choose an arbitrary name and symbol for their asD token.

### Helper contracts

While asD tokens are native to Canto and can only be minted in exchange for NOTE, the [`asdRouter` ](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/asdRouter.sol)helper contract enables asD tokens to be minted from other chains with USDC deposits. This contract:

1. Wraps bridged USDC as asdUSDC
2. Swaps asdUSDC for NOTE on Ambient
3. Mints the specified asD token on Canto
4. Sends the asD token to the destination chain and address

The [`asdUSDC` ](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/asdUSDC.sol)wrapper contract is used to wrap whitelisted representations of USDC into a single Canto-native token, which has deep swap liquidity with NOTE. This enables compatibility with various representations of USDC, such as USDC.e.

## Technical Reference

{% content-ref url="../technical-reference/application-specific-dollar/" %}
[application-specific-dollar](../technical-reference/application-specific-dollar/)
{% endcontent-ref %}
