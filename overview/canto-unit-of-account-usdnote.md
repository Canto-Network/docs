# Canto Unit of Account ($NOTE)

$NOTE is the unit of account on Canto. $NOTE is an over-collateralized currency with a value perpetually rebalanced toward $1 through an algorithmic interest rate policy. It is:

* Over-collateralized
* Capital efficient
* Fully decentralized
* Automated

$NOTE cannot be created – it must be borrowed from the Accountant, a smart contract that implements the algorithmic interest rate policy, via the [Canto Lending Market](../user-guides/lending-and-borrowing.md) (CLM).

All interest charged by the Accountant is earmarked for funding public goods. It is held in the Community Treasury and controlled by Canto governance.

### Over-collateralization

$NOTE is a fully immutable ERC-20 token backed by collateral lent to the CLM. It can can only be borrowed by users who post select collateral assets. At this time, eligible collateral assets are $USDC and $USDT.

As a result, for every $NOTE in circulation, there is more than 1 USD worth of collateral held by the CLM.

### Capital efficiency

Canto Lending Market achieves superior capital efficiency by allowing stablecoin collateral backing $NOTE to be lent out to other participants. For example, a DeFi participant can lend $USDC to Canto Lending Market and then borrow $NOTE. If the borrow rate for $NOTE is less than the supply rate for $USDC, that DeFi participant will be getting paid to hold $NOTE on Canto.

**Important:** Canto Lending Market will launch with conservative parameters. Over time, governance will be able to raise the capital efficiency of CLM to its full potential.

## Maintaining $NOTE Price Stability

Since $NOTE cannot be created, only borrowed, the Accountant contract utilizes interest rates to manage the circulating supply of $NOTE, and by proxy, its price. The interest rate on $NOTE automatically adjusts up or down every 6 hours based on a TWAP of the market price of $NOTE.

Aiming to provide a public utility, the algorithm responsible for adjusting this interest rate is designed to change the interest rate in order to promote a less volatile value as opposed to maximizing revenue.

If $NOTE is trading under $1, the interest rate is raised to strengthen the incentive for buying $NOTE on secondary markets and lending it to the CLM. If $NOTE is trading over a dollar, the interest rate is lowered to make borrowing $NOTE from the CLM and selling it on secondary markets more attractive.

For launch, each interest epoch will be 6 hours and the rate will adjust by 0.25 (the _adjustor coefficient_) of the difference between the price of $NOTE and $1.00.

**$NOTE Interest Rate Formula:**

$$
newInterestRate = max(0,(1 - price ($NOTE))*Adjuster Coefficient+ priorInterestRate)
$$

**Example:**

* Current Interest Rate: 4%
* $NOTE average price over the last 6 hours: 1.04

$$
newInterestRate = max(0,(1-1.04)*0.25+4\%) = 3\%
$$

If $NOTE is trading above $1, the interest rate is lowered to weaken the $NOTE price. If $NOTE is trading below $1, the interest rate is raised to strengthen the $NOTE price.
