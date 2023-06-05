# Community Raise

The NFTX token supply is 650,000 and 60% (i.e. 390k) is being distributed based on the community raise. The raise will accept both ETH and D1 NFT fund tokens to help the NFTX Dao bootstrap AMM pools. Half of the 390k tokens are for ETH contributions and the other half are for D1 NFT fund tokens. All NFTX sent to supporters in return for their contributions are vested (i.e. locked) until January 5th 2021.

The raise will begin on Dec 22, 2020 at 11am PST. There will be a per-transaction NFTX cap that starts at 0 NFTX and increases to 50,000 NFTX over the span of one hour. This is simply to avoid the possibility of whales eating up the entire supply before smaller contributors have had a chance to participate.

You can view the "XBounties" smart contract [at this link](https://etherscan.io/address/0x9C5a36AEf5A7b04b0123b2064BD20bc47183e1DC#code).

## ETH Contributions

The 195,000 NFTX tokens allocated for ETH contributions are tranched over three valuations. It is not expected that the second or third tranche will get reached anytime soon, but by pre-programming future rounds early contributors know exactly what to expect.

* Tranche 1: 65k NFTX @ 130 NFTX/ETH
* Tranche 2: 65k NFTX @ 65 NFTX/ETH
* Tranche 3: 65k NFTX @ 43.3 NFTX/ETH

## NFT Contributions

The 195,000 NFTX tokens allocated for NFT contributions are split across 16 different fund tokens which wrap 6 different NFT contracts. Here are the NFT contracts preceded by the total amount being allocated to each:

* 93,925 NFTX for CryptoPunks
* 23,400 NFTX for AxieInfinity
* 23,400 NFTX for Avastars
* 23,400 NFTX for Autoglyphs
* 19,175 NFTX for CryptoKitties
* 11,700 NFTX for JOYWORLD

Below is a list of D1 fund bounties. Each fund token has a certain reward rate which contributors are eligible for. For example, the reward rate for PUNK-BASIC is 390 NFTX, which means that if Alice mints and deposits 2 PUNK-BASIC then she will receive 2 x 390 NFTX (for a total of 780 NFTX tokens). However, each fund also has a reward cap, which is the maximum amount of NFTX tokens to be distributed. So, in our previous example, Alice's transaction would only get accepted if her transaction did not cause that category to go above its cap. The "expected" column is simply the reward cap divided by the reward rate.

| Fund           | Reward Rate | Reward Cap  | Expected |
| -------------- | ----------- | ----------- | -------- |
| PUNK-BASIC     | 390 NFTX    | 31,200 NFTX | 80       |
| PUNK-FEMALE    | 520 NFTX    | 15,600 NFTX | 30       |
| PUNK-ATTR-4    | 585 NFTX    | 14,625 NFTX | 25       |
| PUNK-ATTR-5    | 1,950 NFTX  | 15,600 NFTX | 8        |
| PUNK-ZOMBIE    | 8,450 NFTX  | 16,900 NFTX | 2        |
| GLYPH          | 1,300 NFTX  | 23,400 NFTX | 18       |
| AXIE-ORIGIN    | 130 NFTX    | 7,800 NFTX  | 60       |
| AXIE-MYSTIC-1  | 975 NFTX    | 7,800 NFTX  | 8        |
| AXIE-MYSTIC-2  | 3,900 NFTX  | 7,800 NFTX  | 2        |
| AVASTR-BASIC   | 19.5 NFTX   | 7,800 NFTX  | 400      |
| AVASTR-RANK-30 | 26 NFTX     | 7,800 NFTX  | 300      |
| AVASTR-RANK-60 | 195 NFTX    | 7,800 NFTX  | 40       |
| KITTY-GEN-0    | 32.5 NFTX   | 6,760 NFTX  | 208      |
| KITTY-GEN-0-F  | 39 NFTX     | 5,850 NFTX  | 160      |
| KITTY-FOUNDER  | 6,175 NFTX  | 6,175 NFTX  | 1        |
| JOY            | 650 NFTX    | 11,700 NFTX | 18       |

It is possible for our Dao to update this community raise smart contract and change the rate or cap for any particular fund. We will likely choose to do this in cases where the reward rate is too low to suck in any more assets, however we also encourage the community to be patient in this regard, since a rising NFTX token price translates into a higher reward rate, so with enough time it is possible that not many changes will have to be made. As a general standard, we will try to limit changes to at most once per week, and give followers at least a 24 hours notice before changes are enacted.

For those that are unsure about which fund to mint and deposit, consider comparing the prices for NFTs on OpenSea with their respective reward rates above. Also note that some NFTs have their own marketplaces which tend to be more liquid than OpenSea. CryptoPunks have the the [LarvaLabs website](https://www.larvalabs.com/cryptopunks/forsale), Axies have the [AxieInfinity marketplace](https://marketplace.axieinfinity.com/axie?title=Origin), and likewise CryptoKitties have [their own marketplace](https://www.cryptokitties.co/search/50?include=sale\&search=gen:0) as well. It may also be worth checking current supply of fund tokens on the NFTX site. It's safe to assume that anyone who has minted a fund token this early is likely planning to use it for the community raise, so if you see that one fund already has a supply which exceeds the "expected" quantity above, then that may not be a good choice since you will have to compete to not be last when the raise opens.

Some funds also require waiting 24-48 hours after minting to receive your fund tokens. This is referred to as a "mint request" and is necessary for funds which either have a very large number of potentially eligible tokens or that target an attribute which can change (e.g. the "fast" attribute on CryptoKitties). The reason for the delay is that the Dao must verify the mint requests manually, and voting takes 24 hours to complete. After the request has been verified then the requestee will receive their fund tokens (e.g. KITTY-GEN-0). If requestees change their mind or get impatient they can revoke their request and retrieve their NFTs at any time, assuming the request has not already been approved by the Dao.

Lastly, it's important for contributors to remain cognizant of gas costs, which can add up quickly both when purchasing NFTs and also when using those NFTs to mint tokens on NFTX. Gas usage for the NFTX contract is not particularly efficent, and this is something that will be improved in the future. However, in the mean time, we simply recommend that contributors wait for when gas prices are lower.

If you have any questions please visit our discord: https://discord.gg/5ygF8rxdYR
