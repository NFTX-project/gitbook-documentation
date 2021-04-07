# Introduction to NFTX

NFTX is a platform for creating liquid markets for illiquid Non-Fungible Tokens \(NFTs\).

Users deposit their NFT into an NFTX vault and mint a fungible ERC20 token \(xToken\) that represents a claim on a random asset from within the vault.

**Benefits include:**

* Use minted xTokens to earn yield
* Better distribution and price discovery for NFT projects
* Instantly sell any NFT by minting it as an ERC20 and swapping via Sushiswap
* Increased liquidity for NFT investors and speculators

### How does it work?

#### Vault Creation

Vaults can be created by anyone for any NFT asset on Ethereum. Once a vault has been created, any user can then deposit eligible NFTs into the vault to mint a fungible NFT-backed token referred to as an "xToken".

[Learn more about vault creation](https://docs.nftx.org/archive/get-started/how-to-create-an-nft-index-fund)

#### Minting xTokens

Anyone can deposit NFTs into an existing vault \(or one they have created\) in order to mint a fungible xToken that represents a 1:1 claim on a random NFT from within the vault.

[Learn more about minting](tutorials/get-started/minting.md)

#### Floor Prices

Users can then pool their minted xTokens in Automated Market Makers \(AMMs\) like Sushiswap to create a liquid market for other users to trade. With liquidity and trading volume established, the NFT-backed xToken enters into price discovery and a "floor price" is discovered.

The floor price denotes the lowest price for a particular NFT. Users establish a floor price by minting and selling xTokens in markets where they consider their NFT to be overvalued.

{% hint style="info" %}
NFTX is helping to establish reliable floor price feeds for NFTs, enabling their wider application in decentralized finance on Ethereum.
{% endhint %}

For example, a user has 5 Hashmasks and values 2 of them highly. However, they consider the other 3 Hashmasks to be lower value than the market price for the Mask vault on Sushiswap. The user deposits these 3 Hashmasks and sells their 3 minted MASK tokens on Sushiswap, lowering its price and aiding price discovery.

The above process will continue until a floor price is achieved.

#### Eligibilities

The Mask vault allows any Hashmask to be deposited, however other vaults use an eligibility list that only allows a specific sub-category of NFTs to be deposited. For example, the Punk-Female vault has an eligibility list that includes only female CryptoPunk NFT IDs. Other CryptoPunks cannot be deposited.

### Who Benefits From NFTX?

#### Collectors

NFTs in their basic form do not earn yield. However, when they are used to mint xTokens they can tap into the world of decentralized finance. Put simply, collectors can use NFTX to unlock more value from their NFTs:

* Earn protocol fees \(coming soon\)
* Earn trading fees as a liquidity provider
* Farm with stablecoins using xTokens as loan collateral

#### Content Creators

By launching on the NFTX protocol, content creators are able to earn protocol fees in perpetuity \(coming soon\) whilst also improving the reach and fairness of distribution:

* Earn protocol fees \(coming soon\)
* Distribute NFTs via an AMM in the form of xTokens
* Create instantly liquid markets for new content

#### Investors

NFTs are typically highly illiquid and difficult to price. NFTX makes speculating and investing in the NFT market a far simpler process:

* Access the most liquid markets for NFTs
* Track the price of particular categories of NFT





