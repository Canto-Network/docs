# Canto Lending Protocol

Canto’s Lending Protocol is deployed on the network's native EVM (Ethermint) and is based on [Compound Protocol](https://compound.finance/) v2. The main differences between Canto Lending and Compound are:

1. There is no Canto Lending specific token. ([Comp is Compound's ERC-20 token](https://github.com/compound-finance/compound-protocol/blob/master/contracts/Governance/Comp.sol).) Instead, Canto’s ERC20 network token is used as the incentive token on Canto Lending. [Comptroller](https://github.com/compound-finance/compound-protocol/blob/master/contracts/ComptrollerG7.sol) smart contract gives out the token rewards. This file is modified to instead give out Canto rewards.
2. Governance on Canto Lending is controlled by Canto network validators rather than the Decentralized Application. Here is how it works:
   * Proposals are initiated on the Network side (Cosmos runtime) and voted on by network Validators as specified in the [SDK governance module](https://docs.cosmos.network/master/modules/gov/). The lending protocol governance has a specified proposal type that is custom to Canto and exactly matches Compound's proposal type.
   * After the proposal is approved, Canto's custom UniGov then sends the proposal type to the EVM module where it can be retrieved by a smart contract call to a specific address (”oracle address”).
   * When the proposal is retrieved, it is stored in the queue and then executed in the same manner as traditional governance outlined in [Compound's Governor Bravo](https://github.com/compound-finance/compound-protocol/blob/master/contracts/Governance/GovernorBravoDelegateG2.sol) after a proposal is approved.
3. Canto Lending Market will allow LP tokens from Canto’s native decentralized exchange to be used as collateral. This collateral will be deposited in a lending market as supply but users will not be allowed to borrow LP tokens.

Since the Canto Lending Protocol is closely based on Compound, you can find more information about its architecture in the [Compound Protocol documentation](https://github.com/compound-finance/compound-protocol/blob/master/README.md).
