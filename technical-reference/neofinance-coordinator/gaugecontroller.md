# GaugeController

Lockers vote on gauges using the [`GaugeController`](https://oklink.com/canto/address/0x46970b45d114420A71A3d76AA6c398173118C2b8) contract. Gauges represent LP tokens on the Canto DEX and/or cNOTE deposits on third-party lending markets.&#x20;

Voting takes place during one week epochs.

### Voting <a href="#voting" id="voting"></a>

To vote for a gauge, call the `vote_for_gauge_weights(address _gauge_addr, uint256 _user_weight)` method. The `_gauge_addr` parameter is the address of a whitelisted gauge and `_user_weight` is the voting weight in bps (basis points).

**ethers.js**

```
await GaugeController.vote_for_gauge_weights(0x..., 10000) // 10,000 bps = 100%
```

**foundry**

```
cast send --ledger 0x... "vote_for_gauge_weights(address,uint256)" 0x... 10000
```

### Removing/Changing Votes <a href="#removingchanging-votes" id="removingchanging-votes"></a>

To remove or change votes cast in the current epoch, call the `vote_for_gauge_weights(address _gauge_addr, uint256 _user_weight)` method specifying a new weight (e.g. 0 bps).
