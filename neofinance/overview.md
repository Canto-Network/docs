# Overview

Neofinance envisions a new era of financial efficiencies, unlocked at scale, by deploying offchain assets on protocol rails. The Canto neofinance ecosystem consists of several primitives designed to enable transparent, competitive financial terms.

## RWA Backing for NOTE <a href="#rwas" id="rwas"></a>

Neofinance on Canto revolves around a decentralized unit of account – NOTE – which is backed by Real-World Assets (RWAs). At present, NOTE is backed by Canto-native tokenized treasury bills in the form of USYC, fBILL, and ifBILL:

| Token  | Issuer                                  |
| ------ | --------------------------------------- |
| USYC   | [Hashnote](https://www.hashnote.com/)   |
| fBILL  | [FortunaFi](https://www.fortunafi.com/) |
| ifBILL | [FortunaFi](https://www.fortunafi.com/) |

Purchasers of tokenized treasury bills can supply these assets to the [Canto Lending Market](../free-public-infrastructure/lending-market.md) and borrow NOTE against them, allowing them to achieve superior capital efficiency.

## cNOTE <a href="#cnote" id="cnote"></a>

cNOTE is a tokenized deposit of NOTE, and the primary productive asset in the Canto neofinance ecosystem. Any user can permissionlessly [supply NOTE](../user-guides/lending-and-borrowing.md#supplying-tokens) to the Canto Lending Market to obtain cNOTE.

To ensure deep liquidity, liquidity mining incentives are in place for cNOTE/USDC and NOTE/USDC concentrated trading pools on Ambient Finance, [funded by Canto governance](https://app.canto.io/governance/proposal/121).

## Neofinance Coordinator

Neofinance Coordinator is a novel, Canto-native protocol which incentivizes the lending of cNOTE on downstream lending markets. Incentives are paid in CANTO and funded by network governance.

Current downstream lending markets include [Vivacity Finance](https://vivacity.finance).

For more information, see the [technical reference for Neofinance Coordinator](overview.md#neofinance-coordinator).
