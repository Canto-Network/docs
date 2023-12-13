# Neofinance Coordinator

{% hint style="info" %}
This protocol does not have a user interface. To be eligible for and claim incentives, supply cNOTE to whitelisted third-party lending markets such as [Vivacity Finance](https://vivacity.finance/).
{% endhint %}

Neofinance Coordinator is a minimal protocol which incentivizes supplying $cNOTE on third-party lending markets on the Canto blockchain. Within the protocol, $CANTO is sourced from chain governance and distributed according to a vote locking mechanism.

## Architecture <a href="#architecture" id="architecture"></a>

Neofinance Coordinator consists of three smart contracts:

### `VotingEscrow` <a href="#votingescrow" id="votingescrow"></a>

Allows users (typically protocols) to lock $CANTO for a fixed 5-year period. In exchange for locking, users receive $veCANTO which provides gauge voting rights.

### `GaugeController` <a href="#gaugecontroller" id="gaugecontroller"></a>

Allows lockers to vote on gauges, which are liquidity pairs on Canto’s third-party lending markets. Voting takes place during one week epochs, after which $CANTO incentives are allocated to pairs proportionally to votes.

### `LendingLedger` <a href="#lendingledger" id="lendingledger"></a>

Holds incentives received from Canto governance and continuously tracks balances on whitelisted third-party lending markets, allowing liquidity providers to claim incentives proportionally to their balance at a given epoch.
