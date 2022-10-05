# Lending Market Governance

Here is a high level overview of how the Canto Lending Market is governed:&#x20;

1. ​The proposals are initiated on the Network side (Cosmos runtime) and voted on by network Validators as specified in the SDK governance module. Lending protocol governance uses a custom Canto proposal type equivalent to Compound V2's governance proposal type.
2. When a proposal is approved, the GovShuttle module sends the proposal type to the EVM module where it can be retrieved by a smart contract call to a specific oracle address.
3. When the proposal is retrieved, it is stored in the queue and then executed in the same manner as traditional governance on Compound V2, outlined in Compounds Governor Bravo after a proposal is approved.

### Technical Overview & Details

Here is a technical overview of Canto Lending Market governance:

1. User uses cli to submit proposal.`cantod tx unigov submit-proposal “proposal text here” --address="address to map contract"`
2. This submits a proposal using the Governance keeper.
3. Users vote on the proposal.
4. If the proposal passes, the governance module handler sends the proposal to the GovShuttle proposal handler, which triggers the GovShuttle module to call the keeper function AppendLendingMarketProposal located in the proposals.go file.
5. AppendLendingMarketProposal function takes in the LendingMarketProposal from earlier and returns the address at which the Map Contract is deployed.
6. Lending Market can now use the QueryProp method on the map contract to return a proposal struct. Importantly, the lending market can only query proposals that have passed through GovShuttle governance.

Proposals are saved to the EVM as follows:

1. The DeployMapContract packs the arguments contained in the proposal using `ProposalStoreContract.ABI.Pack`&#x20;
2. Then it creates a contract address using `CreateAddress(types.ModuleAddress, nonce)`&#x20;
3. It then creates a byte array with the packed data and passes that into a keeper call to the EVM with `CallEVMWithData(ctx, types.ModuleAddress, nil, data, true)`&#x20;
4. Finally it returns the address where the Map Contract (shown below) with the initial proposal is deployed

```
contract map {
	mapping proposalID : proposal
	
	// only GovShuttle module can call AddProposal method
	function AddProposal(id, proposal) {
		// add new proposal to mapping here
	}
	
	// anyone can call this method 
	function QueryProp(uint id) {
		// return proposal from mapping here using ID
	}
}

```

5\. If a GovShuttle proposal has passed before, add a proposal to the Map Contract by using

```
CallEVM(ctx, 
	contracts.ProposalStoreContract.ABI, 
	types.ModuleAddress, 
	*k.mapContractAddr, 
	true, 
	"AddProposal", 
	sdk.NewIntFromUint64(m.GetPropId()).BigInt(), 
	lm.GetTitle(), 
	lm.GetDescription(), 
	ToAddress(m.GetAccount()), 
	ToBigInt(m.GetValues()), 
	m.GetSignatures(), 
	ToBytes(m.GetCalldatas())
)

```
