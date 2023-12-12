# Getting Started

Third-party lending markets can integrate Neofinance Coordinator to incentivize supplying $cNOTE. However, lending markets must meet certain requirements before they can be whitelisted for a gauge.

### Requirements <a href="#requirements" id="requirements"></a>

Only $cNOTE markets are eligible for neofinance incentives.

The basic requirement for a $cNOTE market integrating Neofinance Coordinator is that it _MUST_ call `sync_ledger(address _lender, int256 _delta)` on the [`LendingLedger`](https://tster.github.io/canto-verwa-docs/LendingLedger.md) every time a user deposits or withdraws $cNOTE. This enables Neofinance Coordinator to continuously track lending balances and allocate incentives accordingly.

Additionally, the relevant smart contracts for the lending market _MUST_ be verified on a Canto block explorer such as [tuber.build](https://tuber.build/).

There are no architectural constraints on lending markets integrating Neofinance Coordinator (such as whether or not they make use of a debt token) so long as the `sync_ledger` method is explicitly used to track only $cNOTE positions.

### Other Recommendations <a href="#other-recommendations" id="other-recommendations"></a>

Since Neofinance Coordinator itself does not have a user interface, lending protocols should implement a claiming interface where liquidity providers can [claim veRWA incentives](https://tster.github.io/canto-verwa-docs/LendingLedger.md).
