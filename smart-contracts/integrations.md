---
description: >-
  Use the NFTX protocol to access NFT liquidity for buys and sells within
  Marketplaces and Aggregators
---

# 🧹 Integrations

NFTX is an NFT liquidity protocl that can be easily integrated into your own NFT marketplace or NFT aggregator.

The steps for displaying the items on your NFT marketplace include

1. Return all published vaults with at least one NFT, plus the default global fee settings
2. For each vault check&#x20;
   1.

## API endpoints

The NFTX V2 subgraph is a GraphQL endpoint that is hosted on The Graph. It can be accessed for free through the existing hosted service, and also through The Graph Studio which is a decentralised endpoint supported by a number of indexers.

When making a request is will be a `POST` request and the endpoint URL will always remain the same, while the the body of the request will change depending on the data you require.

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

## Return all data from all NFT vault collections

The below request body returns all the data you need to include every collection within NFTX into your marketplace or aggregator. To increase response times and lower the response size you can remove any data points that are not required for your particular implementation.

Data requests for a specific vault can be found below.

<details>

<summary>Example Curl Request</summary>

```bash
curl --location --request POST 'https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"{\n  globals {\n    fees {\n      mintFee\n      randomRedeemFee\n      targetRedeemFee\n      randomSwapFee\n      targetSwapFee\n    }\n  }\n  vaults(\n    first: 1000\n    where: { vaultId_gte: 0, isFinalized: true, totalHoldings_gt: 0, shutdownDate: \"0\" }\n  ) {\n    vaultId\n    id\n    is1155\n    isFinalized\n    totalHoldings\n    totalMints\n    totalRedeems\n    totalFees\n    totalSwaps\n    createdAt\n    shutdownDate\n    token {\n      id\n      name\n      symbol\n    }\n    fees {\n      mintFee\n      randomRedeemFee\n      targetRedeemFee\n      randomSwapFee\n      targetSwapFee\n    }\n    usesFactoryFees\n    asset {\n      id\n      name\n      symbol\n    }\n    eligibilityModule {\n      id\n      name\n      eligibleIds\n      eligibleRange\n    }\n    features {\n      enableMint\n      enableRandomRedeem\n      enableTargetRedeem\n      enableRandomSwap\n      enableTargetSwap\n    }\n  }\n}\n","variables":{}}'
```

</details>

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
The request body is what the NFTX V2 frontend uses to retrieve all the required data to build out the homepage of the app. You should use a combination of requests to the subgraph to retrieve the data as needed for your own marketplace or aggregator setup. \


Additional request examples are found below.
{% endhint %}

### Response

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





### Fetch the current buy/sell price for items within a collection



## Example requests

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
