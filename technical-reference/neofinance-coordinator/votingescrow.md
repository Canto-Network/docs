# VotingEscrow

Users create and control locks on the [`VotingEscrow`](https://tuber.build/address/0x2fed02d6d50a8786D53F308024400fDAD275F57C) contract. A user may only have one lock at any given time. Adding to a lock resets the 5-year lock period.

The code samples below demonstrate how to manage locks using ethers.js or foundry. You can also manage locks using a block explorer like [tuber.build](https://tster.github.io/canto-verwa-docs/tuber.build).

### Creating a Lock <a href="#creating-a-lock" id="creating-a-lock"></a>

To create a lock, call the `createLock(uint256 _value)` payable method. The call value and `_value` parameter must match.

**ethers.js**

```
amount = ethers.utils.parseEther("100") // 100 CANTO
await VotingEscrow.createLock(amount, { value: amount })
```

**foundry**

```
cast send --ledger 0x... "createLock(uint256)" 100 --value 100ether
```

#### Adding to a Lock <a href="#adding-to-a-lock" id="adding-to-a-lock"></a>

To add to your existing lock, call the `increaseAmount(uint256 _value)` payable method. The call value and `_value` parameter must match.

**ethers.js**

```
amount = ethers.utils.parseEther("100") // 100 CANTO
await VotingEscrow.increaseAmount(amount, { value: amount })
```

**foundry**

```
cast send --ledger 0x... "increaseAmount(uint256)" 100 --value 100ether
```

### Reading Voting Power <a href="#reading-voting-power" id="reading-voting-power"></a>

To read voting power, call the `balanceOf(address _owner)` view.

**ethers.js**

```
const votingPower = await VotingEscrow.balanceOf("0x...")
```

**foundry**

```
cast call 0x... "balanceOf(address)" 0x...
```

### Withdrawing <a href="#withdrawing" id="withdrawing"></a>

To withdraw a completed lock, call the `withdraw()` method.

**ethers.js**

```
await VotingEscrow.withdraw()
```

**foundry**

```
cast send --ledger 0x... "withdaw()"
```
