# Litepaper

NFTX is a platform for making ERC20 tokens that are backed by NFT collectibles. These tokens are called funds, and (like all ERC20s) they are fungible and composable. With NFTX, it is possible to create and trade funds based on your favorite collectibles such as CryptoPunks, Axies, CryptoKitties, and Avastars, right from a DEX like Uniswap.

There are two types of funds on NFTX:

* D1 funds (input) have a 1:1 backing between a single NFT contract and an ERC20 contract. For example, if Alice owns 2 PUNK-ZOMBIE, that means she can redeem exactly two random zombie CryptoPunks at any moment. Another example would be Alice owning 1 AXIE-MYSTIC-2, giving her the ability to redeem one random Axie with two [Mystic parts](http://axie.wiki/index.php?title=Parts#Mystic). &#x20;
* D2 funds (top-level) are Balancer pools which combine D1 funds. For example, AVASTR will be a D2 fund which combines three different D1 Avastar input funds (AVASTR-BASIC, AVASTR-RANK-30 & AVASTR-RANK-60). The point of this is to offer more diverse exposure without requiring users to hold multiple tokens.&#x20;

When a new fund is created, the account which sends the transaction is designated as the fund manager. This allows the creator to change fund parameters like fees, supplier incentives, and NFT eligibility. When the creator is done modifying the fund they can then “finalize” it which gives up their control to increase trustlessness.

## Target Users

A common misconception is that NFTX is a project for NFT collectors, but most NFT collectors enjoy browsing and trading individual NFTs, so there is no reason for them to wrap their collections into fungible tokens. There are, however, many people out there that don’t have the time or knowledge to trade individual NFTs but would like exposure to NFT markets. These are the NFTX target users—the people trading top-level funds of NFT blue-chips such as AXIE, PUNK & KITTY on Uniswap, not the people minting/redeeming their NFT on the NFTX website. Most of the time the only people minting/redeeming fund tokens will be arbitrageurs. This is similar to the dynamic with WBTC. Most people that trade WBTC do not mint and burn it themselves.

NFTX will start out with just D1 funds, so at first the homepage will have quite specific funds listed, however once the top-level D2 funds are created then the homepage can shift focus to those funds instead. The idea is for NFTX to be somewhat like a CoinMarketCap or DefiPulse style website but for the NFT space. Users will arrive at the homepage and be greeted with metrics for top-level funds backed by NFT blue-chips such as [CryptoPunks](https://www.larvalabs.com/cryptopunks), [Axies](https://marketplace.axieinfinity.com), [CryptoKitties](https://www.cryptokitties.co/), and [Avastars](https://avastars.io/).

Eventually, the hope is for NFTX to become home to over a hundred top-level NFT funds, each of which will feature real-time price, volume and TVL data.

## Platform Management

The process for creating a fund was inspired by Balancer’s process for creating a pool. Essentially, the pool creator gets “manager” privileges but can also call a “finalize” function which renounces their control. Like Balancer pools, NFTX funds also have a finalize function, but unlike Balancer, when the NFTX finalize function is called then control of the fund is handed over to the NFTX Dao. There are two reasons for this.

The first reason for the Dao receiving fund management privileges is that in some cases funds require ongoing governance (e.g. having new eligibilities added). The second, more controversial, reason for why the Dao receives management rights is so that we can guide the platform to evolve in a way that we see fit. If funds start cannibalizing each other (e.g. multiple funds targeting similar NFT subsets) then that can hurt our platform’s UX, so in such a situation we can decide to close all but one of the funds so that the remaining one may prosper.

The goal is for NFTX to offer one top-level fund which gets most of the liquidity for each major NFT contract. For example, if someone wants to create a AVASTR-V2 fund that differs from the main AVASTR fund, then that is fine (and actually encouraged), but if we get into a situation where AVASTR and AVASTR-V2 are splitting the liquidity down the middle and there is an easy fix (e.g. merging the differences) then that is something that the Dao can consider doing.

## Moat & Value Capture

Long-term, the goal for NFTX is to develop a moat as the primary issuer of wrapped NFT funds. This is potentially a huge use-case with the legitimate possibility of one day eclipsing the present market cap of all cryptocurrencies combined. Digital land, in-game items, lease-agreements, digital art, digital collectibles, digital lottery tickets and more can all be represented as NFTs. As the NFT ecosystem grows it will get increasingly difficult to keep track of, and tokenized funds will become a necessity for many investors and trading platforms.

In terms of value capture, it’s not inconceivable to consider a 2.5% fee in the future on all NFTX mint and burn operations. This added cost would mostly be absorbed by arbitrageurs and would essentially cause fund tokens to drift off-peg slightly more than usual. For a wrapped token like WBTC, a 2.5% price difference from regular BTC would be a major UX flaw, but for NFT funds (which represent an inherently illiquid category of assets) a 2.5% price difference would likely be unnoticeable.

## Avenues For Growth

1. **NFT→ ERC20 Loans —** Minting a D1 fund token requires handing over an NFT, and in many cases people will want the benefits of a fund token without having to give up ownership of their NFT. These people would prefer to lockup their NFT in return for a loan (similar to minting Dai with ETH). By having a surplus of D1 tokens in the NFTX treasury, our platform will be able to provide low-interest ERC20 loans to NFT collectors. Furthermore, these loans will have zero risk of unexpected liquidation because NFTs are always worth at least as much as the D1 funds which they are eligible for. &#x20;
2. **On-Chain Liquidity** — _\*\*_One of the biggest problems in the NFT space is price discovery. Unless market makers are in "the know" it can be challenging for them to determine the real price of an asset. One reason for this is wash-trading, another reason is illiquidity and gaps between sales. Having real-time price feeds from popular funds largely solves both of these issues. As a concrete example, if a trader can check that PUNK-ATTR-4 is 150% the price of PUNK-BASIC, and that PUNK-ZOMBIE is 60 ETH, then they are able to determine that a zombie CryptoPunk with four attributes should be about 150% of 60 ETH, or 90 ETH. With this problem ameliorated, it's not hard to imagine NFTX branching into the on-chain liquidity game, enabling NFT market makers to automate their strategies, and aiming to become somewhat of a "Kyber for the NFT space."
3. **Randomized Packs & Gift Cards** — Having a large reserve of NFTs opens up a number of possible usecases for NFTX. One such possibility is a service offering randomized packs with varying likelihoods of different NFTs. Another possibility is gift cards. Currently when a user redeems an NFT by burning a fund token, the NFT they receive is randomly selected, however it is possible for us to extend the NFTX smart contract so that (for a added charge) users can select the exact NFT which they want. This would be analogous to a gift-card and would enable recipients to enjoy the process of selecting their own unique items from the NFTX reserves.

## Near-Term Roadmap

The first item on our organizational to-do list is the NFTX community raise, which will be deployed in the coming week, and which will likely run for a number of months. More information about [this raise can be found here.](../archive/community-raise.md)

Once the community raise is partially complete, and all of the D1 funds have at least one asset in them, then it will be possible for our Dao to launch the top-level D2 funds. This will be a top priority, and in many ways we will consider NFTX to be in a pre-launch state until the top level funds (PUNK, KITTY, AXIE, and AVASTR) are up and running, as these will be four of our six initial flagship tokens (along with GLYPH and JOY).

The current front-end site for the NFTX dapp is quite buggy and needs a number of improvements. This will be an ongoing process over the next couple months, which will become a greater priority as we approach the the start of our liquidity mining program, sometime in late Q1 or early Q2 of 2021, the details of which are still undecided.

Some project followers have already reached out with questions regarding the NFTX brand. In addition to improving the functionality of the front-end, we are also very open to a doing a full rebrand based on the preferences of our nascent community. If you have thoughts on this we encourage you to reach out or put together a community proposal. Like everything else about NFTX, the brand is not fixed in stone and may be altered subject to voter approval.

In terms of governance, we will begin by using only Discord and Aragon. Discord will be used for discussion and Aragon will be used to enact decisions we have reached consensus on. Of course, Aragon may also be used to decide internal conflicts, but we will do our best to avoid contentious issues early on. Once we have found our bearings as a community we will create a Discourse forum and begin outlining some more formal procedures for decision making.

There will be no employees to begin with, however it is very likely that our organization will employ people in the future, so it's worth noting that we will aim to offer competitive compensation that is similar to what could be expected in the tech industry.

## V2 & Gas

Although NFTX version 1 is only just taking off, there are already improvements in mind for version 2. Some of these improvements involve new features, like smart funds, which will have dynamic rule sets. Other improvements involve security concerns which were brought up during our audit but which were tabled on account of being considered low severity. Likely the most pressing issue for version 1 will be gas costs, which are quite high, and which will be considered a top priority improvement for NFTX v2.

Even though most end-users (top-level fund traders backed by blue-chip NFTs) are unaffected by platform costs, it can still be a high friction point for arbitrageurs and the occasional users who do mint or redeem. High fees also limit NFTX's ability to offer price-accurate funds for lower value items (e.g. NFTs < 0.1 ETH). In the mean time we will make do by subsidizing platform costs if necessary and recommending that users avoid minting and burning during high volume periods.

## Conclusion

If there is one important take-away for readers it should be that NFTX is entirely community-governed. This document describes a vision for the future, but that future depends entirely on what NFTX token holders decide to implement. All assets from the community raise will be considered as part of the NFTX treasury and will be under the control of token holders. The intention is to use the bulk of the treasury to supply liquidity for fund tokens and also for the NFTX token, however, make no mistake, those are treasury assets and may at any moment be used to cover expenses, should the Dao choose to do so.

The current NFTX mission is to become a DeFi black hole for NFT assets. We will aspire to remain objective about which NFTs we give preferential treatment, focusing above all else on what is best for the long-term appreciation of the NFTX token. That said, we will also place high value on principles of decentralization and endeavor to work with like-minded organizations.

The only potentially unpopular opinions the NFTX DAO will have which community members should be aware of is (A) a bias for ETH and Ethereum, and (B) a bias for PUNK and CryptoPunks as a store of value for the NFTX DAO treasury.

When in doubt, we will store our organization's wealth in these assets. And, unless met with no other option, we will always remain rooted on Ethereum. Treasury allocation may shift towards a more diversified basket of blue-chip NFTs such as Axies, Avastars, CryptoKitties, Autoglyphs & Joyworld Joys' as more community members get involved in DAO operations & a proposal to diversify gets voted in through DAO governance.

We invite anyone and everyone to join us in our mission. Over time, that mission will inevitably change but it's important that we begin our journey on the same footing, and with the same principles in mind, so that we may move forward, not only as a community, but as an anti-fragile digital warband 😈

Discord link: [https://discord.gg/5ygF8rxdYR](https://discord.gg/5ygF8rxdYR)
