# asdRouter

[`asdRouter`](https://github.com/Plex-Engineer/ASD-V2/blob/main/contracts/asd/asdRouter.sol) enables asD tokens to be minted from other chains with USDC deposits. Its only public method, `lzCompose`, is called by the LayerZero executor when minting is initiated by a user on another network.

<figure><img src="../../.gitbook/assets/asdFlow.png" alt=""><figcaption></figcaption></figure>

## Minting

To mint asD tokens from another network, a user should first obtain a whitelisted USDC OFT on the origin network (by wrapping or swapping). Then call the [LayerZero `send` method](https://docs.layerzero.network/v2/developers/evm/oft/composing#sending-token) on the OFT passing the following struct (encoded as bytes) in the [`composeMsg` parameter](asdrouter.md#minting):

```solidity
struct OftComposeMessage {
    uint32 _dstLzEid; // destination endpoint id
    address _dstReceiver; // receiver on destination
    address _dstAsdAddress; // asD address on destination
    address _cantoAsdAddress; // asD on Canto (where to mint asD from)
    uint256 _minAmountASD; // minimum amount (slippage for swap)
    address _cantoRefundAddress; // canto refund address
    uint256 _feeForSend; // fee for bridge to destination chain
}
```

## Methods

### `lzCompose`

The `lzCompose(...)` method is called by the LayerZero executor when minting is initiated on another network. The calldata for this method is determined by the `composeMsg` parameter sent on the origin chain when USDC is sent, as described above.

This method:

1. Wraps bridged USDC as asdUSDC
2. Swaps asdUSDC for NOTE on Ambient
3. Mints the specified asD token on Canto
4. Sends the asD token to the destination chain and address
