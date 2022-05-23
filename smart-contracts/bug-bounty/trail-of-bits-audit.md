# Trail of Bits Audit

{% hint style="info" %}
Below is an excerpt from the Trail of Bits Audit, however due to the formatting of the PDF report not everything have been added to the page below.

You can access the full report as a PDF directly below.


{% endhint %}

{% file src="../../.gitbook/assets/ToB_Audit.pdf" %}
Click on the link above to download the full public report of the Trail of Bits audit.
{% endfile %}

## About Trail of Bits

Founded in 2012 and headquartered in New York, Trail of Bits provides technical security assessment and advisory services to some of the world’s most targeted organizations. We combine high-end security research with a real-world attacker mentality to reduce risk and fortify code. With 80+ employees around the globe, we’ve helped secure critical software elements that support billions of end users, including Kubernetes and the Linux kernel.

We maintain an exhaustive list of publications at https://github.com/trailofbits/publications, with links to papers, presentations, public audit reports, and podcast appearances.

In recent years, Trail of Bits consultants have showcased cutting-edge research through presentations at CanSecWest, HCSS, Devcon, Empire Hacking, GrrCon, LangSec, NorthSec, the O’Reilly Security Conference, PyCon, REcon, Security BSides, and SummerCon.

We specialize in software testing and code review projects, supporting client organizations in the technology, defense, and finance industries, as well as government entities. Notable clients include HashiCorp, Google, Microsoft, Western Digital, and Zoom.

Trail of Bits also operates a center of excellence with regard to blockchain security. Notable projects include audits of Algorand, Bitcoin SV, Chainlink, Compound, Ethereum 2.0, MakerDAO, Matic, Uniswap, Web3, and Zcash.

To keep up to date with our latest news and announcements, please follow @trailofbits on Twitter and explore our public repositories at https://github.com/trailofbits. To engage us directly, visit our “Contact” page at https://www.trailofbits.com/contact, or email us at info@trailofbits.com.

## Notices and Remarks

### Copyright and Distribution

All rights reserved. Trail of Bits hereby asserts its right to be identified as the creator of this report in the United Kingdom.

This report is considered by Trail of Bits to be public information; it is licensed to NFTX under the terms of the project statement of work and has been made public at NFTX’s request. Material within this report may not be reproduced or distributed in part or in whole without the express written permission of Trail of Bits.

### Test Coverage Disclaimer

All activities undertaken by Trail of Bits in association with this project were performed in accordance with a statement of work and mutually agreed upon project plan.

Security assessment projects are time-boxed and often reliant on information that may be provided by a client, its affiliates, or its partners. As a result, the findings documented in this report should not be considered a comprehensive list of security issues, flaws, or defects in the target system or codebase.

Trail of Bits uses automated testing techniques to rapidly test the controls and security properties of software. These techniques augment our manual security review work, but each has its limitations: for example, a tool may not generate a random edge case that violates a property or may not fully complete its analysis during the allotted time. Their use is also limited by the time and resource constraints of a project.

## Executive Summary

### Engagement Overview

NFTX engaged Trail of Bits to review the security of version 2 of its protocol. From April 4 to April 15, 2022, a team of two consultants conducted a security review of the client-provided source code, with four person-weeks of effort. Details of the project’s timeline, test targets, and coverage are provided in subsequent sections of this report.

### Project Scope

Our testing efforts were focused on the identification of flaws that could result in a compromise of confidentiality, integrity, or availability of the target system. We conducted this audit with full knowledge of the target system, including access to the source code and documentation for all of the on-chain components. Off-chain code was not included in the scope of this assessment. Also, we were instructed to ignore specific files in the codebase, enumerated in the Project Coverage section.

### Summary of Findings

The audit uncovered two flaws that could impact system confidentiality, integrity, or availability. Details on these notable findings are provided below. This report also contains technical appendices. Appendix C lists code quality findings that do not necessarily have security implications. Appendix D provides guidance on redesigning the fee distribution mechanism. Finally, appendix E provides security guidance on interacting with third-party token contracts

### Notable Findings

Significant flaws that impact system confidentiality, integrity, or availability are listed below.

#### TOB-NFTX-9

The process of creating vaults in the NFTX protocol is trustless. This means that anyone can create a new vault and use any asset as the underlying vault NFT. The user calls the NFTXVaultFactoryUpgradeable contract to create a new vault. After deploying the new vault, the contract sets the user as the vault manager.

Vault managers can change the vault fees and disable certain vault features. Therefore, users must verify that vaults that they interact with have reliable managers or have had their managers disabled through verification.

## Project Goals

The engagement was scoped to provide a security assessment of version 2 of the NFTX protocol. Specifically, we sought to answer the following non-exhaustive list of questions:

* Is there a way for users to circumvent fees?
* Can the fee distributor be abused?
* Can a buildup of fees introduce attack vectors?
* Is there a way for a malicious vault manager to grief the vault’s users?
* Is there a way for a malicious third-party token to compromise an NFTX vault?



## Project Targets

The engagement involved a review and testing of the following target.

### NFTX Protocol v2

[https://github.com/NFTX-project/nftx-protocol-v2/](https://github.com/NFTX-project/nftx-protocol-v2/)

```
c8ddc72b4400ad1e12ed03f4369b765371564a00
```

Note: Some files in the repository were explicitly out of scope for this assessment. These are enumerated in the following section.

## Project Coverage

This section provides an overview of the analysis coverage of the review, as determined by our high-level engagement goals. Our approaches and their results include the following:

### NFTXVaultFactoryUpgradeable

This upgradeable contract is one of the centerpieces of the protocol. It is responsible for the deployment and management of vaults. As a vault factory, it is responsible for deploying new vault proxies. It also acts as a beacon proxy: vault proxies query the factory for the address of the vault reference implementation before executing delegatecall into it.

This beacon structure allows the NFTX team to upgrade all its vaults at the same time without much friction by simply updating the address of the reference implementation stored by the beacon.

### NFTXVaultUpgradeable

This contract is the reference vault implementation and is the core of the NFTX protocol. Users can deposit NFTs (ERC721 and ERC1155) into vaults and receive ERC20 tokens representing claims to the deposited NFTs. This allows users to gain exposure to the floor price of the collection and to provide liquidity on protocols such as automated market makers (AMMs), like Uniswap and Sushiswap. Vaults also allow users to redeem NFTs by burning the corresponding ERC20 tokens and swapping their NFTs for those deposited in a vault.

### NFTXInventoryStaking

This upgradeable contract acts as both a factory and a beacon proxy. As a factory, it enables the creation of xToken (also written “XToken” in the codebase) proxies; these ERC20 tokens are wrappers around vault tokens and enable depositors to earn rewards by staking their vault tokens in the inventory staking contract.

As a beacon proxy, similarly to the vault factory, it stores the reference to the xToken implementation contract, which xToken proxies can query before executing delegatecall into it.

The contract receives fees from the NFTXSimpleFeeDistributor contract. NFTXLPStaking

This upgradeable contract acts as both a factory and an intermediary. As a factory, it deploys minimal proxies using CREATE2, which allows it to compute the addresses of the newly deployed proxies without having to store them.

As an intermediary, it manages the staking functionality, which allows users to deposit liquidity provider (LP) tokens to receive rewards, and is responsible for directing calls to the right proxy contracts by computing their addresses; to do so, it relies on the StakingTokenProvider contract, which maps vaults to paired tokens.

The contract receives fees from the `NFTXSimpleFeeDistributor` contract.

### NFTXSimpleFeeDistributor

This upgradeable contract is responsible for managing the distribution of protocol fees. The owner (the NFTX DAO in this particular case) is responsible for adding and removing fee receivers. Anyone can perform fee distribution, although it is typically performed by users interacting with the vaults when they perform actions that charge them protocol fees.

### Coverage Limitations

Because of the time-boxed nature of testing work, it is common to encounter coverage limitations. This engagement was scoped to assess only on-chain code. The web-based front end and the protocols for deploying and upgrading contracts warrant a separate review. The following files in the reviewed repository were also explicitly out of scope:

* contracts/solidity/NFTXV1Buyout.sol
* contracts/solidity/tools/NFTXFlashSwipe.sol
* contracts/solidity/other/PalmNFTXStakingZap.sol
* /contracts/solidity/eligibility/\*
  * Except for the following file, which was in scope: contracts/solidity/eligibility/NFTXRangeEligibility.sol



