# Neofinance Coordinator

{% hint style="info" %}
This protocol does not have a user interface. To be eligible for and claim incentives, supply cNOTE to whitelisted third-party lending markets such as [Vivacity Finance](https://vivacity.finance/).
{% endhint %}

Neofinance Coordinator is a minimal protocol which incentivizes supplying cNOTE on third-party lending markets on the Canto blockchain. Within the protocol, CANTO is sourced from chain governance and distributed according to a vote locking mechanism.

## Architecture <a href="#architecture" id="architecture"></a>

Neofinance Coordinator consists of three smart contracts:

### [`VotingEscrow`](votingescrow.md) <a href="#votingescrow" id="votingescrow"></a>

Allows users (typically protocols) to lock CANTO for a fixed 5-year period. In exchange for locking, users receive veCANTO which provides gauge voting rights.

{% embed url="https://oklink.com/canto/address/0x2fed02d6d50a8786D53F308024400fDAD275F57C" %}
Mainnet deployment
{% endembed %}

### [`GaugeController`](./#gaugecontroller) <a href="#gaugecontroller" id="gaugecontroller"></a>

Allows lockers to vote on gauges, which are liquidity pairs on Canto’s third-party lending markets. Voting takes place during one week epochs, after which CANTO incentives are allocated to pairs proportionally to votes.

{% embed url="https://oklink.com/canto/address/0x46970b45d114420A71A3d76AA6c398173118C2b8" %}
Mainnet deployment
{% endembed %}

### [`LendingLedger`](./#lendingledger) <a href="#lendingledger" id="lendingledger"></a>

Holds incentives received from Canto governance and continuously tracks balances on whitelisted third-party lending markets, allowing liquidity providers to claim incentives proportionally to their balance at a given epoch.

Additionally, implements a view third-party lending markets can use to distribute secondary token rewards.

{% embed url="https://www.oklink.com/canto/address/0x831f746d3b0137b0f3311013e95842cf60fa44ed" %}
Mainnet deployment
{% endembed %}
