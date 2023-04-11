# GovShuttle Module

The GovShuttle module is a custom-built governance module that enables network-level governance over applications deployed to the EVM. At the functional level, the module passes information from Cosmos SDK governance proposals to an oracle address on the EVM, which can be read and implemented by Free Public Infrastructure DApps.

## How GovShuttle Works

The GovShuttle module is a Cosmos SDK module that unifies network and DApp governance. The module allows stakers of $Canto to create and vote on governance proposals that can be transported to a proposal store contract called the Port on Canto’s EVM. On initialization, GovShuttle’s keeper checks to see if the Port exists. If it hasn’t been deployed, the keeper will use the `DeployMapContract` function to deploy the Port.

```go
if nonce == 0 {
	*k.mapContractAddr, err = k.DeployMapContract(ctx, lm)
	if err != nil {
		return nil, err
	}
	return lm, nil
}
```

This contract is wholly owned by the module itself and _cannot_ be modified by any other account. Deployment of this contract is handled by the GovShuttle’s keeper and at its core utilizes the `Create` function in Geth.

After deployment of the Port, users have the option to submit special proposal types that are routed to the GovShuttle. On passing, the GovShuttle’s keeper calls a function called `AppendProposal` , which uses Geth’s `Call` function to add the proposal’s data to the Port. The Port can then propagate these proposals to DApps on the EVM.

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

### Reading Shuttled Data in EVM

Reading a proposal written to the Port is as simple as querying the contract using the function `QueryProp` . This function takes in a proposal id as an argument and returns the corresponding proposal’s data. In doing so, contracts on Canto’s EVM can now read data from proposals passed from the Cosmos SDK. This allows any application to become a Free Public Good by integrating its governance directly into network governance with very little modification. Technically speaking this system can be generalized for any form of cross runtime information passing including additional proposal types allowing for a highly flexible, application-agnostic interface.

**Below is a visual representation of how this system works:**

![](<../../.gitbook/assets/Blank diagram (1).png>)

By using GovShuttle and generalizing it further for additional data types, Canto stakeholders can govern an arbitrary number of applications on the EVM.
