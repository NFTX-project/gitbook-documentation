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



## Return all data from all NFT vault collections

The below request body returns all the data you need to include every collection within NFTX into your marketplace or aggregator. To increase response times and lower the response size you can remove any data points that are not required for your particular implementation.

Data requests for a speficic vault can be found below.

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
    where: { vaultId_gte: 0, isFinalized: true, totalHoldings_gt: 0 }
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

####

### Response

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

* **mintFee** : Selling an item on NFTX. The current default is 10%, or 0.1 token
* **randomRedeemFee:** Buying a random NFT from the vault. Default is 4% or 0.04 token
* **targetRedeemFee:** Buying a specific NFT from the vault. Default is 6% of 0.06 token
* **randomSwapFee:** Swapping an existing item in your wallet with a random item in the vault. Default is 4% or 0.04 token
* **targetSwapFee:** Swapping an exisitng item in your wallet with a specific NFT in the vault. Default is 10% or 0.1 token

{% hint style="info" %}
Some vaults will not allow all vault features like targetRedeem, targetSwap even though there are fees set globally.
{% endhint %}

#### vaults

* vaultId: The squential number of the vault created on NFTX.
* id: the token contract address
* is1155: Defines if the collection is an ERC1155 collection. If `false` the collection will be ER721, if `true` is an 1155 collection.
* isFinalized: If set to `true` the vault details can not be updated unless going through a governance process and a vote through Aragon. There is a `where` clause on the request to set `isFinalized: true` so only finalised vaults are returned in this request.
* totalHoldings: The total number of NFTs inside the vault. For 1155's this counts the total number of NFTs, not the total individual NFT `tokenId` numbers.
*

### Return all collection holdings from an NFTX Vault





### Fetch the current buy/sell price for items within a collection

