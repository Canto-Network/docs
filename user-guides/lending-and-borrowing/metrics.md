# Metrics

Here is a breakdown of the metrics that are displayed in the Canto Lending Market:

1. [Total supply balance](metrics.md#1.-total-supply-balance)
2. [Total borrow balance](metrics.md#2.-total-borrow-balance)
3. [Borrow limit meter](metrics.md#3.-borrow-limit-meter)
4. [Current supplied assets](metrics.md#4.-current-supplied-assets)
5. [Available assets to supply](metrics.md#5.-available-assets-to-supply)
6. [Current borrowed assets](metrics.md#6.-current-borrowed-assets)
7. [Available assets to borrow](metrics.md#7.-available-assets-to-borrow)

**Lending Market Home Page**

![Lending Market Home](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.33.52 PM.png>)

#### 1. Total Supply Balance

![The supply balance is the sum of all assets supplied, converted into $NOTE](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.37.34 PM.png>)

#### 2. Total Borrow Balance

![The borrow balance is the sum of all assets borrowed, converted into $NOTE](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.39.28 PM.png>)

#### 3. Borrow Limit Meter

![](<../../.gitbook/assets/image (15).png>)

The borrow limit meter shows how much of your total borrow limit you are currently using. This limit is calculated by summing all of the supplied tokens, along with their individual collateral factors and converting into $NOTE. Beware of using more than 80% of your total borrow limit since going over may lead to liquidation.

#### 4. Current Supplied Assets

![Supply Table](<../../.gitbook/assets/image (10).png>)

The currently supplying row consists of the asset name, apy (top: supply apy, bottom: distribution apy), balance (top: token supplied, bottom: token supplied balance in $NOTE), and a collateral switch indicating if this asset is currently being used as collateral in the lending market.&#x20;

#### 5. Available Assets to Supply

![Available Supply Table](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.49.50 PM.png>)

The available supply table shows the markets you have not entered yet. Each row contains the asset name, supply APY, total wallet balance, and the collateral switch to indicate if this asset is used as collateral. (An asset that is not currently supplied may have this switch turned on if it is currently being borrowed, since any borrowed asset is automatically used as collateral)

#### 6. Current Borrowed Assets

![Borrowing Table](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.52.54 PM.png>)

The current borrowed assets are shown to see which markets you are currently borrowing from. Each row consists of the asset name, total borrow apy (accrued interest) on the asset, balance in terms of the token denomination and $NOTE, as well as the percentage of your total borrow limit that this market is using.

#### 7. Available Assets to Borrow

![Available Borrow Table](<../../.gitbook/assets/Screen Shot 2022-07-27 at 4.59.22 PM.png>)

The available borrow table displays which assets are currently available to borrow. Each row contains the asset name, borrow APY, user wallet balance, and total liquidity in the pool in terms of $NOTE.&#x20;
