# Slashing

Canto implements the [Cosmos SDK slashing module](https://docs.cosmos.network/master/modules/slashing/), which penalizes validators for downtime and consensus faults in various ways:

* **Slashing:** the validator loses a percentage of their stake
* **Jailing:** the validator is temporarily removed from the validator set
* **Tombstoning (infinite jailing):** the validator is irreversibly removed from the validator set

## Downtime Slashing

Downtime slashing occurs when a validator fails to sign 3000 consecutive blocks, which corresponds to approximately three hours of downtime.

As a penalty for downtime, validators are:

* slashed by **0.75%**
* jailed temporarily

## **Consensus Fault Slashing**

Consensus fault slashing occurs when a validator commits any kind of consensus fault, intentionally or unintentionally.

As a penalty for consensus faults, validators are:

* slashed by **5%**
* **tombstoned** (infinitely jailed)

{% hint style="danger" %}
The most common consensus fault is double signing. Do not attempt to run two validators with the same private key.
{% endhint %}

### **Tombstoning**

Validators who commit a consensus fault are put in a tombstone state, which means they are irreversibly removed from the validator set and cannot rejoin.

In this case, the only resolution for the validator and its delegators is to unbond and delegate anew pursuant to the 21-day unbonding period.

A tombstoned validator operator may relaunch under a different key, but will have to build up their delegations from ~~~~ scratch.

