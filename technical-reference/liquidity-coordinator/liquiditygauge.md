# LiquidityGauge

When an LP token is whitelisted on `LendingLedger`, a `LiquidityGauge` wrapper is automatically created. This simple wrapper calls `sync_ledger` in the `_afterTokenTransfer` hook to ensure eligible LP positions are continuously tracked by the protocol.

### Depositing <a href="#claiming" id="claiming"></a>

To deposit LP tokens into a wrapper, call the `depositUnderlying(uint256 _amount)` method. The wrapper must be approved to spend the underlying token.

**ethers.js**

```
await LiquidityGauge.depositUnderlying(10000000000000000000) // Deposit 10 LP tokens
```

**foundry**

```
cast send --ledger 0x... "depositUnderlying(uint256)" 10000000000000000000
```

### Withdrawing <a href="#claiming" id="claiming"></a>

To withdraw LP tokens from a wrapper, call the `withdrawUnderlying(uint256 _amount)` method.

**ethers.js**

```
await LiquidityGauge.withdrawUnderlying(10000000000000000000) // Withdraw 10 LP tokens
```

**foundry**

```
cast send --ledger 0x... "withdrawUnderlying(uint256)" 10000000000000000000
```
