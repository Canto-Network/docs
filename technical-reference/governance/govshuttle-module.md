# GovShuttle Module

The [`x/govshuttle`](https://github.com/Canto-Network/Canto/tree/main/x/govshuttle) module is a custom-built governance module that enables network-level governance over applications deployed to the Canto EVM.

At the functional level, the module passes information from Canto governance proposals on the Cosmos SDK layer to an oracle address (the "Port") on the Canto EVM, which can be read and implemented by Free Public Infrastructure smart contracts.

{% hint style="info" %}
Port Address (mainnet): 0x648a5Aa0C4FbF2C1CF5a3B432c2766EeaF8E402d
{% endhint %}

## Overview

On initialization, the `x/govshuttle` keeper checks to see if the Port contract is deployed to the Canto EVM. If not, the keeper uses the `DeployMapContract` function to deploy the Port.

```go
if nonce == 0 {
	*k.mapContractAddr, err = k.DeployMapContract(ctx, lm)
	if err != nil {
		return nil, err
	}
	return lm, nil
}
```

Deployment of this contract utilizes the `Create` function in Geth. The resulting contract is wholly owned by the module itself and _cannot_ be modified by any other account.&#x20;

After deployment of the Port, governance proposals of predefined types are automatically routed to `x/govshuttle`. Upon passing of a proposal, the module's keeper calls the `AppendProposal`  function, which uses Geth’s `Call` function to add the proposal’s data to the Port contract's storage.

```go
func handleLendingMarketProposal(ctx sdk.Context, k *keeper.Keeper, p *types.LendingMarketProposal) error {
	err := p.ValidateBasic()
	if err != nil {
		return err
	}
	_, err = k.AppendProposal(ctx, p) 
	if err != nil {
		return err
	}
	return nil
}
```

The proposal types routed to the module are [specified in the Canto binary](https://github.com/Canto-Network/Canto/blob/main/x/govshuttle/proposal\_handler.go#L12). At the time of writing,  `LendingMarketProposal` and `TreasuryProposal` proposals are routed to the module.

### Reading Shuttled Data in EVM

Reading a proposal written to the Port is as simple as querying the contract using the `QueryProp` view. This function takes in a `propId` (proposal ID) as an argument and returns the corresponding proposal’s data.

#### Example (ethers.js)

<pre class="language-javascript"><code class="lang-javascript"><strong>const Port = new ethers.Contract(0x648a5Aa0C4FbF2C1CF5a3B432c2766EeaF8E402d, ABI, provider)
</strong><strong>const proposalData = await Port.QueryProp(50)
</strong>console.log(proposalData) // returns...

/*
[
  50n,
  'Governance Proposal to Update Comp Speeds in Canto Lending Market',
  'If successful, this governance proposal will update comp speeds in the Canto Lending Market for Canto/Note, Canto/Atom, Canto/Eth, Note/USDC, Note/USDT, USDC, and USDT as detailed in https://canto.mirror.xyz/-nSUAL6_YXbXxrQoZiAmlwDPi4s_RsJrX0H6_1iUzEM',
  Result(1) [ '0x5E23dC409Fc2F832f83CEc191E245A191a4bCc5C' ],
  Result(1) [ 0n ],
  Result(1) [ '_setCompSpeeds(address[],uint256[],uint256[])' ],
  Result(1) [
    '0x0000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000016000000000000000000000000000000000000000000000000000000000000002600000000000000000000000000000000000000000000000000000000000000007000000000000000000000000de59f060d7ee2b612e7360e6c1b97c4d8289ca2e0000000000000000000000006b46ba92d7e94ffa658698764f5b8dfd537315a9000000000000000000000000d6a97e43fc885a83e97d599796458a331e580800000000000000000000000000f0cd6b5ce8a01d1b81f1d8b76643866c5816b49f000000000000000000000000c0d6574b2fe71eed8cd305df0da2323237322557000000000000000000000000b49a395b39a0b410675406bee7bd06330cb503e30000000000000000000000003c96dcfd875253a37acb3d2b102b6f328349b16b00000000000000000000000000000000000000000000000000000000000000070000000000000000000000000000000000000000000000000429d069189e00000000000000000000000000000000000000000000000000000429d069189e000000000000000000000000000000000000000000000000000017508f1956a8000000000000000000000000000000000000000000000000000017508f1956a800000000000000000000000000000000000000000000000000006ccd46763f1000000000000000000000000000000000000000000000000000006ccd46763f100000000000000000000000000000000000000000000000000000f8b0a10e4700000000000000000000000000000000000000000000000000000000000000000000070000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000'
  ]
*/
</code></pre>

The `x/govshuttle` module can be generalized to pass any form of information between Canto layers, including additional proposal types, allowing for a highly flexible, application-agnostic interface.
