# Staking

## Why stake on NFTX?

Earn fees from the vault, currently 100% of protocol fees are paid out to those that stake. Liquidity providers earn a share of 80% and inventory providers earn a share of 20% of the fees.

Stakers also receive an ERC20 “xToken” like xPUNKWETH that is a claim on the underlying staked SLP, or xPUNK which is a claim on the underlying staked inventory. We expect other projects to build use cases for these xTokens.

You can learn more about the benefits of staking on [https://academy.nftx.io/staking](https://academy.nftx.io/staking)

{% hint style="info" %}
APRs are calculated by annualizing the last 30 days of the vault's fee earnings. The real rate of return will vary throughout the year.
{% endhint %}

## How to stake on NFTX?

To stake on NFTX you need an NFT from that collection. In this example we're going to look at the Space Poggers collection.

There are two ways to stake and earn fees

* Liquidity staking
* Inventory staking

Remember that in both situations your NFT ends up inside of the vault where _anyone_ can buy or swap it back out. You are not gauranteed to get the same NFT back, so don't stake any rare NFTs or NFTs that you are attached to.

### Inventory Staking

Go to the Stake page on the vault.

![The stake page shows you the NFTs in your connected wallet that you can stake into the vault.](<../.gitbook/assets/image (23).png>)

Select the NFT that you would like to stake as inventory into the vault. Note that in the image below we are staking Pogger #2877 which will give me a share of 3.26% of the inventory rewards (which is 20% of the fees), and the **position will be locked for 7 days**.

The lock period is there to avoid users from using staking as a way to bypass the mint/sell fees.

![](<../.gitbook/assets/image (22).png>)

Once you have confirmed BOTH the **Approve** and **Stake** transactions you will receive the below message that your transaction was successful.

<img src="../.gitbook/assets/image (6).png" alt="" data-size="original">

This will provide you with an xTOKEN (xPOGGER) which is a reference to your staked inventory position. The xTOKEN is usually _less_ than the number of NFTs you have added, for example we received 0.9241 xPOGGER back from staking one Space Pogger.

When we decide to exit our position, that is equivalent to at least 1 POGGER token plus any fees that are accrued during the time we are staked. When exiting you are also able to claim a random NFT from the vault and bypass the redeem fee, so you're always gauranteed to get the same number of NFTs out of the vault that you put in when inventory staking.

![](<../.gitbook/assets/image (19).png>)



### Liquidity Staking

Go to the Stake page on the vault.

Select the NFT that you would like to stake as liquidity into the vault. Note that in the image below we are staking Pogger #5389 which will give me a share of 0.78% of the liquidity rewards (which is 80% of the fees), and the **position will be locked for 2 days**.

![](<../.gitbook/assets/image (16).png>)

The lock period is there to avoid users from using staking as a way to bypass the mint/sell fees.

Once you have confirmed BOTH the **Approve** and **Stake** transactions you will receive the below message that your transaction was successful.

<img src="../.gitbook/assets/image (6).png" alt="" data-size="original">

This will provide you with an xTOKENWETH (xPOGGERWETH) which is a reference to your staked liquidity position. The xTOKENWETH is usually _less_ than the number of NFTs you have added, for example we received 0.0992 xPOGGERWETH back from staking one Space Pogger. This is your claim on the SLP on Sushi.

When we decide to exit our position, that **will not** be equivalent to the 1 POGGER or equivalent ETH your added into the pool when staking. If there were lots of sells you will get back more POGGER tokens and less ETH, if there were lots of buys then you will get back more ETH and less POGGER tokens, and unlike Inventory staking your rewards are not compounded into your position, and instead you can claim them at any time through the Dashboard.

![](<../.gitbook/assets/image (25).png>)





## How to UNstake your position on NFTX?

You can unstake both your liquidity and inventory positions on the [https://nftx.io/rewards/dashboard/](https://nftx.io/rewards/dashboard/)

Find the position that you would like to exit and select the "Unstake" button.

### Inventory Unstaking

When unstaking your position you have the option to receive just the vault tokens which you can then sell on Sushi for ETH, or you can claim a random NFT (or multiple if you staked more) and bypass the random redeem fee.

There is also the option to "Withdraw remaining x.xxxx TOKEN" which you could then sell on Sushi. If you decide not to claim the additional tokens they will remain staked and earning fees.

![](<../.gitbook/assets/image (17).png>)

### Liquidity Unstaking

Choose the "Unstake" button and select the amount of xTOKENWETH you would like to withdraw. This will return the SLP token which you can then unwind on Sushi directly.

{% hint style="info" %}
Before we unstaked there were 0.1499 BUNNY tokens that can be claimed. If you are unstaking your position those tokens will automatically be claimed as part of the process, saving you an additional transaction fee as part of the process.
{% endhint %}

When unstaking you will automatically claim all the reward tokens as well (so there is no need to claim your rewards before you unstake).

![](<../.gitbook/assets/image (24).png>)

Once the transaction is complete you can click through the link to "Remove Liquidity". This takes you to Sushi to unwind your SLP position and get back vTOKENS and ETH.

![](<../.gitbook/assets/image (18).png>)

In this example we will be receiving back almost 2 bunny tokens and 0.031ETH.

![Preconfirmation screen to approve the transaction (signed only, no gas)](<../.gitbook/assets/image (21).png>)

![Confirm the burning on the BUNNY/ETH and receiving tokens back - this costs gas.](<../.gitbook/assets/image (20).png>)



## Removing Liquidity from V1 Vaults <a href="#docs-internal-guid-227675f5-7fff-e5b1-c52b-9d3c69bb7b2e" id="docs-internal-guid-227675f5-7fff-e5b1-c52b-9d3c69bb7b2e"></a>

### Overview

With the release of NFTX Version 2 there is more benefit from moving your position from the old vaults on V1 to the new vaults on V2.

For an overview on the release of NFTX V2 you can read the blog, however in this tutorial we’re going to focus on how you can remove your liquidity from existing vaults on V1.

### Steps to remove your liquidity

Head over to the pool which you are providing liquidating. An easy way to do this is to find the Vault on the [gallery](https://gallery.nftx.org) and select the “Swap on Sushi” button.

Choose the “Liquidity” tab from that pool and then select “Remove” from the options. In this case we’re going to remove all of our liquidity from the pool and we will get back 0.0811434 ETH and 2.09975 TWERKY tokens.

You will first need to “Approve” the transaction and then “Confirm Withdrawl”.

![](https://lh5.googleusercontent.com/UtVb7DxosPHqg3xGk-U8l7D5JHWBn4wJ\_91sONewx6uR9ZdDLxBBifxM87JxfoWwpt2F4oNL4qFuy692uNzXDXQMVR9omEGkceWlbC6fcnz132BMAoKMxbeWJwr0qfMbiem0h6PH)

{% hint style="info" %}
Note: there is no rush for you to remove your liquidity from the pool, especially while GAS prices are high.
{% endhint %}

Once the transaction has been processed you will receive a confirmation along with details about the final Tokens and ETH returned.

![](https://lh5.googleusercontent.com/vbZxAEl2uujYEo17DPN-3ByK4pU-PSfT8XZyJAQmauL8ejnb9gQJFzGrCs-7fYsJ1nQbFSI83N6ZN\_cmrp\_2RPuWDnXJfIebHnBIW8wRVnWl7LMloC2HTdO15YwPsRm7tW1Dz8uv)

You will now be able to view your tokens in Metamask, and if you go to the NFTX App you can see your tokens in the header and sidebar.

![](https://lh6.googleusercontent.com/Il6GjVs7IuJRVuG-H7Eyz2ArG9iq5XSmfjyYMzuJd9p20TTDTZbhDYOoliyrFm0UP3\_9yYmIz9VF\_OkMfNJTA2JXmI7fye7FrhUh1xMK02DgvtabH9rV7q3bUM9D5bnhB37s1buv)

With you tokens you can now Redeem your NFTs from the Vault which will then allow you to

### FAQs

#### Why has my claimable balance not increased?

Rewards are earned when the vault generates fees. APRs are calculated based on the last 7 days of vault fees.

#### Do I have to remove my Liquidity?

No. You can keep your liquidity on the current vaults in V1 for as long as you would like and continue to earn fees on the trades on SushiSwap.

You will not be able to stake your liquidity and earn any of the 5% minting and 5% targeted fees on the new vaults unless you become a liquidity provider on V2.

#### I still have fractions of a token left after withdrawing my liquidity, what can I do?

These fractions of tokens are often referred to as dust. You have three options.

1. Sell the fractions of the token you have on a DEX like SushiSwap.  For low value NFTs there is a good chance that the GAS cost of this transaction will exceed the value of the dust.
2. Buy more of the token to take you up to one full token and use it to redeem an NFT from the pool.
3. Hold onto the dust until NFTX move towards a buyout. We expect there will be one NFT stuck in each of the vaults due to the dust and reduction of the liquidity. There are two options for resolving this which the DAO will vote on in the next few months
   1. The DAO will sell the final NFT and provide the fractionalised value of the sale to the dust holders.
   2. The DAO will propose to buy back the dust to retrieve the final NFT and keep it in the treasury

#### When will the NFTX DAO remove their liquidity from the V1 Vaults?

The DAO will remove their Liquidity in thirds across three weeks starting from the public release of V2. This is to ensure that holders of the NFT Tokens have time to sell their position without any major slippage/price impact.

{% hint style="info" %}
Lower liquidity does not impact the redeeming of NFTs from the V1 Vaults. 1 Token is always worth 1 NFT from the corresponding vault.
{% endhint %}
