# Vault Creation

NFTX v2 introduces a new vault creation interface that allows you to easily create a public vault for any NFT or a specific subset of IDs for an NFT.

[Watch the video tutorial for creating vaults on NFTX V2](https://www.youtube.com/watch?v=Yt2aU7hxMmc)

## Why create a vault?

Vault creation is at the heart of the NFTX protocol and allows users and content creators to begin [minting](minting.md) fungible ERC20 tokens for any NFT.

By creating NFT-backed ERC20 tokens, users can create liquid markets for otherwise illiquid NFTs whilst also earning fees and rewards from liquidity provision.

Protocol fees have been introduced in V2 of the NFTX.

## Vault Creation Step-by-Step

### Create NFTX Vault

Three fields are required to create an NFTX vault as shown below.

![](../.gitbook/assets/tutorial-v2-create-vault-02.png)

**NFT Asset Address**

The NFT asset address is immutable and points to the contract from which this vault will accept mints. By default, all NFT IDs from this contract will be eligible for minting in the vault.

{% hint style="info" %}
Eligibility lists or ranges can be added once the vault has been created. This will allow you to target specific NFT IDs for groups of NFTs like "Female Punks", or create NFT ID ranges for specific projects like "720 Minutes" from Art Blocks, from within a single NFT contract address.
{% endhint %}

Some assets are already used in other vaults. For example, Art Blocks are used in multiple vaults and separated using eligibility ranges. To avoid adding a duplicate vault and splitting liquidity, review the matching vaults list before proceeding.

![](<../.gitbook/assets/check-matching-vaults (1) (1) (1).png>)

**Vault Name**

This will be the _name_ of the ERC20 token that is minted from this vault.

**Vault Symbol**

This will be the _symbol_ of the ERC20 token that is minted from this vault.

Both the Vault Name and Vault symbol will appear anywhere that this token appears, from CoinGecko and Etherscan through to Sushi and Uniswap.

{% hint style="info" %}
A strong name and symbol play a critical part in a vault's long-term success. Try to keep the name singular (PUNK, not PUNKS), six characters or less (to enable ticker links in Twitter), and use a real word where possible (BUNNY, not GENBIT).
{% endhint %}

### Vault Created

![](../.gitbook/assets/tutorial-v2-create-vault-04.png)

Once your create vault transaction has been confirmed onchain you will be notified and asked to proceed to managing your vault.

Your vault will not be visible in the NFTX app until it has been minted to and published. Click "Manage Vault" to complete the process.

### Manage Vault

Vault management allows vault creators to modify a number of important settings as well as publishing the vault so that it becomes visible on the NFTX app.

{% hint style="warning" %}
Published vaults cannot be edited by the creator, only the DAO can make updates to published vaults. Carefully review the vault's settings before publishing, including setting the Fees and Eligibility screens.
{% endhint %}

![](../.gitbook/assets/tutorial-v2-create-vault-05.png)

#### **Enable Vault Features**

**Enable Minting —** The most important part of creating a vault is allowing users to mint their NFTs in. If you wanted to use the vault as a way to airdrop tokens for users to redeem NFTs from the vault you might disable the mint feature.

**Enable Random Redeems —** Allow users to randomly retrieve an NFT from your vault.

**Enable Target Redeems** — Users will be able to choose the NFTs they are redeem from the vault for an additional fee which you can set within the Fees section.

#### Fees

![](../.gitbook/assets/tutorial-v2-create-vault-06.png)

Fees can now be set on the individual vaults which will then be distributed to the liqudity providers staking their LP. By default all new vaults are set with 10% Mint Fee (meaning you receive 0.95 tokens for each NFT minted), 4% Random Redeem Fee (so 1.06 tokens can redeem 1 random NFT from the vault), and a 6% Targeted Redeem Fee (1.06 tokens are needed to choose the NFT you want from the vault).

~~When you first create the vault, and _**before**_ you finalise the vault, you can set the mint fees to 0% to encourage the initial seeding of the vault~~. When seeding the vault with liquidity and inventory staking you bypass the mint fees, so you no longer need to reduce the fees to get the vault seeded.

{% hint style="info" %}
Don't forget that you can use Zaps to bypass the 5% mint fee by providing ETH liquidity for the vault and staking it to earn yourself fees. Find out more on [Bypassing Mint Fee's with Zaps](minting.md#bypass-mint-fees-with-zaps).
{% endhint %}

#### **Eligibilities**

![](../.gitbook/assets/tutorial-v2-create-vault-07.png)

A vault's eligibility list is an allow list or range of NFT IDs that can be minted to this vault.

**List Module**

![](../.gitbook/assets/tutorial-v2-create-vault-08.png)

Use this setting to specific individual IDs to add to the eligibility list.

**Eligibility Range**

![](../.gitbook/assets/tutorial-v2-create-vault-09.png)

For blocks of eligible IDs, use this setting to specify the "from" and "to" (inclusive) IDs that will be added to the eligibility list. **These work well for projects like Art Blocks Curtated which are all minted from the same contract but have distinct ranges for each project.**

### Publishing your Vault

Before your vault will be visible on the app you will need to mint at least one eligible NFT.

![](../.gitbook/assets/tutorial-v2-create-vault-12.png)

Once you've added one or more NFTs to your new vault you will have the option to publish your vault. Remember, once the vault has been published the ownership is passed to the DAO and you will no longer be able to update the Fees or Eligibilities.

![](../.gitbook/assets/tutorial-v2-create-vault-14.png)

![Last chance. You are asked to confirm your setting for Fees](../.gitbook/assets/tutorial-v2-create-vault-15.png)

Once confirmed you will be redirected to the vault detail page. On this page it will provide you with an overview of the vault details, including Vault ID, URL, Token Address, current Holdings, and Lifetime Fees.

![](../.gitbook/assets/tutorial-v2-create-vault-16.png)

### Verifying your vault & adding a vault icon

Once you have created and published your vault you will also need to provide an icon so that the vault can go through the final verification process.

To [add the icon and request verification complete this form](https://notionforms.io/forms/vault-verification), but make sure you have all the information required. Let's take a look at the requirements.

1. **Vault Name:** The name of your vault (not the token name).
2. **Vault ID:** You can find the Vault ID on the Info tab on your vault page in the right hand sidebar (or at the bottom if your are on mobile).
3.  **Discord Username** _(i.e. javery#3313)_: You can get this by clicking on your discord user on the bottom left of the discord app. We need this so we can reach out to confirm the details are correct.

    ![](https://downloads.intercomcdn.com/i/o/437512436/12c9066f38f468ba71454c91/Screenshot+2021-12-21+at+12.16.04.png)
4.  **Vault Icon**: upload a 512x512px transparent PNG icon that you want associated with the vault. See an example of the CryptoPunk vault icon below.

    ![PUNK](https://nftx-8e1220506660.intercom-attachments-1.com/i/o/437571507/89010aeffa2b0579949f63fa/256x256.png)
5.  **Signed Message**: Visit https://app.mycrypto.com/sign-message and create a signed message with the wallet that you used to create the vault. This allows the NFTX DAO to confirm that the request is originating from the owner of vault.

    \
    When adding your signed message please **ensure that you are signing the message with the wallet that you used to create the vault**.

Once we recieve the request someone from the team will verifity the signed message, update the vault icon, and verify the vault.

Please note that the vault is usable even though it has not been verified.

[Verify Vault Now](https://notionforms.io/forms/vault-verification)

## FAQ

### I am being warned about the vault name or symbol, what does this mean?

Naming conventions provide structure for NFTX vaults that makes them instantly recognisable across platforms and help improve the network effects for all participants in the NFTX ecosystem.

**Naming conventions**

| Vault Name                 | Vault Symbol                                     |
| -------------------------- | ------------------------------------------------ |
| Alphanumeric only          | Less than 7 characters                           |
| Capitalized (i.e. Meebits) | Singular (i.e. PUNK for CryptoPunks floor vault) |
|                            | Uppercase                                        |
|                            | Real words where possible                        |

The tight recommendations on Vault Symbol are in place to conform to Twitter's cashtag standard.

### Why isn't my vault isn't showing in the NFTX app?

The most common reason for this is that your vault does not yet have holdings or has not been published. To add holdings, visit the vault management page and click "Add Holdings".
