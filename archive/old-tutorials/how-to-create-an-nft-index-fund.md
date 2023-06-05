# How to create an NFT Index Fund

One of the advantages of using the NFTX platform is the permissionless way in which anyone can create a fund. Below are the steps you need to go through to create a fund yourself.

Note: SushiSwap is currently having issues listing the tokens on the frontend, which should be resolved shortly.

## **Choosing your NFT collection**

Funds created on NFTX are currently only for Ethereum-based NFTs, and the following contract types are supported for fund creation:

* ERC721
* ERC1155&#x20;

Once you have confirmed you are creating a fund for one of the supported NFT formats listed above, you can move to the next step.

You must have at least one NFT for the fund you plan to create. You will use this NFT to add your first asset to the fund/vault.

## **Step 1: Creating the NFT Vault**

The next thing to do is head over to[ **https://nftx.org/#/backend**](https://nftx.org/#/backend)\*\*\*\*

![](https://lh6.googleusercontent.com/icYa-bDC9Vd8Ph03KOdQiJVVaP2mJJzz851WzRYu4tDNjCCGGsyei-\_8-2j3eUiJYht8yr9bRwLecX2RlckyeVdnYg0zWp1Cj3x83N-hm9ub5SI3I6F0BR-9TbImQ1o36twDAkVZ)

After connecting with your wallet, you will notice there are two (2) contracts, **NFTX** and **XStore**. We will be primarily using NFTX for this tutorial.

Choose the `Write` action from the `[...]` dropdown menu next to the NFTX Contact.

![](https://lh5.googleusercontent.com/o6NB72Tb8xBlMr0BPS8\_kjIPQSnXt4qiUNDbdIPdDwNBI5OHVT77Uen04ppIwU3f0JqYnWcay5BfNBi6\_wKiXIMBs63Yab553\_0arlUuEvxB6grRXHvg0\_LFr8QIrzwi7qvsA8SA)

Scroll through the list until you see the `CreateVault` function where you will need to fill in four (4) fields. We've used Twerky Pepes as an example in the tutorial:

1. **Name of fund:** Twerky Pepe _(This is the name your fund token will have)_
2. **Token Name:** TWERKY _(Try to keep the token name simple. One word, if possible. No dashes. Seven (7) characters or fewer, if possible.)_
3. **Contract Address:** 0xf4680c917A873E2dd6eAd72f9f433e74EB9c623C _(the NFT contract address)_
4. **D2 Vault:** false

![](https://lh6.googleusercontent.com/xOADj9mvPz2ulmcIUoAvQ8lcPKtKWx1aOA\_u6n1ZO47TkPdvXNmLmLMOX8LSPaVT\_SGQoLGRTytiZcK6U9o0WQvusC3DLC5sd441Wn0jB88F0frkCosCg1i2hTkiEhIaz3aK0b2A)

If you are unsure what the contract address is for your NFT, you can find it in the Chain Info dropdown menu on your NFT OpenSea page (you can also get an individual Token ID from here).

Clicking on the link will take you to Etherscan where you can copy the address. Keep that Etherscan page open; you'll need it soon.

![Screenshot from the Opensea page for Twerky Pepe](https://lh4.googleusercontent.com/2BoigsrWDsbB4FZsjbBVTqwJOQr9B7uJ1ku-w7We8ztD3Ah7Wwze9WSwSI1mtKcvYICwTsmkxWbhAaDB0TM1j8AWqZgqrqC0\_ojpevQQhLuFiIAZQiRiG7pmu1D-Zqcq0Or6cR6q)

Once you've got those details, click on `CreateVault` to advance in creating your first NFT index fund. At this point, you will get a prompt from MetaMask to pay Gas for the transaction.

![Metamask asking for permission to create the vault.](https://lh6.googleusercontent.com/LpwxTOpATTs8xPJEnOx\_LM3C5Kz9GaHyvQ-J6Zqcj6qcVcoOfNxPZHZ5w5nc-VZ9sjr8W0Wi2GytKNNakzFJdqg67BF2NieL\_IB3RwONvv\_Uz9NmP3zqfMX1BkMfPkf6-xuWbpbm)

Once you get confirmation that the process has been completed, you will need to find the `vaultID`.

## **Step 2: Finding the vaultID**

Every fund that is created gets its own vaultID. You will need to finish setting up the vault. In the future, these steps will be taken care of for you through a new frontend.

You should still be on [**https://nftx.org/#/backend**](https://nftx.org/#/backend), but this time we need to interact with the XStore contract.

![](https://lh3.googleusercontent.com/D9QILFVhZXYyGAf-xC5sDOYGUmAlbEsdsZu9eDPJNk-oTxVaD3-ETyyTzM8VhSwU7xiYh8pmEC36B9PfY9dQwf1gI9PufkYWxD9SlO5J1rn0o5rBd5CCUxQr\_9OoXFxJ2kB0vEkn)

Copy the XStore contract address,[ 0xBe54738723cea167a76ad5421b50cAa49692E7B7](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7#readContract) and head over to Etherscan.

Paste in the contract address and go down to Contracts → Read Contract.

Alternatively, here's a link:[ https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7#readContract](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7#readContract)

Scroll to the bottom of the page until you come across `vaultsLength` which will show how many funds have been created. The image below shows thirty-two (32) vaults, but because the vaultID's start at 0 the latest vault created will be number 31.

![Showing the number of Vaults](https://lh3.googleusercontent.com/5rHmK8MZTSWEl1XTOVW5YoPF9mQ5OE2uL2GbyTygXQkXsFBzOc9PEVN3A2Czy\_yxaq8SwruTkVHK3r1ZIQ9PFAO5DMY0Zdm0GK3Dhtisqkr86CDIj6-vhjwz-TfHlGNqV-CLQWq3)

For our purposes, our `vaultID` was number 29 when we created the TWERKY fund.

Now that we have the `vaultID`, we need to confirm what type of fund this is and finalise, but before we do that, let's double check that we've got the right ID.

While still in the XStore Contract, move down to function number 33, xTokenAddress, and add the `vaultID` (in our example, 29).

![](https://lh6.googleusercontent.com/Gwt08\_EmhWTzebtxkMUm6B6KxSPJrFU46kutqrJ\_88ww45MJAnAmiESGa7AVrbOhd3DQlWIn4abrIX71jwC0WpFEM3KKmKetJKUv8LhU1TM0ZX6BYBlCHeCw9x9hjsIzmh6WI-G5)

This provides us with the address for the token as a link to that contract on Etherscan. Click the link and you will be able to see what the token contract address is.

![](https://lh3.googleusercontent.com/7eheI6mtYdPyO1DLqCoAQN61qUGgTCUDFsI2faRbPfWuiJf\_A8DwiHoQESs3zYeY4eKVS3qgBNWgKeN-Kl23GG0ASSeYOLqq5mc9ItBlzMYJuUmwJDgVXro2DH-h3qJ2BXXgvaQ6)

As you can see, the Token Tracker contains the name and the token for the fund we just created. If this doesn't match your fund, someone might have created a new fund just after you, so try the preceding or following `vaultID`.

## **Step 2.5: Setting vault to ERC1155**

**This step is only required if you are creating an ERC1155 fund, otherwise skip to Step 3: Finalising the vault.**

Return to the[ https://nftx.org/#/backend](https://nftx.org/#/backend) and choose the NFTX `Write` function again, except this time instead of creating a vault we want to use `setIs1155`.

Include the vaultID as 29 (which is the vaultID for TWERKY) in the first field and the value "true" for the second field.

![](https://lh5.googleusercontent.com/5OBeefdEfX-fFg7CIotFM7eaP1AePfResppRZJnlP\_\_lJXWIGBkkuZPV1akqTbv2jNkL4sRbvciERNPLpkSgm27FxUGkThP--yv3-vXbtXUIvIO1nw2ubXXF\_YYlmteoTnOUJ50Q)

This will require a bit (but not much) more gas, as it involves another transaction. Confirm the transaction on the MetaMask prompt.

![](https://lh5.googleusercontent.com/UHuP-LtNo37J5gzphluMxOMlUd28gQhAKk-y3kkLw4ITlJ2ErrI\_OB0xz2ubW\_aiGsdlpO6EMyyR2\_ZwcseVQVIc5uHXH1f-6RXM9KddMUUaI6B15XhaGD9nKrC19\_WryUAxS46W)

Once that has been completed, it's time to finalise your vault.

## **Step 3: Finalising the Vault**

We've almost finished.

Head back to[ https://nftx.org/#/backend](https://nftx.org/#/backend) and into the NFTX → `Write` option again. This time find the `finalizeVault` function. Add the `vaultID` you confirmed a couple of steps back (in our example, 29).

![](https://lh5.googleusercontent.com/xy4ubUJHsay6d3cIZA4XrZtfdYRLiCN37YsCCgE0q1uXDr4ERFH4szyZmx54uIIivFT1eagT0eYlY3vf9c29SI4RLqDzp64OwuSdqxkANNo8DheWGz5jJart4ZLXIOvQEKySDu1Y)

This is the final transaction for creating the Vault.

![](https://lh4.googleusercontent.com/SpRCBaFIsDNQozjXo\_CzKky5dxDKqgpufWBlsiUvaqAJiLzZxYLGz7FWlE45yhfWWZawEsOjmmFa6PJtulvpjIz8onknV\_Xyruc-6EwnxomP2kUvzOa7sOCkCsiFM3JvOFodJLpr)

Congratulations, now you've created your first vault! 🦧🕳

### **Things to note**

1. Once you create your vault, you will not appear on the list of available funds on the NFTX.org site automatically. While it is permissionless to create funds, we want to manually approve them for display in order to prevent scams. You can still send people to your fund by providing them with a direct link,[ https://nftx.org/#/fund/](https://nftx.org/#/fund/29)**vaultID**, or in this case[ https://nftx.org/#/fund/29](https://nftx.org/#/fund/29)
2. Minting tokens isn't immediately possible until you have completed step 4. See the instructions below.
3. Your fund will not automatically be displayed on the [NFTX Gallery](../../) site. This is done for two (2) reasons: to prevent scam funds from being promoted on the NFTX site AND because there are some image/content requirements for fund displays. If you would like to be added to the Gallery, please complete this form:[ https://docs.google.com/forms/d/e/1FAIpQLScnaUGFuz6-iyLTCeLhcLcFfxAdpPhGzGfxDtET7qgBIJO\_xg/viewform](https://docs.google.com/forms/d/e/1FAIpQLScnaUGFuz6-iyLTCeLhcLcFfxAdpPhGzGfxDtET7qgBIJO\_xg/viewform). Once you complete and submit this form, we will review your fund.

## **Step 4: Allowing Minting**

Now that the fund has been created, we need to give permissions in order to mint NFTs into that fund.

We will need the Etherscan NFT Contract Address page for the next step(s).

As a reminder, the contract address for the NFT collection (_not your fund_) can be found listed in the Chain Info on an OpenSea page:

![](https://lh6.googleusercontent.com/RAbDlw01O2w4obiK2F8fcriDRx1FOG\_V9jG5teOkUPJmpkgsoPwReASDyNPWSiE\_7ayZmjqu5vGvhlIwk3ri2T18GafuJGUocofm-3j713EkE2Knn8bGYFWXE9zhlqb7tF\_3AyA3)

Now that you've got that link (in our example [https://etherscan.io/address/0xf4680c917a873e2dd6ead72f9f433e74eb9c623c](https://etherscan.io/address/0xf4680c917a873e2dd6ead72f9f433e74eb9c623c)), visit it and move to Contract -> `Write`.

In this step, we are specifying the NFTX Proxy contract to allow interacting with the NFT contract, with the intent to mint index fund tokens in step 5 of this tutorial.

Use the following information to fill in the `setApprovalforAll` fields on Etherscan.

* **\_operator:** 0xAf93fCce0548D3124A5fC3045adAf1ddE4e8Bf7e (NFTX proxy contract)
* **\_approved:** true

![](https://lh6.googleusercontent.com/-uX1kJJMnNwp-iNZlDBCPLjPSJCS3cEQlgrA-\_2V87g2ipMlvDwGYMDaMHof1kxYBWkql\_st9yDfuyWO5Gmlffe9L6quLW5lnQeIDYmOjhOeiK21mYIeKUB2DxCUncZmNDxgCT5k)

This will require another transaction and transaction fee.

![](https://lh5.googleusercontent.com/wvp90ovq73vL3vrlkOq0xCJoKUG6qaCnll2d6eEYRc0PQvHgimOgPMYayXOo3REPPZVm6FbbxtlOlNQ3bnMn9xyTP3xo-fyVmtVSufInxCWSL9HilNtduxpPNyRMQ3rh7F0xW5KC)

## **Step 5: Using your new fund**

Now that you have set up your new NFT Index Fund and allowed Minting, you can start using your fund to create Index Fund tokens (ERC20) using `Mint`.

This can be done from the frontend once the fund has been approved. If you don't want to wait, you can get started instantly on Etherscan by following the guide below.

[**Go to the NFTX contract address**](https://etherscan.io/address/0xAf93fCce0548D3124A5fC3045adAf1ddE4e8Bf7e#writeProxyContract) _\*\*0xAf93fCce0548D3124A5fC3045adAf1ddE4e8Bf7e_ , click on Contracts → `Write as Proxy`, and then choose `Mint`.

**You want to include:**

* **payableAmount** — put a 0
* **vaultID** — the vault you want to mint into (likely the one you just created)
* **nftids** — you need to put these in \[48] square brackets. You can mint more than one, but separate them with commas and no spaces i.e. \[48,53,89]. These ID numbers are also listed on the OpenSea info.&#x20;
* **d2Amount** — put 0 into this field

![](https://lh5.googleusercontent.com/rD4LbjGPMO0lFIfxLqeiaHfvIO5FyDVwvbcRg3W2ikq9nZivafKvMyAVZUZ6lu4NRZnMfso0WzoeyzR4oGZrGDXGXlSSDqH5U16iqdDJV57KkhLOuGDiP8gON7p-GvefhQwmbe-D)

Once you're happy, you can click `Write` and it will ask you to confirm the transaction with your MetaMask.

![](https://lh4.googleusercontent.com/Vm-UOlYky029Fa895h53wUFRqdGZd2WNERf9MYEaNUI4HS2BDfaMMrYjyYittZXvlrAYZ4aObBzcoBh3BuOkx6BTDw\_EUI5YDjbs-73l2ZCOBEmvkgAAiKI9cM2wSnxvJTNvxJbW)

Once completed, you can verify that the NFT has gone into the fund two ways.

**First way:** Check the OpenSea listing after a few minutes (takes a while to refresh) and you should see a transfer of ownership between you and NFTX.

![The minting was successful, moving the NFT into the NFTX fund.](https://lh5.googleusercontent.com/oYs-FPZoU9i3MQ8kX-6Wds7BYB6g059ISrlD0NZ1EJbfmFQ8NuHIxhVtRWcoTBX4q\_5ORyqq3xh97HTza7-TUi\_5j7Xd2FkqvD1mAU1mKB1GOyqSQD\_0fzvb\_9\_cc4Mxnvlazov4)

**Second way:** Head to the[ XStore contract on Etherscan](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7#readContract) and run the Read Contract `holdingsLength` which should return the number of NFTs in your new fund.

![](https://lh4.googleusercontent.com/BtG39o4PsuiXrTF9oUGn6fCcVtFDSSAczXCXXo8\_wrNFP9F8tPcQ80TBgDUe7\_nF0bxVQ8LLfvoNFv1hlU16JHy2sUlhVFd4PWKtV\_J8yu34o0d\_Wq7v2XuSCUiFZyDchfzuI2Xa)

## **Wrapping up**

You're now a proud parent of an NFT Index Fund.

We weren't able to cover every scenario in this tutorial, but the instructors cover the process of creating your own fund. The current vault creation process is being refined by our team. Soon, the process will be simplified for our users.

Some things that weren't covered in this guide, but are possible, include:

* Adding Allow Deny lists for Funds. This is great if you want to create a fund like Punk Zombie and only allow certain NFTs (the ones with Zombie traits) from the same collection (CryptoPunks) to be minted.
* Allowing Allow ranges — This is great for funds like Art Blocks that are all on the same NFT Contract, but each project has its own distinctive range for their NFTs (based on the ID of the project).

If you have any suggestions or comments please drop by discord for a chat.
