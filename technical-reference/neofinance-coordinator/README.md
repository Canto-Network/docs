# Neofinance Coordinator

Neofinance Coordinator is a minimal protocol which incentivizes supplying $cNOTE on third-party lending markets on the Canto blockchain. Within the protocol, $CANTO is sourced from chain governance and distributed according to a vote locking mechanism.

## Architecture <a href="#architecture" id="architecture"></a>

Neofinance Coordinator consists of three smart contracts:

### [`VotingEscrow`](https://tster.github.io/canto-verwa-docs/docs/VotingEscrow.md) <a href="#votingescrow" id="votingescrow"></a>

Allows users (typically protocols) to lock $CANTO for a fixed 5-year period. In exchange for locking, users receive $veCANTO which provides gauge voting rights.

### [`GaugeController`](https://tster.github.io/canto-verwa-docs/docs/GaugeController.md) <a href="#gaugecontroller" id="gaugecontroller"></a>

Allows lockers to vote on gauges, which are liquidity pairs on Canto’s third-party lending markets. Voting takes place during one week epochs, after which $CANTO incentives are allocated to pairs proportionally to votes.

### [`LendingLedger`](https://tster.github.io/canto-verwa-docs/docs/LendingLedger.md) <a href="#lendingledger" id="lendingledger"></a>

Holds incentives received from Canto governance and continuously tracks balances on whitelisted third-party lending markets, allowing liquidity providers to claim incentives proportionally to their balance at a given epoch.
