---
description: Requesting data from the NFTX Subgraph.
---

# Subgraph Sample Request

The NFTX app is powered by a combination of Web3 calls for realtime data (token prices, connected wallet holdings etc) and calls to [The Graph](https://thegraph.com/en/) for the data that can't easily be requested from the blockchain.

Below are some common requests that you can make to the NFTX V2 subgraph to retrieve data about the vaults and their holdings.

### NFTX V2 Subgraph Endpoint

You can make `POST` requests to the following endpoint.

`http://api.thegraph.com/subgraphs/name/nftx-project/nftx-v2`

### Global Fees

This requests returns the global fees (default fees) that are applied to all vaults. The vaults have their own fees also applied to them so check what the `usesFactoryFees` is set. If it is set to `true` then the global fees are used, if it is set to `false` then the fees defined on the vault are used.

{% tabs %}
{% tab title="Request" %}
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
{% endtab %}

{% tab title="Response" %}
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
                    "targetSwapFee": "60000000000000000"
                }
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### Retrieve first 10 Published Vaults with Holdings

This request returns the first 10 vaults that have been finalised and have more than `0` NFTs in the holdings. To get all vaults change the `first: 10` to `first: 1000` and loop the request as nescessary (currently there are less than 1000 vaults so no loops required).

{% tabs %}
{% tab title="Request" %}
```graphql
{
  vaults(
    first: 10
    where: { vaultId_gte: 0, isFinalized: true, totalHoldings_gt: 0 }
  ) {
    vaultId
    token {
      id
      name
      symbol
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "data": {
        "vaults": [
            {
                "vaultId": "297",
                "token": {
                    "id": "0x00c4a73f10b05228c64e971cf81ae84426a64780",
                    "name": "MineablePunks",
                    "symbol": "MPUNK"
                }
            },
            {
                "vaultId": "370",
                "token": {
                    "id": "0x00d0a61c5cb78f236a715fe08a6bb4a72514f460",
                    "name": "R0N1 World",
                    "symbol": "RONI"
                }
            },
            {
                "vaultId": "220",
                "token": {
                    "id": "0x0115bd305885999562d593c94328fe25190dbc90",
                    "name": "EtherGals",
                    "symbol": "ETHGAL"
                }
            },
            {
                "vaultId": "379",
                "token": {
                    "id": "0x011671956844f31620bb8b9709f32230186a307a",
                    "name": "Turtle Town",
                    "symbol": "TRTL"
                }
            },
            {
                "vaultId": "131",
                "token": {
                    "id": "0x01b0b287f784ccd19cf0a7c11127a70963fd9d30",
                    "name": "Party Penguins",
                    "symbol": "PPENG"
                }
            },
            {
                "vaultId": "411",
                "token": {
                    "id": "0x03b1a9e8bc6cbe4beaeeac277a042a584fe0af59",
                    "name": "Goopdoods Vault",
                    "symbol": "GOOP"
                }
            },
            {
                "vaultId": "286",
                "token": {
                    "id": "0x03f80ed11125f72537b8ad25855f907f5ef53c65",
                    "name": "HoneyBadger by Robness 734 ttl",
                    "symbol": "HONEYB"
                }
            },
            {
                "vaultId": "145",
                "token": {
                    "id": "0x04c5d215401411c4f28e167b3e9e3290d1178cd8",
                    "name": "JunkYard Dogs",
                    "symbol": "JYD"
                }
            },
            {
                "vaultId": "126",
                "token": {
                    "id": "0x051218de982d91c3af03187ed3d8a0dde8231333",
                    "name": "Nice Drips",
                    "symbol": "DRIP"
                }
            },
            {
                "vaultId": "427",
                "token": {
                    "id": "0x055c4497506ee438c6f7a73a8750561d4a334712",
                    "name": "Rebel's Haunted Mansion",
                    "symbol": "REBEL"
                }
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### Single Vault Details

If you want all the details for a single vault you can pass across the `vaultId` as an argument

{% tabs %}
{% tab title="Request" %}
```graphql
{
  vaults(
    first: 1000
    where: { vaultId: 0 }
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
{% endtab %}

{% tab title="Response" %}
```json
{
    "data": {
        "vaults": [
            {
                "vaultId": "0",
                "id": "0x269616d549d7e8eaa82dfb17028d0b212d11232a",
                "is1155": false,
                "isFinalized": true,
                "totalHoldings": "147",
                "totalMints": "341",
                "totalRedeems": "194",
                "totalFees": "6599999999999999000",
                "totalSwaps": "193",
                "createdAt": "1624265437",
                "token": {
                    "id": "0x269616d549d7e8eaa82dfb17028d0b212d11232a",
                    "name": "CryptoPunks",
                    "symbol": "PUNK"
                },
                "fees": {
                    "mintFee": "50000000000000000",
                    "randomRedeemFee": "20000000000000000",
                    "targetRedeemFee": "30000000000000000",
                    "randomSwapFee": "20000000000000000",
                    "targetSwapFee": "30000000000000000"
                },
                "usesFactoryFees": false,
                "asset": {
                    "id": "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb",
                    "name": "CRYPTOPUNKS",
                    "symbol": "Ͼ"
                },
                "manager": {
                    "id": "0x0000000000000000000000000000000000000000"
                },
                "createdBy": {
                    "id": "0x3fce5449c7449983e263227c5aaeacb4a80b87c9"
                },
                "eligibilityModule": null,
                "features": {
                    "enableMint": true,
                    "enableRandomRedeem": true,
                    "enableTargetRedeem": true,
                    "enableRandomSwap": true,
                    "enableTargetSwap": true
                },
                "inventoryStakingPool": {
                    "id": "0x08765c76c758da951dc73d3a8863b34752dd76fb",
                    "dividendToken": {
                        "symbol": "xPUNK"
                    }
                },
                "lpStakingPool": {
                    "id": "0xfb2f1c0e0086bcef24757c3b9bfe91585b1a280f",
                    "stakingToken": {
                        "id": "0x0463a06fbc8bf28b3f120cd1bfc59483f099d332"
                    }
                },
                "holdings": [
                    {
                        "tokenId": "197"
                    },
                    {
                        "tokenId": "402"
                    },
                    {
                        "tokenId": "441"
                    },
                    {
                        "tokenId": "548"
                    },
                    {
                        "tokenId": "669"
                    },
                    {
                        "tokenId": "675"
                    },
                    {
                        "tokenId": "680"
                    },
                    {
                        "tokenId": "743"
                    },
                    {
                        "tokenId": "1011"
                    },
                    {
                        "tokenId": "1071"
                    },
                    {
                        "tokenId": "1109"
                    },
                    {
                        "tokenId": "1194"
                    },
                    {
                        "tokenId": "1254"
                    },
                    {
                        "tokenId": "1322"
                    },
                    {
                        "tokenId": "1345"
                    },
                    {
                        "tokenId": "1350"
                    },
                    {
                        "tokenId": "1436"
                    },
                    {
                        "tokenId": "1461"
                    },
                    {
                        "tokenId": "1482"
                    },
                    {
                        "tokenId": "1628"
                    },
                    {
                        "tokenId": "1713"
                    },
                    {
                        "tokenId": "1813"
                    },
                    {
                        "tokenId": "1893"
                    },
                    {
                        "tokenId": "1927"
                    },
                    {
                        "tokenId": "1940"
                    },
                    {
                        "tokenId": "2043"
                    },
                    {
                        "tokenId": "2170"
                    },
                    {
                        "tokenId": "2197"
                    },
                    {
                        "tokenId": "2233"
                    },
                    {
                        "tokenId": "2286"
                    },
                    {
                        "tokenId": "2339"
                    },
                    {
                        "tokenId": "2398"
                    },
                    {
                        "tokenId": "2447"
                    },
                    {
                        "tokenId": "2511"
                    },
                    {
                        "tokenId": "2522"
                    },
                    {
                        "tokenId": "2557"
                    },
                    {
                        "tokenId": "2575"
                    },
                    {
                        "tokenId": "2595"
                    },
                    {
                        "tokenId": "2629"
                    },
                    {
                        "tokenId": "2733"
                    },
                    {
                        "tokenId": "2791"
                    },
                    {
                        "tokenId": "2808"
                    },
                    {
                        "tokenId": "2837"
                    },
                    {
                        "tokenId": "2907"
                    },
                    {
                        "tokenId": "2941"
                    },
                    {
                        "tokenId": "3050"
                    },
                    {
                        "tokenId": "3067"
                    },
                    {
                        "tokenId": "3082"
                    },
                    {
                        "tokenId": "3118"
                    },
                    {
                        "tokenId": "3143"
                    },
                    {
                        "tokenId": "3235"
                    },
                    {
                        "tokenId": "3241"
                    },
                    {
                        "tokenId": "3257"
                    },
                    {
                        "tokenId": "3453"
                    },
                    {
                        "tokenId": "3527"
                    },
                    {
                        "tokenId": "3610"
                    },
                    {
                        "tokenId": "3627"
                    },
                    {
                        "tokenId": "3789"
                    },
                    {
                        "tokenId": "4011"
                    },
                    {
                        "tokenId": "4050"
                    },
                    {
                        "tokenId": "4064"
                    },
                    {
                        "tokenId": "4091"
                    },
                    {
                        "tokenId": "4195"
                    },
                    {
                        "tokenId": "4306"
                    },
                    {
                        "tokenId": "4348"
                    },
                    {
                        "tokenId": "4357"
                    },
                    {
                        "tokenId": "4406"
                    },
                    {
                        "tokenId": "4455"
                    },
                    {
                        "tokenId": "4486"
                    },
                    {
                        "tokenId": "4493"
                    },
                    {
                        "tokenId": "4496"
                    },
                    {
                        "tokenId": "4546"
                    },
                    {
                        "tokenId": "4563"
                    },
                    {
                        "tokenId": "4643"
                    },
                    {
                        "tokenId": "4875"
                    },
                    {
                        "tokenId": "4912"
                    },
                    {
                        "tokenId": "4930"
                    },
                    {
                        "tokenId": "4933"
                    },
                    {
                        "tokenId": "4951"
                    },
                    {
                        "tokenId": "5067"
                    },
                    {
                        "tokenId": "5254"
                    },
                    {
                        "tokenId": "5354"
                    },
                    {
                        "tokenId": "5462"
                    },
                    {
                        "tokenId": "5467"
                    },
                    {
                        "tokenId": "5516"
                    },
                    {
                        "tokenId": "5703"
                    },
                    {
                        "tokenId": "5766"
                    },
                    {
                        "tokenId": "5821"
                    },
                    {
                        "tokenId": "5881"
                    },
                    {
                        "tokenId": "5945"
                    },
                    {
                        "tokenId": "5962"
                    },
                    {
                        "tokenId": "5999"
                    },
                    {
                        "tokenId": "6028"
                    },
                    {
                        "tokenId": "6193"
                    },
                    {
                        "tokenId": "6276"
                    },
                    {
                        "tokenId": "6335"
                    },
                    {
                        "tokenId": "6341"
                    },
                    {
                        "tokenId": "6434"
                    },
                    {
                        "tokenId": "6561"
                    },
                    {
                        "tokenId": "6584"
                    },
                    {
                        "tokenId": "6603"
                    },
                    {
                        "tokenId": "6646"
                    },
                    {
                        "tokenId": "6772"
                    },
                    {
                        "tokenId": "6804"
                    },
                    {
                        "tokenId": "6997"
                    },
                    {
                        "tokenId": "7032"
                    },
                    {
                        "tokenId": "7054"
                    },
                    {
                        "tokenId": "7281"
                    },
                    {
                        "tokenId": "7304"
                    },
                    {
                        "tokenId": "7486"
                    },
                    {
                        "tokenId": "7608"
                    },
                    {
                        "tokenId": "7626"
                    },
                    {
                        "tokenId": "7628"
                    },
                    {
                        "tokenId": "7754"
                    },
                    {
                        "tokenId": "7957"
                    },
                    {
                        "tokenId": "8054"
                    },
                    {
                        "tokenId": "8089"
                    },
                    {
                        "tokenId": "8150"
                    },
                    {
                        "tokenId": "8208"
                    },
                    {
                        "tokenId": "8308"
                    },
                    {
                        "tokenId": "8331"
                    },
                    {
                        "tokenId": "8409"
                    },
                    {
                        "tokenId": "8444"
                    },
                    {
                        "tokenId": "8470"
                    },
                    {
                        "tokenId": "8538"
                    },
                    {
                        "tokenId": "8542"
                    },
                    {
                        "tokenId": "8730"
                    },
                    {
                        "tokenId": "8755"
                    },
                    {
                        "tokenId": "8858"
                    },
                    {
                        "tokenId": "8885"
                    },
                    {
                        "tokenId": "8922"
                    },
                    {
                        "tokenId": "9215"
                    },
                    {
                        "tokenId": "9228"
                    },
                    {
                        "tokenId": "9243"
                    },
                    {
                        "tokenId": "9364"
                    },
                    {
                        "tokenId": "9370"
                    },
                    {
                        "tokenId": "9386"
                    },
                    {
                        "tokenId": "9442"
                    },
                    {
                        "tokenId": "9490"
                    },
                    {
                        "tokenId": "9620"
                    },
                    {
                        "tokenId": "9747"
                    },
                    {
                        "tokenId": "9815"
                    },
                    {
                        "tokenId": "9846"
                    },
                    {
                        "tokenId": "9887"
                    },
                    {
                        "tokenId": "9903"
                    },
                    {
                        "tokenId": "9924"
                    },
                    {
                        "tokenId": "9956"
                    }
                ]
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### NFTX App Request

While there are a number of requests made to the subgraph to run the NFTX site the main request most integrations require is to retrieve all current vaults with the available NFTs available for purchase, and the facility to calculate the price.

This uses a combination of all the requests listed above.

{% tabs %}
{% tab title="Request" %}
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
{% endtab %}

{% tab title="Response" %}
```
// response truncated for brevity.
{
    "data": {
        "globals": [
            {
                "fees": {
                    "mintFee": "100000000000000000",
                    "randomRedeemFee": "40000000000000000",
                    "targetRedeemFee": "60000000000000000",
                    "randomSwapFee": "40000000000000000",
                    "targetSwapFee": "60000000000000000"
                }
            }
        ],
        "vaults": [
            {
                "vaultId": "297",
                "id": "0x00c4a73f10b05228c64e971cf81ae84426a64780",
                "is1155": false,
                "isFinalized": true,
                "totalHoldings": "38",
                "totalMints": "47",
                "totalRedeems": "9",
                "totalFees": "2440000000000000000",
                "totalSwaps": "0",
                "createdAt": "1639894659",
                "holdings": [
                    {
                        "id": "0x276c-0x00c4a73f10b05228c64e971cf81ae84426a64780",
                        "tokenId": "10092",
                        "amount": "1",
                        "dateAdded": "1646022345"
                    },
                    {
                    ...37 more nfts listed here....
                    }
                ],
                "token": {
                    "id": "0x00c4a73f10b05228c64e971cf81ae84426a64780",
                    "name": "MineablePunks",
                    "symbol": "MPUNK"
                },
                "fees": {
                    "mintFee": "100000000000000000",
                    "randomRedeemFee": "50000000000000000",
                    "targetRedeemFee": "100000000000000000",
                    "randomSwapFee": "50000000000000000",
                    "targetSwapFee": "100000000000000000"
                },
                "usesFactoryFees": true,
                "asset": {
                    "id": "0x595a8974c1473717c4b5d456350cd594d9bda687",
                    "name": "MineablePunks",
                    "symbol": "MPUNKS"
                },
                "manager": {
                    "id": "0x0000000000000000000000000000000000000000"
                },
                "createdBy": {
                    "id": "0x33569c101562e1faf5b24581057e5cee4c8288d7"
                },
                "eligibilityModule": null,
                "features": {
                    "enableMint": true,
                    "enableRandomRedeem": true,
                    "enableTargetRedeem": true,
                    "enableRandomSwap": true,
                    "enableTargetSwap": true
                },
                "inventoryStakingPool": {
                    "id": "0x013cf78239144abcf06bbd56d3d190c65d7f9635",
                    "dividendToken": {
                        "symbol": "xMPUNK"
                    }
                },
                "lpStakingPool": {
                    "id": "0xfda2d4ea96ae4c6c21b34ec4e607576163a55ec0",
                    "stakingToken": {
                        "id": "0xe7d5d6b7d3a3c70174d6b567697287a3322c4789"
                    }
                }
            },
            .... more vaults.....
            ] 
        }
    }
```
{% endtab %}
{% endtabs %}
