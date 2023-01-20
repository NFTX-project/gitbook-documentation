---
description: >-
  Use the NFTX protocol to access liquidity for NFT buys and sells within
  marketplaces and aggregators
---

# 🧹 Integrations

NFTX is an NFT liquidity protocol that can be integrated into other NFT marketplace or NFT aggregator (both [Gem](https://gem.xyz) and [Uniswap](https://app.uniswap.org/#/nfts) have already integrated with NFTX).

The steps for displaying the items on your NFT marketplace include

1. Fetch NFTX vaults and their NFT holdings & fee settings
2. Check the price of buy/sell of those tokens on 0xProtocol for and ETH price
3. Call the 0xMarketplaceZap to perform the buy/sell (or the mint (sell) or redeem (buy) functions)

You can make a [single request to retrieve all vault data](integrations.md#return-all-data-from-all-nft-vault-collections) from NFTX, or you can make [individual requests](integrations.md#all-collection-details-from-a-single-vault) depending on your requirements.

{% hint style="info" %}
Vault tokens have a 1:1 relationship with the NFTs within the vault.&#x20;

* Adding an NFT to the vault, a vault token (vToken) is minted.
* Removing an NFT from the vault, a vToken is burned

Retrieving items from the vault, or buying NFTs, requires the 1 token to be burned plus the fees associated with the buy. Likewise, adding an item will return a vToken minus the fees associated with the sell.
{% endhint %}

## Example marketplace integration

These are the pseudo steps to integrate NFTX NFTs and liquidity into your application

1. Retrieve all NFTX vaults from the subgraph, including global fees, and holdings
2. Use the `asset > id` in the subgraph response to link the NFTX vault with the appropriate NFT collection in your application
3. Verify that the vault has `features > enableTargetRedeems` set to `true` so specific NFTs can be bought from the vault.
4. Check if the vault uses default fees using `usesFactoryFees` , if `true` use the global fees to calculate the tokens required to buy an NFT, if `false` use the `fees > targetRedeemFee` associated with the vault. To buy an NFT you need 1 token + target redeem fee.
5. Using the 0xAPI, check the ETH cost to buy the required tokens. As the number of tokens required increases (i.e. the user adds more items to their basket) the average price of the NFT will increase due to price impact on the token buy.
6. When the user buys, call the `0xMarketplaceZap` to complete the purchase, or alternatively call your own contracts to buy the token, redeem the NFTs using the `redeemTo` function on the vault contract.
7. For realtime updates on holdings, you can request individual vault holdings.

## API endpoints

The NFTX V2 subgraph is a GraphQL endpoint that is hosted on The Graph. It can be accessed for free through the existing hosted service, and also through The Graph Studio which is a decentralised endpoint supported by a number of indexers.

When making a request is will be a `POST` request and the endpoint URL will always remain the same, while the the body of the request will change depending on the data you require.

### NFTX Graph Endpoints

**Hosted service graph endpoint**: [https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2](https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2)

**Decentralised Studio endpoint**: [https://gateway.thegraph.com/api/\[api-key\]/subgraphs/id/4gZf3atMXjYDh4g48Zr83NFX3rkvZED86VqMNhgEXgLc](https://gateway.thegraph.com/api/\[api-key]/subgraphs/id/4gZf3atMXjYDh4g48Zr83NFX3rkvZED86VqMNhgEXgLc)

**Studio Playground**: [https://thegraph.com/explorer/subgraphs/4gZf3atMXjYDh4g48Zr83NFX3rkvZED86VqMNhgEXgLc?view=Playground](https://thegraph.com/explorer/subgraphs/4gZf3atMXjYDh4g48Zr83NFX3rkvZED86VqMNhgEXgLc?view=Playground)

{% hint style="info" %}
An API key is required when making requests through the decentralised studio. Each request costs around 0.0005 GRT and you recieve free credits when you first sign up for a developer key.
{% endhint %}

{% hint style="warning" %}
The Graph Hosted service is being decomissioned in Q1 of 2023 and the only way to access the subgraphs will be through the new decentralised studio.
{% endhint %}

A few notes about making requests to the Subgraph

* Requests are always POST and the body of the request will define the response
* Reponses from GraphQL are always `200` success responses, even when the request fails. See below for the response from an incorrect query sent

{% code title="200 response from a misformed request body" %}
```json
{
    "errors": [
        {
            "locations": [
                {
                    "column": 1,
                    "line": 1
                }
            ],
            "message": "Unexpected `not[Name]`\nExpected `{`, `query`, `mutation`, `subscription` or `fragment`"
        }
    ]
}
```
{% endcode %}

### 0x Protocol Endpoints

The 0x endpoint is used to check the price for buying the tokens required to redeem NFTs from the NFTX vaults.

The price endpoint allows you to get the current price for displaying on the front end. Once someone adds an item to their basket to purchase you want to make another call to the `quote` endpoint to get the call data.

{% code title="GET request for pricing" overflow="wrap" %}
```url
https://api.0x.org/swap/v1/price?buyToken=0x269616D549D7e8Eaa82DFb17028d0B212D11232A&sellToken=WETH&buyAmount=1030000000000000000
```
{% endcode %}

{% code title="GET quote request for buying/selling" overflow="wrap" %}
```url
https://api.0x.org/swap/v1/quote?buyToken=0x269616D549D7e8Eaa82DFb17028d0B212D11232A&sellToken=WETH&buyAmount=1030000000000000000
```
{% endcode %}

## NFTX Graph requests

### Return all data from all NFT vault collections

The below request body returns all the data you need to include every collection within NFTX into your marketplace or aggregator. To increase response times and lower the response size you can remove any data points that are not required for your particular implementation.

Data requests for a specific vault can be found below.

#### Request

{% code title="Request URL" %}
```
https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2
```
{% endcode %}

{% code title="GraphQL Query" %}
```graphql
{
  globals {
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
  }
  vaults(
    first: 1000
    where: { vaultId_gte: 0, isFinalized: true, totalHoldings_gt: 0, shutdownDate: "0"  }
  ) {
    vaultId
    id
    is1155
    isFinalized
    totalHoldings
    totalMints
    totalRedeems
    totalFees
    totalSwaps
    createdAt
    shutdownDate
    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {
      id
      tokenId
      amount
      dateAdded
    }
    token {
      id
      name
      symbol
    }
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
    usesFactoryFees
    asset {
      id
      name
      symbol
    }
    eligibilityModule {
      id
      name
      eligibleIds
      eligibleRange
    }
    features {
      enableMint
      enableRandomRedeem
      enableTargetRedeem
      enableRandomSwap
      enableTargetSwap
    }
  }
}

```
{% endcode %}



{% hint style="info" %}
The above request body is what the NFTX V2 frontend uses to retrieve all the required data to build out the homepage of the app. You should use a combination of requests to the subgraph to retrieve the data as needed for your own marketplace or aggregator setup. \


Additional [request examples](integrations.md#example-requests) are found below.
{% endhint %}

#### Response

Below is a breakdown of the response from the request response.

#### globals -> fees

These are the default fee's that are set for the NFTX protocol. If a vault returns `usesFactoryFees: true` then the globals fees are used for items within that vault. This is true even if the vault returns alternative fees.

{% code title="Example response for global fees" lineNumbers="true" %}
```json
"globals": [
            {
                "fees": {
                    "mintFee": "100000000000000000",
                    "randomRedeemFee": "40000000000000000",
                    "targetRedeemFee": "60000000000000000",
                    "randomSwapFee": "40000000000000000",
                    "targetSwapFee": "100000000000000000"
                }
            }
        ],
```
{% endcode %}

The response is defined in wei and shows&#x20;

* `fees` : Contains the differnt global fee settings.
  * `mintFee`: Selling an item on NFTX. The current default is 10%, or 0.1 token
  * `randomRedeemFee`: Buying a random NFT from the vault. Default is 4% or 0.04 token
  * `targetRedeemFee`: Buying a specific NFT from the vault. Default is 6% of 0.06 token
  * `randomSwapFee`: Swapping an existing item in your wallet with a random item in the vault. Default is 4% or 0.04 token
  * `targetSwapFee`: Swapping an exisitng item in your wallet with a specific NFT in the vault. Default is 10% or 0.1 token

{% hint style="info" %}
Some vaults will not allow all vault features like targetRedeem, targetSwap even though there are fees set globally. See below the details defined in `features`
{% endhint %}

#### vaults

* `vaultId`: The squential number of the vault created on NFTX.
* `id`: the token contract address
* `is1155`: Defines if the collection is an ERC1155 collection. If `false` the collection will be ER721, if `true` is an 1155 collection.
* `isFinalized`: If set to `true` the vault details can not be updated unless going through a governance process and a vote through Aragon. There is a `where` clause on the request to set `isFinalized: true` so only finalised vaults are returned in this request.
* `totalHoldings`: The total number of NFTs inside the vault. For 1155's this counts the total number of NFTs, not the total individual NFT `tokenId` numbers.
* `totalMints`: total number of NFTs that have been added to the vault since the vault was created. This can be through selling or staking.
* `totalRedeems`: total number of NFTs taken from the vault since the vault was created. This can be done through target buys, random buys, unstaking.
* `totalFees`: total number of fees generated on the vault through buys/sells/swaps.
* `createdAt`: the unix timestamp when the vault was created
* `shutdownDate`: If this is set to `0` the vault is still functional. If there is a value other than `0` (a unix timestamp) then the vault has been shut down and should be ignored. This is why `shutdownDate: "0"` is included in the `where` filter during the initial request.
* `holdings`: provides the first `1000` tokens held in the vault
  * `id`: the ID of the NFT
  * `tokenId`: the NFT token ID.
  * `amount`: always 1 when dealing with `ERC721` , but if the vault has `is1155: true` then there can be multiple amounts for a single token id.
  * `dateAdded`: the unix timestamp the NFT was added to the vault
* `token`: details about the vault contract/token
  * `id`: the contract address of the vault on NFTX
  * `name`: the vault name defined by the vault creator
  * `symbol`: the cash tag given to the vault
* `fees`: these fees are only valid if the following is returned `usesFactoryFees: false`
  * see definitions in the global fee response above
* `usesFactoryFees`: if this is set to `true` then the fees from the global fees section should be used and these vault specific fees should be ignored. If this is set to `false` then the fees defined against the vault fees response should be used.
* `asset`: these are the details about the NFT collection that the vault is based on
  * `id`: the contract address for the collection. You would use this to match holdings in NFTX with NFT collections displayed in your marketplace or aggregator.
  * `name`: the name of the NFT Collection - this can sometimes be the same as the vault
  * `symbol`: the symbol for the NFT collections - this can somethimes be the same as the vault
* `eligibilityModule`: this is important where vaults are set to only allow certain items. Examples include the ArtBlocks collections which are all tied to the same contract, however are differentiated by the NFT id ranges. This is only important if you are looking to allow instant sells on your platform to ensure the NFT is able to go into the vault.
* `features`: when vaults are created they can have certain features disabled. By default, all items are enabled, however for some vaults users choose to remove the ability to choose a specific item to redeem, making the vault more like a lucky dip. For each, the relevant fee is added (or removed for mints) to the transaction.
  * `enableMint`: when set to `true` this will allow users to sell NFTs into the vault.
  * `enableRandomRedeem`: when set to `true` allows users to retrieve random items from the vault.
  * `enableTargetRedeem`: when set to `true` allows users to choose item to buy from teh vault. If this is disabled, you probably don't want to list them on your marketplace or aggregator.
  * `enableRandomSwap`: when set to `true` allows users to swap an existing NFT from their wallet that is suitable for the vault with a random one in the vault.
  * `enableTargetSwap`: when set to `true` allows users to choose an item to swap out of the vault.

### All collection details from a single vault

The below request body returns all the data for a specific vault. To increase response times and lower the response size you can remove any data points that are not required for your particular implementation.

The `{ globals { fees { ... } } }` has been left in, but this could be captured once and cached as the default global fees don't change.

```graphql
{
  globals {
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
  }
  vaults(
    where: { vaultId: "297" }
  ) {
    vaultId
    id
    is1155
    totalHoldings
    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {
      id
      tokenId
      amount
      dateAdded
    }
    token {
      id
      name
      symbol
    }
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
    usesFactoryFees
    asset {
      id
      name
      symbol
    }
    eligibilityModule {
      id
      name
      eligibleIds
      eligibleRange
    }
    features {
      enableMint
      enableRandomRedeem
      enableTargetRedeem
      enableRandomSwap
      enableTargetSwap
    }
  }
}

```

If the response shows that `totalHoldings` is more than 1000 then a follow up request containing can be made to get the next set of holdings.

```graphql
{
  vaults(
    where: { vaultId: "297" }
  ) {
    holdings(first: 1000, skip: 1000, orderBy: tokenId, orderDirection: asc) {
      id
      tokenId
      amount
      dateAdded
    }
  }
}

```

The use of `skip: 1000` will get the next set of holdings up to `2000`. You can either keep looping based on the original `totalHoldings` value, or check to see if the `holdings` array has 1000 items, and if you skip to retrieve the next set.&#x20;

Currently there are only a couple collections with more than 1000 items.

## 0x Protocol Requests

The final step is to price the buy/sell price for the NFTs. All NFTs within the vault are the same floor price. To calculate the price for each item you check the fee settings for the collection, and add that to the number of NFTs being bought. For example, on a vault with the default targetRedeem (the fee to choose an item to buy) of 6% the following tokens would be required...

| Number of NFTs | Fee | Total required |
| -------------- | --- | -------------- |
| 1              | 6%  | 1.06           |
| 2              | 6%  | 2.12           |
| 5              | 6%  | 5.30           |
| 10             | 6%  | 10.60          |

Next, you calculate the amount of ETH required to buy that number of tokens. NFTX recently switched using the 0x protocol when buying tokens through our 0xMarketplaceZap to take advantage of liquidty on any number of providers, including Uniswap V3 concentrated liquidity pools.

**Request**

{% code title="0x API Request" overflow="wrap" %}
```url
https://api.0x.org/swap/v1/price?buyToken=0x269616D549D7e8Eaa82DFb17028d0B212D11232A&sellToken=WETH&buyAmount=1030000000000000000
```
{% endcode %}

**Response**

{% code title="0x API Response" overflow="wrap" %}
```json
{
  "chainId": 1,
  "price": "66.139686266145680957",
  "estimatedPriceImpact": "2.4621",
  "value": "0",
  "gasPrice": "37000000000",
  "gas": "259700",
  "estimatedGas": "259700",
  "protocolFee": "0",
  "minimumProtocolFee": "0",
  "buyTokenAddress": "0x269616d549d7e8eaa82dfb17028d0b212d11232a",
  "buyAmount": "1030000000000000000",
  "sellTokenAddress": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
  "sellAmount": "68123876854130051385",
  "sources": [
    {
      "name": "0x",
      "proportion": "0"
    },
    {
      "name": "Uniswap",
      "proportion": "0"
    },
    {
      "name": "Uniswap_V2",
      "proportion": "0"
    },
    {
      "name": "Curve",
      "proportion": "0"
    },
    {
      "name": "Balancer",
      "proportion": "0"
    },
    {
      "name": "Balancer_V2",
      "proportion": "0"
    },
    {
      "name": "Bancor",
      "proportion": "0"
    },
    {
      "name": "BancorV3",
      "proportion": "0"
    },
    {
      "name": "mStable",
      "proportion": "0"
    },
    {
      "name": "SushiSwap",
      "proportion": "0.9231"
    },
    {
      "name": "Shell",
      "proportion": "0"
    },
    {
      "name": "DODO",
      "proportion": "0"
    },
    {
      "name": "DODO_V2",
      "proportion": "0"
    },
    {
      "name": "CryptoCom",
      "proportion": "0"
    },
    {
      "name": "Lido",
      "proportion": "0"
    },
    {
      "name": "MakerPsm",
      "proportion": "0"
    },
    {
      "name": "KyberDMM",
      "proportion": "0"
    },
    {
      "name": "Component",
      "proportion": "0"
    },
    {
      "name": "Saddle",
      "proportion": "0"
    },
    {
      "name": "Uniswap_V3",
      "proportion": "0.07692"
    },
    {
      "name": "Curve_V2",
      "proportion": "0"
    },
    {
      "name": "ShibaSwap",
      "proportion": "0"
    },
    {
      "name": "Synapse",
      "proportion": "0"
    },
    {
      "name": "Synthetix",
      "proportion": "0"
    },
    {
      "name": "Aave_V2",
      "proportion": "0"
    },
    {
      "name": "Compound",
      "proportion": "0"
    }
  ],
  "allowanceTarget": "0xdef1c0ded9bec7f1a1670819833240f027b25eff",
  "sellTokenToEthRate": "1",
  "buyTokenToEthRate": "0.01550116240807967",
  "expectedSlippage": null
}
```
{% endcode %}



## Example requests

<details>

<summary>Fetch global fees</summary>

{% code title="GraphQL request" %}
```graphql
{
  globals {
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
  }
}
```
{% endcode %}

{% code title="cURL request" overflow="wrap" %}
```bash
curl --location --request POST 'https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"{\n  globals {\n    fees {\n      mintFee\n      randomRedeemFee\n      targetRedeemFee\n      randomSwapFee\n      targetSwapFee\n    }\n  }\n}\n","variables":{}}'
```
{% endcode %}

</details>

<details>

<summary>Fetch all active vault ids with more than one item</summary>

{% code title="GraphQL request" %}
```graphql
{
  vaults(
    first: 1000
    where: { isFinalized: true, totalHoldings_gt: 0, shutdownDate: "0" }
  ) {
    vaultId
  }
}

```
{% endcode %}

{% code title="cURL request" overflow="wrap" %}
```bash
curl --location --request POST 'https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"{\n  vaults(\n    first: 1000\n    where: { isFinalized: true, totalHoldings_gt: 0, shutdownDate: \"0\" }\n  ) {\n    vaultId\n  }\n}\n","variables":{}}'
```
{% endcode %}

</details>

<details>

<summary>Fetch single vault details</summary>

The `{vaultId}` can be pulled from response on the Fetch all active vault ids request above, i.e. "0" is the CryptoPunks vault, and "1" is the Avastar vault.&#x20;

{% code title="GraphQL request" %}
```graphql
{
  vaults(
    first: 1000
    where: { vaultId: "{vaultId}" }
  ) {
    vaultId
    id
    is1155
    totalHoldings
    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {
      id
      tokenId
      amount
      dateAdded
    }
    token {
      id
      name
      symbol
    }
    fees {
      mintFee
      randomRedeemFee
      targetRedeemFee
      randomSwapFee
      targetSwapFee
    }
    usesFactoryFees
    asset {
      id
      name
      symbol
    }
    eligibilityModule {
      id
      name
      eligibleIds
      eligibleRange
    }
    features {
      enableMint
      enableRandomRedeem
      enableTargetRedeem
      enableRandomSwap
      enableTargetSwap
    }
  }
}

```
{% endcode %}

{% code title="cURL request" overflow="wrap" %}
```bash
curl --location --request POST 'https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"{\n  globals {\n    fees {\n      mintFee\n      randomRedeemFee\n      targetRedeemFee\n      randomSwapFee\n      targetSwapFee\n    }\n  }\n  vaults(\n    first: 1000\n    where: { vaultId: \"0\" }\n  ) {\n    vaultId\n    id\n    is1155\n    totalHoldings\n    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {\n      id\n      tokenId\n      amount\n      dateAdded\n    }\n    token {\n      id\n      name\n      symbol\n    }\n    fees {\n      mintFee\n      randomRedeemFee\n      targetRedeemFee\n      randomSwapFee\n      targetSwapFee\n    }\n    usesFactoryFees\n    asset {\n      id\n      name\n      symbol\n    }\n    eligibilityModule {\n      id\n      name\n      eligibleIds\n      eligibleRange\n    }\n    features {\n      enableMint\n      enableRandomRedeem\n      enableTargetRedeem\n      enableRandomSwap\n      enableTargetSwap\n    }\n  }\n}\n","variables":{}}'


```
{% endcode %}

</details>

<details>

<summary>Fetch singe vault holdings</summary>

The `{vaultId}` can be pulled from response on the Fetch all active vault ids request above, i.e. "0" is the CryptoPunks vault, and "1" is the Avastar vault.&#x20;

{% code title="GraphQL request" %}
```graphql
{
  vaults(
    where: { vaultId: "{vaultId}" }
  ) {
    totalHoldings
    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {
      id
      tokenId
      amount
      dateAdded
    }
  }
}

```
{% endcode %}

{% code title="cURL request" overflow="wrap" %}
```bash
curl --location --request POST 'https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"{\n  vaults(\n    where: { vaultId: \"0\" }\n  ) {\n    totalHoldings\n    holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {\n      id\n      tokenId\n      amount\n      dateAdded\n    }\n  }\n}","variables":{}}'
```
{% endcode %}

</details>

