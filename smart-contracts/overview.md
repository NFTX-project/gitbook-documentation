# Overview

## **Deployed Contracts** 

| **Contracts** | **Code** | **Address** |
| :--- | :--- | :--- |
| **NFTXFundProxy** | [**GitHub**](https://docs.openzeppelin.com/contracts/3.x/api/proxy#UpgradeableProxy) | [**0xAf93fCce0548D3124A5fC3045adAf1ddE4e8Bf7e**](https://etherscan.io/address/0xAf93fCce0548D3124A5fC3045adAf1ddE4e8Bf7e) |
| **NFTXv7 Implementation** | [**GitHub**](https://github.com/NFTX-project/x-contracts-private/blob/master/contracts/NFTXv7.sol) | [**0x87665c29ea77c4285ea7443f5f71c54ea90305b8**](https://etherscan.io/address/0x87665c29ea77c4285ea7443f5f71c54ea90305b8#code) |
| **xStore** | [**GitHub**](https://github.com/NFTX-project/x-contracts/blob/master/contracts/XStore.sol) | [**0xBe54738723cea167a76ad5421b50cAa49692E7B7**](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7) |
| **$NFTX Token** | [**GitHub**](https://github.com/aragon/minime/blob/master/contracts/MiniMeToken.sol) | [**0x87d73e916d7057945c9bcd8cdd94e42a6f47f776**](https://etherscan.io/address/0x87d73e916d7057945c9bcd8cdd94e42a6f47f776) |
| **Bounties** | [**GitHub**](https://github.com/NFTX-project/x-bounties/blob/master/contracts/XBouties.sol) | [**0x9C5a36AEf5A7b04b0123b2064BD20bc47183e1DC**](https://etherscan.io/address/0x9C5a36AEf5A7b04b0123b2064BD20bc47183e1DC) |
| **DAO** | [**GitHub**](https://github.com/NFTX-project/x-contracts/blob/master/contracts/XController.sol) | [**0x40d73df4f99bae688ce3c23a01022224fe16c7b2**](https://etherscan.io/address/0x40d73df4f99bae688ce3c23a01022224fe16c7b2) |
| **TokenApp** | [**GitHub**](https://github.com/NFTX-project/x-bounties/blob/master/contracts/TokenAppController.sol) | [**0x5566b3e5fc300a1b28c214b49a5950c34d00eb33**](https://etherscan.io/address/0x5566b3e5fc300a1b28c214b49a5950c34d00eb33) |
| **xStoreMultiCall** | [**GitHub**](https://github.com/NFTX-project/x-backend/blob/master/contracts/XStoreMultiCall.json) | [**0x0ccA025C7b8C264F7a569afF1A74907CD43AeD62**](https://etherscan.io/address/0x0ccA025C7b8C264F7a569afF1A74907CD43AeD62) |
| **TokenMultiCall** | [**GitHub**](https://github.com/NFTX-project/x-backend/blob/master/contracts/TokenMultiCall.json) | [**0xd62b2DD08FCA73B82f014107bF1CC888C61b8dF3**](https://etherscan.io/address/0xd62b2DD08FCA73B82f014107bF1CC888C61b8dF3) |
| **ProxyController** | [**GitHub**](https://github.com/NFTX-project/x-contracts/blob/master/contracts/ProxyController.sol) | [**0x947c0bfA2bf3Ae009275f13F548Ba539d38741C2**](https://etherscan.io/address/0x947c0bfA2bf3Ae009275f13F548Ba539d38741C2) |
| **xTokenClonable** | [**GitHub**](https://github.com/NFTX-project/x-contracts-private/blob/master/contracts/XTokenClonable.sol) | [**0x925297edcb4893d0d914e6d28f49381d47b864b0**](https://etherscan.io/address/0x925297edcb4893d0d914e6d28f49381d47b864b0) |

## Contract User Interfaces

**Mainnet:** https://nftx.org/#backend/
**Rinkeby:** https://rinkeby.nftx.org/#/backend/

## **NFTX Interfaces**

**Source code:** [**https://github.com/NFTX-project/x-frontend/blob/master/src/contracts/NFTXv7.json**](https://github.com/NFTX-project/x-frontend/blob/master/src/contracts/NFTXv7.json)

### **NFTX Contracts**

#### **Structure Summary** 

At the core of NFTX is the NFTX Fund contract which holds all NFTs stored by all various NFTX funds. The NFTX Fund contract maintains a vault per NFT address identified with a vault ID. Using the vault ID, the NFTX Fund contract accesses all fund/vault related storage through the xStore contract.

For every vault, there is a fund token \(xToken\) deployed for it, which is eligible for redeeming a pseudorandom NFT from the fund.

### \*\*\*\*[**NFTXv7 Implementation**](https://etherscan.io/address/0x87665c29ea77c4285ea7443f5f71c54ea90305b8)\*\*\*\*

#### **Vault Creation**

```javascript
function createVault(
    string memory name,
    string memory symbol,
    address _assetAddress,
    bool _isD2Vault
) public virtual nonReentrant returns (uint256 vaultId);
```

Anyone can create a vault by calling `createVault`. When a vault is made, a fund token \(xToken\) is deployed, and the vault ID is returned.

#### **Minting**

```javascript
function mint(uint256 vaultId, uint256[] memory nftIds, uint256 d2Amount) external;
```

The mint function allows you to mint an xToken for each NFT provided to the fund.

This function expects the contract to have approval of the NFTs or set as an operator from `msg.sender`.

#### **Redeeming**

```javascript
function redeem(uint256 vaultId, uint256 amount) external;
```

The redeem function allows users to use their NFTX Fund tokens to redeem NFTs pseudorandomly from the proper vault. 

This function expects the contract to have approval of the NFTX Fund token by the `msg.sender`.

#### **xToken \(Fund Tokens\)**

For every fund on NFTX, an xToken proxy clone contract is deployed to serve as the means of minting/redeeming through that fund. Every xToken is a standard ERC20.

### \*\*\*\*[**xStore**](https://etherscan.io/address/0xBe54738723cea167a76ad5421b50cAa49692E7B7)\*\*\*\*

Using the vault ID, you can access vault information from xStore using the following view functions:

#### **Reading the vaults parameters**

```javascript
function xTokenAddress(uint256 vaultId) external view returns (address);
function assetAddress(uint256 vaultId) external view returns (address);
```

The xToken address represents the token that is minted/redeemed for the assets in that vault ID. This is also referred to as the fund token.

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

It takes as argument a vaultId and it checks if the vault is finalized or not, if it's finalized only the [owner](#permissioning) can continue forward otherwise only the [manager](#permissioning) can call it.

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

