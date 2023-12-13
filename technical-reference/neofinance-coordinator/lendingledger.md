# LendingLedger

Third-party lending markets call `sync_ledger` on [`LendingLedger`](https://tuber.build/address/0x85156B45B3C0F40f724637ebfEB035aFB29BD083) every time a user deposits or withdraws $cNOTE. This enables Neofinance Coordinator to continuously track lending balances and allocate incentives accordingly.

Additionally, users claim incentives from `LendingLedger`. This should be facilitated by a claiming interface on the lending market.

### Syncing Ledger <a href="#syncing-ledger" id="syncing-ledger"></a>

To sync the ledger, call the `sync_ledger(address _lender, int256 _delta)` method. The address is that of the user (liquidity provider) and the int256 is the amount of $cNOTE deposited (positive) or withdrawn (negative) with 18 decimal places of precision.

**Important:** The `sync_ledger` method reverts if the caller is not a whitelisted lending market. As a result, this method should be wrapped in a try-catch block to ensure liquidity providers can still deposit/withdraw if a market is removed from the whitelist.

**ethers.js**

```
await LendingLedger.sync_ledger(0x..., 10000000000000000000) // 10 $cNOTE deposit
```

**foundry**

```
cast send --ledger 0x... "sync_ledger(address,int256)" 0x... 10000000000000000000
```

### Claiming <a href="#claiming" id="claiming"></a>

To claim incentives, call the `claim(address _market, uint256 _claimFromTimestamp, uint256 _claimUpToTimestamp)` method. The address is that of the market and the two uint256 parameters represent from and to timestamps.

**ethers.js**

```
await LendingLedger.claim(0x..., 0, ethers.constants.MaxUint256) // Claim all incentives
```

**foundry**

```
cast send --ledger 0x... "claim(address,uint256,uint256)" 0x... 0 0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
```
