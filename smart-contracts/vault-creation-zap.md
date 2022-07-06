# Vault Creation Zap

To assist in the creation of an NFTX vault, we created a zap that amalgamates a number of processes into a singular contract call. This call will allow you to perform the following steps:

1. Create a default vault
2. _(optional)_ Add an eligibility storage module
3. _(optional)_ Add 721 or 1155 tokens to the vault, returning tokens to the sender
4. _(optional)_ Set vault features
5. Set vault fees
6. Finalise the vault

_Please note: Due to the evolution of ERC721 support, we have chosen to exclude support for the CryptoKitties contract to save gas for the majority of users._

| Network | Contract Address |
| ------- | ---------------- |
| Mainnet | Coming soon      |

Our vault creation function takes the following attributes, each of which will be explained in this document. Upon successful creation we receive the ID of the vault that was created. This can then be subsequently referenced in our NFTX Vault Factory to get address and implementation information.

```
  function createVault(
    vaultInfo calldata vaultData,
    uint vaultFeatures,
    vaultFeesConfig calldata vaultFees,
    vaultEligibilityStorage calldata eligibilityStorage,
    vaultTokens calldata assetTokens
  ) external nonReentrant returns (uint vaultId_);
```

### vaultData

Takes a formatted struct containing basic information regarding the vault.

```
  struct vaultInfo {
    address assetAddress;
    bool is1155;
    bool allowAllItems;
    string name;
    string symbol;
  }
```

### vaultFeatures

A integer value of a binary representation of booleans. This allows us to map five boolean values, one for each optional vault feature, inside of a single parameter. The order of these booleans aligns as:

1. Allow minting to the vault
2. Allow random redemptions
3. Allow targeted redemptions
4. Enable random swaps
5. Enable targeted swaps

For example, to allow only minting inside the vault, but no redemptions or swaps, this would give a binary value of `10000` as this would equate to `true, false, false, false, false`. Converted into an integer value, this would then come out as `16`, which would be passed to the contract.

We can use `parseInt` in JS to make this conversion into an integer value simple:

```
let x = '10000';
parseInt(x, 2) // 16
```

#### Examples

| Booleans | Binary | Integer |
| -------- | ------ | ------- |
| FFFFF    | 00101  | 5       |
| TFFFF    | 10000  | 16      |
| TFTFT    | 10101  | 21      |
| TTFTT    | 11011  | 27      |
| TTTTT    | 11111  | 31      |

### vaultFees

The fees for the vault, entered in 9-decimal format.

```
  struct vaultFeesConfig {
    uint32 mintFee;
    uint32 randomRedeemFee;
    uint32 targetRedeemFee;
    uint32 randomSwapFee;
    uint32 targetSwapFee;
  }
```

### eligibilityStorage

Allows for a vault eligibility storage implementation to be specified for the vault to use. The `moduleIndex` will represent the index ID of a valid eligibility module, and the `initData` bytes will be passed to the module when initialising. More information about eligibility modules can be found [here](eligibility-modules/).

```
  struct vaultEligibilityStorage {
    int moduleIndex;
    bytes initData;
  }
```

If no module is required, then you can set a `moduleIndex` of `-1`.

### assetTokens

Tokens to be transferred to the vault to populate its initial supply. The vault tokens will be returned to the `msg.sender`.

_**Note: Tokens must all be owned and approved for the zap to use by the sender as a precursor to calling.**_

```
  struct vaultTokens {
    uint[] assetTokenIds;
    uint[] assetTokenAmounts;
  }
```

An array of token ID values that belong to the specified vault `assetAddress`, along with the amount of each token. If you're sending `ERC721` tokens, then the amount values will be ignored, though this will be required for `ERC1155` tokens to indicate how many of each token ID will be sent to the vault.

### Example Call

The below shows an example of an 1155 vault, deployed with 10 tokens across 3 different IDs. We don't have an eligibility module attached, but define features and fees.

```
  const vaultId = await vaultCreationZap.createVault(
    // Vault creation
    {
      name: 'Pace Spoggers',
      symbol: 'SPOGGERS',
      assetAddress: erc1155.address,
      is1155: true,
      allowAllItems: true
    },

    // Vault features
    26,  // 11010

    // Fee assignment
    {
      mintFee: 20000000,            // 0.2
      randomRedeemFee: 12500000,    // 0.125
      targetRedeemFee: 20000000,    // 0.2
      randomSwapFee: 15000000,      // 0.15
      targetSwapFee: 20000000       // 0.2
    },

    // Eligibility storage
    {
      moduleIndex: -1,
      initData: 0
    },

    // Mint and stake
    {
      assetTokenIds: [1, 2, 3],
      assetTokenAmounts: [2, 5, 3]
    }
  );
```
