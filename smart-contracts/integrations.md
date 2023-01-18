---
description: >-
  Use the NFTX protocol to access NFT liquidity for buys and sells within
  Marketplaces and Aggregators
---

# 🧹 Integrations

NFTX is an NFT liquidity protocl that can be easily integrated into your own NFT Marketplace or NFT Aggregator.

### Return all vault collections from NFTX

{% swagger method="post" path="" baseUrl="https://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2" summary="Fetch all NFTX Vaults" expanded="false" %}
{% swagger-description %}
This returns a list of all the current NFTX vaults that are published and contain at least one item.
{% endswagger-description %}

{% swagger-parameter in="body" type="{   globals {     fees {       mintFee       randomRedeemFee       targetRedeemFee       randomSwapFee       targetSwapFee     }   }   vaults(     first: 1000     where: { vaultId_gte: 0, isFinalized: true, totalHoldings_gt: 0 }   ) {     vaultId     id     is1155     isFinalized     totalHoldings     totalMints     totalRedeems     totalFees     totalSwaps     createdAt     shutdownDate     holdings(first: 1000, orderBy: tokenId, orderDirection: asc) {       id       tokenId       amount       dateAdded     }     token {       id       name       symbol     }     fees {       mintFee       randomRedeemFee       targetRedeemFee       randomSwapFee       targetSwapFee     }     usesFactoryFees     asset {       id       name       symbol     }     manager {       id     }     createdBy {       id     }     eligibilityModule {       id       name       eligibleIds       eligibleRange     }     features {       enableMint       enableRandomRedeem       enableTargetRedeem       enableRandomSwap       enableTargetSwap     }     inventoryStakingPool {       id       dividendToken {         symbol       }     }     lpStakingPool {       id       stakingToken {         id       }     }   } }" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
  "data": {
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
    ]
}
```
{% endswagger-response %}
{% endswagger %}

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
    manager {
      id
    }
    createdBy {
      id
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
    inventoryStakingPool {
      id
      dividendToken {
        symbol
      }
    }
    lpStakingPool {
      id
      stakingToken {
        id
      }
    }
  }
}

```

### Return all collection holdings from an NFTX Vault





### Fetch the current buy/sell price for items within a collection

