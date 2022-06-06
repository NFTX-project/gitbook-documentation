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
```
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
```
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
