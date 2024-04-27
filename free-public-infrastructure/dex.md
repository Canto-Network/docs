# Canto DEX

In order to prevent the possibility of a predatory evolution toward rent-seeking behaviors, Canto’s decentralized exchange protocol:

* Cannot be upgraded
* Has no official interface
* Runs in perpetuity without the ability to implement fees

At launch, users can interact with the DEX contracts through [Slingshot](https://app.slingshot.finance/), a DEX aggregator platform.

## **Trading on Canto DEX**

Like other DEXes, Canto uses an automated market maker (AMM) to price assets. The AMM derives liquidity for trading pairs from user-supplied pools of assets called liquidity pools.&#x20;

At launch, Canto supports two types of liquidity pools:&#x20;

* Full range liquidity pools using a `xy=k` formula (constant product)
* Concentrated liquidity pools using a `yx^3 + xy^3 = k` formula, to deepen liquidity for stablecoins and other units of account such as Note

## **Providing Liquidity**

In order to participate in Canto liquidity mining, users are able to provide liquidity to the Canto DEX at [canto.io/lp](https://canto.io/lp).&#x20;

Users providing liquidity receive LP tokens that can be supplied in the [Canto Lending Market](lending-market.md) to earn incentives.

### **Incentivized Pools**

At present, Canto has 5 incentivized pools:

* USDC/NOTE Concentrated Liquidity Pool (`yx^3 + xy^3 = k`)
* USDT/NOTE Concentrated Liquidity Pool (`yx^3 + xy^3 = k`)
* NOTE/CANTO Full Range Liquidity (\`xy = k\`)
* CANTO/ETH Full Range Liquidity (`xy = k`)
* CANTO/ATOM Full Range Liquidity (`xy = k`)
