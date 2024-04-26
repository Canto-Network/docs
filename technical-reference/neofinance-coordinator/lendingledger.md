# LendingLedger

LP tokens on the Canto DEX and cNOTE deposits on third-party lending markets are continuously tracked by [`LendingLedger`](https://oklink.com/canto/address/0x85156B45B3C0F40f724637ebfEB035aFB29BD083).

* In the case of cNOTE deposits, third-party lending markets call `sync_ledger` every time a user deposits or withdraws cNOTE.
* In the case of LP tokens, tokens should be wrapped in a [`LiquidityGauge`](https://docs.canto.io/technical-reference/neofinance-coordinator/liquiditygauge), which calls `sync_ledger` in the `_afterTokenTransfer` hook.

Additionally, users claim incentives from `LendingLedger`.

### Syncing Ledger <a href="#syncing-ledger" id="syncing-ledger"></a>

To sync the ledger, call the `sync_ledger(address _lender, int256 _delta)` method. The address is that of the user (liquidity provider) and the int256 is the amount of tokens deposited/received (positive) or withdrawn/sent (negative) with 18 decimal places of precision.

**Important:** The `sync_ledger` method reverts if the caller is not a whitelisted lending market or `LiquidityGauge`. As a result, lending markets integrating Liquidity Coordinator should wrap this method in a try-catch block to ensure liquidity providers can still deposit/withdraw if their market is removed from the whitelist.

**ethers.js**

```
await LendingLedger.sync_ledger(0x..., 10000000000000000000) // 10 cNOTE deposit
```

**foundry**

```
cast send --ledger 0x... "sync_ledger(address,int256)" 0x... 10000000000000000000
```

### Claiming <a href="#claiming" id="claiming"></a>

To claim incentives, call the `claim(address _market)` method. Previously, incentives could only be claimed for past epochs; however, incentives are now claimed for all epochs including partial incentives for the current epoch.

**ethers.js**

```
await LendingLedger.claim(0x...) // Claim all incentives
```

**foundry**

```
cast send --ledger 0x... "claim(address)" 0x...
```

### Secondary Rewards

Third-party protocols can use `LendingLedger`'s deposit tracking to implement secondary token rewards, e.g. lending market governance tokens.

Within the`userInfo` mapping, lending market addresses map to user addresses, which in turn map to `UserInfo` structs. `UserInfo.secRewardDebt` is the amount of secondary rewards the user is entitled to.
