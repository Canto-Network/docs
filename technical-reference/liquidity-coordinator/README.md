# Liquidity Coordinator

Liquidity Coordinator, formerly Neofinance Coordinator, is a minimal protocol which incentivizes providing liquidity to Canto neofinance primitives.

Rewards are sourced from network governance in the form of CANTO and distributed according to a vote locking mechanism to the following liquidity providers:

* Suppliers of [cNOTE](../../neofinance/overview.md#cnote) on third-party lending markets (such as [Vivacity Finance](https://vivacity.finance/))
* LPs of TOKEN/WCANTO pairs on the [Canto DEX](../../free-public-infrastructure/dex.md)&#x20;

## Architecture <a href="#architecture" id="architecture"></a>

Liquidity Coordinator consists of four smart contracts:

### [`VotingEscrow`](votingescrow.md) <a href="#votingescrow" id="votingescrow"></a>

Allows users (typically protocols) to lock CANTO for a fixed 5-year period. In exchange for locking, users receive veCANTO which provides gauge voting rights.

{% embed url="https://oklink.com/canto/address/0x2fed02d6d50a8786D53F308024400fDAD275F57C" %}
Mainnet deployment
{% endembed %}

### [`GaugeController`](./#gaugecontroller) <a href="#gaugecontroller" id="gaugecontroller"></a>

Allows lockers to vote on gauges, which represent LP tokens on the Canto DEX and/or cNOTE deposits on third-party lending markets. Voting takes place during one week epochs.

Incentives are weighted by gauge types (as determined by governance) and subsequently allocated proportionally to votes.

{% embed url="https://oklink.com/canto/address/0x46970b45d114420A71A3d76AA6c398173118C2b8" %}
Mainnet deployment
{% endembed %}

### [`LendingLedger`](./#lendingledger) <a href="#lendingledger" id="lendingledger"></a>

Holds incentives received from Canto governance and continuously tracks balances of eligible LP tokens and cNOTE deposits, allowing liquidity providers to claim incentives proportionally to their balance at a given epoch.

Additionally, implements a view third-party lending markets can use to distribute secondary token rewards.

{% embed url="https://www.oklink.com/canto/address/0x831f746d3b0137b0f3311013e95842cf60fa44ed" %}
Mainnet deployment
{% endembed %}

### [`LiquidityGauge`](https://docs.canto.io/technical-reference/neofinance-coordinator/liquiditygauge)

Wraps LP tokens 1:1 to ensure balances can be tracked by `LendingLedger`.
