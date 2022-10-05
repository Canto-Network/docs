# Lending & Borrowing

The Canto Lending Market allows your to supply and borrow assets, including LP tokens received from the Canto LP Interface. You can access the Canto Lending Market [here](https://lending-canto-testnet.netlify.app/).&#x20;

## Supplying Tokens

To supply an asset, click on a row in the available supply table and the supply modal will open.

![Supply Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.07.25 PM.png>)

In order to supply any asset, it must first be enabled by the market by clicking the enable button. Once approved, the asset is ready to be supplied. You can either manually type the amount of asset you wish to supply, or click the `max` button to supply your entire wallet balance of this asset.&#x20;

![Supply Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.14.25 PM.png>)

Once a value is inputted, the modal will update with the hypothetical borrow limit as well as the hypothetical borrow limit used if this transaction were to be made. If you are ready to supply this asset, click the `supply` button and Metamask will open with the transaction ready to sign.&#x20;

![Metamask Confirmation](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.18.32 PM.png>)

Click `confirm` in Metamask and the transaction will be validated. The modal will update with the transaction status letting you know when the supply has gone through. After the supply has been validated, you will receive cTokens in your Metamask wallet, the total of which depend on the exchange rate between the underlying asset and the cToken. These cTokens are used to track your total supply in the market and can be used to redeem your supply balance in the withdraw modal.

![cToken in Metamask](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.23.36 PM.png>)

### Withdrawing Supply

If you wish to withdraw any of your supply balance, you can click on the currently supplying row and switch to the withdraw tab.

![Withdraw Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.33.01 PM.png>)

The withdraw tab will show how much of the asset you are currently supplying, and you can manually type in the amount desired to be withdrawn, in terms of the underlying token, or you can click the `max` button to withdraw your entire balance. (You will not be able to withdraw if the hypothetical borrow limit used will go over 100% as this will result in liquidation). The withdraw modal will also automatically update the hypothetical borrow limits as the value in the withdraw input changes.&#x20;

![Withdraw Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 5.36.10 PM.png>)

Once you are ready to withdraw, click `withdraw` and Metamask will open with the transaction ready to be signed and verified. After the transaction is completed, you will see your cToken balance of this asset decrease and the underlying token balance increase by the amount you have requested to withdraw.

## Collateralizing

In order to borrow any asset from the lending market, you must collateralize your supply. The amount you can borrow is directly related to the collateral factor of each specific token and how much you have supplied in the market. To collateralize an asset, click on the collateral switch in the supply rows.&#x20;

&#x20;

![Collateral Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 6.34.10 PM.png>)

In this modal, you can click `use 'asset' as collateral` and the transaction will open up in Metamask. After the transaction has been verified, you will see the switch in the lending market flip.&#x20;

![Supply Row With Collateral On](<../../.gitbook/assets/Screen Shot 2022-07-27 at 7.10.10 PM.png>)

### Decollateralizing

If you would like to decollateralize an asset, the same switch can be clicked and this modal will open:&#x20;

![Collateral Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 7.56.28 PM.png>)

In this modal, you can click `disable 'asset' as collateral` and the transaction will open in Metamask. This button will not be available if performing this action will put you above 80% of your borrow limit, since this may lead to liquidation.&#x20;

![Collateral Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 7.59.06 PM.png>)

## Borrowing

In order to borrow an asset, there must be enough supply in the lending market to borrow against. To borrow, click on the row in the available borrow table. This will open the borrow modal.

![Borrow Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 8.05.12 PM.png>)

In this modal, you can type in a manual amount to borrow or click the `80% limit` button to use 80% of your total borrow limit. More than this may be manually entered, but be careful of using too much of your borrow limit. As the value in the input changes, the hypothetical borrow limits are also updated to reflect your position if this transaction were made.&#x20;

![Borrow Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 8.08.43 PM.png>)

Once you are ready to borrow this asset, click `borrow` and the transaction will open up in Metamask to be signed and verified. (Note that any asset borrowed will automatically switch this asset to "collateralized")

### Repaying Borrows

To repay a borrowed asset, click on the currently borrowing row and switch to the repay tab.&#x20;

![Repay Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 11.17.28 PM.png>)

In order to repay any asset, it must first be enabled by the market by clicking the `enable` button. Once approved, the asset is ready to be repaid. You can either manually type the amount of asset you wish to repay, or click the `max` button to repay your entire borrow balance of this asset (if you currently do not have enough to pay back the entire borrow balance, the `max` button will input your entire wallet balance instead).&#x20;

![Repay Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 11.19.20 PM.png>)

Once a value is inputted, the hypothetical borrow limits will update and when you are ready to repay the borrowed asset, click `repay`. This will bring the transaction to metamask where it can be signed and verified. Once verified, the screen will update and your borrow balance will update accordingly



#### 6. Claim Rewards

After supplying assets, you will receive distribution apy. To claim these rewards click on `claim rewards` in the top right corner of the page.&#x20;

![Claim Rewards Button](<../../.gitbook/assets/Screen Shot 2022-07-27 at 11.33.39 PM.png>)

![Claim Rewards Modal](<../../.gitbook/assets/Screen Shot 2022-07-27 at 11.34.18 PM.png>)

The claim rewards modal will show how much Canto you have in your wallet, how much unclaimed Canto rewards you have, and the $Note value of these rewards. In order to claim these rewards, click `claim` and metamask will open with the claim rewards transaction.

Disclaimer: These rewards are paid out in WCANTO, the wrapped ERC20 token with the same value as Canto. In order to covert this token back to Canto native token, visit [convert coin](broken-reference).

