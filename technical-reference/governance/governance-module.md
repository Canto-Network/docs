# Governance Module

Canto's on-chain governance system leverages the Cosmos SDK `x/gov` module. In this system, $CANTO stakers can vote on proposals with votes weighted proportionally to their stake.

The module supports the following basic features:

* **Proposal submission:** Users submit governance proposals with a deposit. Once the minimum deposit is reached, the proposal enters voting.
* **Voting:** Participants can vote on proposals that reached MinDeposit.
* **Inheritance and penalties:** Delegators inherit their validator's vote if they don't vote themselves.
* **Claiming deposit:** Users that deposited on proposals can recover their deposits if the proposal was accepted OR if the proposal never entered the voting period.

## Proposal submission <a href="#proposal-submission" id="proposal-submission"></a>

Every account can submit proposals by sending a `MsgSubmitProposal` transaction through a [Canto node](../../canto-node/validators/). Once a proposal is submitted, it is identified by its unique `proposalID`.

### Proposal Messages <a href="#proposal-messages" id="proposal-messages"></a>

A proposal includes an `sdk.Msg` array, which is executed automatically if the proposal passes. Messages are executed by the governance `ModuleAccount` itself. Modules such as `x/upgrade`, that want to allow certain messages to be executed by governance only should add a whitelist within the respective msg server, granting the governance module the right to execute the message once a quorum has been reached. The governance module uses the `MsgServiceRouter` to check that these messages are correctly constructed and have a respective path to execute on but does not perform a full validity check.

## Deposit <a href="#deposit" id="deposit"></a>

To prevent spam, proposals must be submitted with a deposit in the cryptocurrency defined by the `MinDeposit` param.

When a proposal is submitted, it has to be accompanied with a deposit that must be strictly positive, but can be inferior to `MinDeposit`. The submitter doesn't need to pay for the entire deposit on their own. The newly created proposal is stored in an _inactive proposal queue_ and stays there until its deposit passes the `MinDeposit`. Other token holders can increase the proposal's deposit by sending a `Deposit` transaction. If a proposal doesn't pass the `MinDeposit` before the deposit end time (the time when deposits are no longer accepted), the proposal will be destroyed: the proposal will be removed from state and the deposit will be burned (see x/gov `EndBlocker`). When a proposal deposit passes the `MinDeposit` threshold (even during the proposal submission) before the deposit end time, the proposal will be moved into the _active proposal queue_ and the voting period will begin.

The deposit is kept in escrow and held by the governance `ModuleAccount` until the proposal is finalized (passed or rejected).

### Deposit refund and burn <a href="#deposit-refund-and-burn" id="deposit-refund-and-burn"></a>

When a proposal is finalized, the coins from the deposit are either refunded or burned according to the final tally of the proposal:

* If the proposal is approved or rejected but _not_ vetoed, each deposit will be automatically refunded to its respective depositor (transferred from the governance `ModuleAccount`).
* When the proposal is vetoed with greater than 33.4% of the votes, deposits will be burned from the governance `ModuleAccount` and the proposal information along with its deposit information will be removed from state.
* All refunded or burned deposits are removed from the state. Events are issued when burning or refunding a deposit.

## Voting <a href="#vote" id="vote"></a>

### Participants <a href="#participants" id="participants"></a>

_Participants_ are users that have the right to vote on proposals. On Canto, participants are bonded $CANTO holders. Unbonded $CANTO holders and other users do not get the right to participate in governance. However, they can submit and deposit on proposals.

Note that some _participants_ can be forbidden to vote on a proposal under a certain validator if:

* The _participant_ bonded or unbonded $CANTO to said validator after the proposal entered voting period.
* The _participant_ became a validator after the proposal entered voting period.

This does not prevent _participants_ from voting with $CANTO bonded to other validators. For example, if a _participant_ bonds some $CANTO to Validator A before a proposal entered voting period, and bonds more $CANTO to Validator B after a proposal entered voting period, only the vote bonded to Validator B will be forbidden.

### Voting period <a href="#voting-period" id="voting-period"></a>

Once a proposal reaches `MinDeposit`, it immediately enters `Voting period`. We define `Voting period` as the interval between the moment the vote opens and the moment the vote closes. `Voting period` should always be shorter than `Unbonding period` to prevent double voting. The initial value of `Voting period` is 1 hour.

### Option set <a href="#option-set" id="option-set"></a>

The option set of a proposal refers to the set of choices participants can choose from when casting their votes.

The initial option set includes the following options:

* `Yes`
* `No`
* `NoWithVeto`
* `Abstain`

`NoWithVeto` counts as `No` but also adds a `Veto` vote. The `Abstain` option allows voters to signal that they do not intend to vote for or against the proposal but will accept the result of the vote.

### Quorum <a href="#quorum" id="quorum"></a>

Quorum is defined as the minimum percentage of voting power that needs to be cast on a proposal for the result to be valid. At launch, quorum is set to 33.4%.

### Threshold <a href="#threshold" id="threshold"></a>

Threshold is the minimum proportion of `Yes` votes to total votes (excluding `Abstain` votes) required for a proposal to be accepted.

Initially, the threshold is set at 50%. A possibility to veto exists if more than 33.4% of all votes are `NoWithVeto` votes. Both of these values are derived from the `TallyParams` on-chain parameter, which is modifiable by governance. This means that proposals are accepted if:

* There exist bonded tokens.
* Quorum has been achieved.
* The proportion of `Abstain` votes is inferior to 100%, i.e. at least one `Yes`, `No`, or `NoWithVeto` vote was submitted one.
* The proportion of `NoWithVeto` votes to total votes (including`Abstain` votes) is inferior to 33.4%.
* The threshold is met.

### Inheritance <a href="#inheritance" id="inheritance"></a>

If a delegator does not vote, they will inherit their validator's vote.

* If a delegator votes before their validator, they will not inherit their validator's vote.
* If a delegator votes after thei validator, they will override their validator's vote with their own. If the proposal is urgent, it is possible that the vote will close before delegators have a chance to react and override their validator's vote. This is not a problem, as proposals require more than 66.6% of the total voting power to pass before the end of the voting period. Because as little as 33.4% + 1 validation power could collude to censor transactions, non-collusion is already assumed for ranges exceeding this threshold.

### Validator’s punishment for non-voting <a href="#validator-s-punishment-for-non-voting" id="validator-s-punishment-for-non-voting"></a>

At present, validators are not punished for failing to vote.

### Governance address <a href="#governance-address" id="governance-address"></a>

Later, the Canto network may introduce permissioned keys that can only sign txs from certain modules. For the MVP, the `Governance address` will be the main validator address generated at account creation. This address corresponds to a different PrivKey than the Tendermint PrivKey which is responsible for signing consensus messages. Validators thus do not have to sign governance transactions with the sensitive Tendermint PrivKey.

## Software Upgrades <a href="#software-upgrade" id="software-upgrade"></a>

If proposals are of type `SoftwareUpgradeProposal`, then nodes need to upgrade their software to the new version that was voted for. This process is divided into two steps, signal and switch.

### Signal <a href="#signal" id="signal"></a>

After a `SoftwareUpgradeProposal` is accepted, validators are expected to download and install the new version of the software while continuing to run the previous version. Once a validator has downloaded and installed the upgrade, it will start signaling to the network that it is ready to switch by including the proposal's `proposalID` in its _precommits_.

Note: There is only one signal slot per _precommit_. If several `SoftwareUpgradeProposals` are accepted in a short timeframe, a pipeline will form and they will be implemented one after the other in the order that they were accepted.

### Switch <a href="#switch" id="switch"></a>

Once a block contains more than 66.6% _precommits_ where a common `SoftwareUpgradeProposal` is signaled, all the nodes (including validator nodes, non-validating full nodes and light-nodes) are expected to switch to the new version of the software.

More information can be found in the [Cosmos SDK documentation.](https://docs.cosmos.network/master/modules/gov/)
