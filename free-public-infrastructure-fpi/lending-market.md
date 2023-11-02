# Canto Lending Market

For the Canto Lending Market (CLM), governance is controlled by Canto stakers. Canto stakers have broad interests in the growth of the ecosystem and fostering the best environment for both developers and DeFi users. As such, they have no incentive to extract rent at the application layer.

As long as liquidity mining incentives are provided to Canto stakers, CLM will always be available.

## Using Canto Lending Market

A user interface for supplying assets to and borrowing assets from the Canto Lending Market is available at [canto.io/lending](https://canto.io/lending), although the underlying contracts can easily be integrated with other frontends and smart contract protocols.

In addition to supporting Canto's [neofinance](../neofinance/overview.md) ecosystem by supplying RWAs and/or cNOTE, users can deposit LP tokens to the lending market to earn incentives.

## Design

CLM is an adaptation of Compound V2. It operates with an AMM that allows users to carry out borrowing and lending transactions using the underlying liquidity pool. This stands in contrast to the alternative of forcing peer-to-peer transactions. Using underlying liquidity in this manner reduces wait times and makes the system self-sustaining.

Governance over the Canto Lending Market by Canto stakers is enabled by the custom [`x/govshuttle`](../technical-reference/governance/govshuttle-module.md) module.
