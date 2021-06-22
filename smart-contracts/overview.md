# Overview

### **NFTX Contracts**

#### **Structure Summary**

At the core of NFTX is the NFTX Fund contract which holds all NFTs stored by all various NFTX funds. The NFTX Fund contract maintains a vault per NFT address identified with a vault ID. Using the vault ID, the NFTX Fund contract accesses all fund/vault related storage through the xStore contract.

For every vault, there is a fund token \(vToken\) deployed for it, which is eligible for redeeming a pseudorandom NFT from the fund.

### [NFTXv7 Implementation](https://etherscan.io/address/0x87665c29ea77c4285ea7443f5f71c54ea90305b8)

#### **Vault Creation**

```javascript
function createVault(
    string memory name,
    string memory symbol,
    address _assetAddress,
    bool _isD2Vault
) public virtual nonReentrant returns (uint256 vaultId);
```

Anyone can create a vault by calling `createVault`. When a vault is made, a fund token \(vToken\) is deployed, and the vault ID is returned.

#### **Minting**

```javascript
function mint(uint256 vaultId, uint256[] memory nftIds, uint256 d2Amount) external;
```

The mint function allows you to mint an vToken for each NFT provided to the fund.

This function expects the contract to have approval of the NFTs or set as an operator from `msg.sender`.

#### **Redeeming**

```javascript
function redeem(uint256 vaultId, uint256 amount) external;
```

The redeem function allows users to use their NFTX Fund tokens to redeem NFTs pseudorandomly from the proper vault.

This function expects the contract to have approval of the NFTX Fund token by the `msg.sender`.

#### **vToken \(Fund Tokens\)**

For every fund on NFTX, an vToken proxy clone contract is deployed to serve as the means of minting/redeeming through that fund. Every vToken is a standard ERC20.

### [**xStore**](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7)

Using the vault ID, you can access vault information from xStore using the following view functions:

#### **Reading the vaults parameters**

```javascript
function xTokenAddress(uint256 vaultId) external view returns (address);
function assetAddress(uint256 vaultId) external view returns (address);
```

The vToken address represents the token that is minted/redeemed for the assets in that vault ID. This is also referred to as the fund token.

The asset address is the asset used to mint fund tokens, and what is given back to the user when they redeem their fund tokens.

#### **Reading the vaults contents and information**

```javascript
function reservesLength(uint256 vaultId) external view returns (uint256);
function reservesContains(uint256 vaultId, uint256 elem) external view returns (bool);
function reservesAt(uint256 vaultId, uint256 index) external view returns (uint256);
```

A reserve defines the vault's contents, which consists of ERC721s.

You can view the total amount of assets in a vault; if an asset is present in a vault; and which asset is located at a given index.

#### **Permissioning**

Currently there are 2 distinct roles which the permission checks are based on.

**Owner:** the address who initialized the NFTX contract, the owner of the NFTX Fund contract.  
**Manager:** the address who created the vault. \(Note: every vault has its own manager.\)

There is 1 modifier and 2 functions that are used as a permission check.

#### onlyOwner

```javascript
modifier onlyOwner()
```

Only the owner can execute the functions with this modifier.

#### **onlyOwnerIfPaused**

```javascript
function onlyOwnerIfPaused(uint256 pauserId) public view virtual;
```

It takes an ID as an argument which corresponds to an action and checks if the specific action is paused or not.

If the action is paused only the owner can call the function. If it isn’t paused, it is permissionless.

As of now the actions that can be “paused” are `createVault()`, `mint()`, `redeem()`.

**The functions that use this access control are:**

```javascript
function createVault(string memory name, string memory symbol, address _assetAddress, bool _isD2Vault) public virtual nonReentrant returns (uint256 vaultId);
function requestMint(uint256 vaultId, uint256[] memory nftIds) public payable virtual override nonReentrant;
function mint(uint256 vaultId, uint256[] memory nftIds, uint256 d2Amount) public payable virtual override nonReentrant;
function redeem(uint256 vaultId, uint256 amount) public payable virtual nonReentrant;
```

#### onlyPrivileged

```javascript
function onlyPrivileged(uint256 vaultId) internal view;
```

It takes as argument a vaultId and it checks if the vault is finalized or not, if it's finalized only the [owner](overview.md#permissioning) can continue forward otherwise only the [manager](overview.md#permissioning) can call it.

**The functions that use this access control are:**

```javascript
// Configuration
function setIs1155(uint256 vaultId, bool _boolean) public virtual;
function setNegateEligibility(uint256 vaultId, bool shouldNegate) public virtual override;
function setRange(uint256 vaultId, uint256 start, uint256 end) public virtual;
function setIsEligible(uint256 vaultId, uint256[] memory nftIds, bool _boolean) public virtual;
function setMintFees(uint256 vaultId, uint256 _ethBase, uint256 _ethStep) public virtual;
function setBurnFees(uint256 vaultId, uint256 _ethBase, uint256 _ethStep) public virtual;
function setSupplierBounty(uint256 vaultId, uint256 ethMax, uint256 length) public virtual;
function setAllowMintRequests(uint256 vaultId, bool isAllowed) public virtual;
function setFlipEligOnRedeem(uint256 vaultId, bool flipElig) public virtual;
function setNegateEligibility(uint256 vaultId, bool shouldNegate) public virtual;
function approveMintRequest(uint256 vaultId, uint256[] memory nftIds) public virtual;

// Management
function changeTokenName(uint256 vaultId, string memory newName) public virtual;
function changeTokenSymbol(uint256 vaultId, string memory newSymbol) public virtual;
function setManager(uint256 vaultId, address newManager) public virtual;
function finalizeVault(uint256 vaultId) public virtual;
function closeVault(uint256 vaultId) public virtual;)
```

