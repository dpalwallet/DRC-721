[English](./README_en.md) | [中文](./README.md)

---

# DRC-721：Non-Fungible Tokens on the Dogecoin Network

DRC-721 is inspired by the BRC-721，an experimental standard for creating fungible tokens on the Dogecoin network. BRC-721, which can be found at，ims to bring the functionality of issuing tokens to the Bitcoin ecosystem.
By building upon the ideas and principles of brc-721，DRC-721 extends the capabilities of tokenization on the dogecoin network to include non-fungible tokens, thus enabling a broader range of digital asset management and value representation.

DRC-721 is designed for non-fungible tokens (NFTs) on the Dogecoin network. It allows for the creation, ownership, and transfer of unique digital assets on the Dogecoin blockchain. Each token created under DRC-721 has a unique identifier, making them distinct and non-interchangeable.

## Operations

### Deploy  DRC-721

Deploy a DRC-721 NFT and use external links to provide image uri information for each token to reduce the data footprint of images:

``` json
{
    "p": "drc-721",
    "op": "deploy",
    "tick": "burn",
    "max": "10000",
    "buri": "https://ipfs.io/abc/"
}
```

* For token ID 1, the metadata is located at `https://ipfs.io/abc/1`
* Note: After the deployment is complete, please record the transaction hash. This hash is similar to the address of the Ethereum smart contract and is used to locate the nft collection. The advantage of this is to avoid the abuse of duplicate names and facilitate the minter and publisher to locate a certain NFT collection
* RC20 and NFT are different types of assets. NFT needs a transaction hash similar to the original deployment (I call it a verifiable contract address), so as to facilitate the management of the nft collection and confirm the uniqueness, so that any publisher can notify the user to mint based on the transaction , even if your brand is abused, you can still solve the duplicate name problem through the original transaction hash
### Mint DRC-721

``` json
{
    "p": "drc-721",
    "op": "mint",
    "txid": "the deployed hash"
}
```

| Key | Required？ | Description |
|---|---|---|
| p | Y | Protocol: Helps other systems identify and process drc-721 events |
| op | Y | Operation: Type of event（deploy, mint, transfer） |
| txid | Y | txid：Similar to the contract address of the Ethereum smart contract, the hash is the deployed script transaction hash. The advantage of this is that it can locate the original deployed transaction ID and solve the problem of duplicate names. |

* token ID is generated from 1 to max according to the order of inscription IDs.

### Transfer DRC-721

Transferring DRC-721 tokens is as simple as minting a transfer transaction and the index will identify the transaction

``` json
{
    "p": "drc-721",
    "op": "transfer",
    "id": "1",
    "txid" : "the deployed hash",
    "to" : "receiver address"
}
```

| Key | Required？ | Description |
|---|---|---|
| p | y | Protocol: Helps Other Systems Identify and Process DRC-721 Events |
| op | y | Action: Event type (deploy, mint, transfer) |
| id | y | id： unique tokenid of collection|
| txid | y | Deploy transaction hash |
| to | y | receiver |

* This operation only allows transfers by the owner of `id`
  
### Abount indexer

The index is still under test, and the details and principles will be released after the test and verification pass, mainly solving several problems below:

* The traditional way of directly writing pictures cannot prove the uniqueness of assets, so a verifiable index is still needed to ensure asset ownership
* Dust problem, this version of the index rules will not be troubled by dust
* drc721 base on  doginal Upgraded Agreement (doginal+)


## Contribute

DRC-721 is an experimental standard that brings non-fungible tokens (NFTs) to the Dogecoin network. With this standard, users can create, mint, transfer, and update unique digital assets, enabling a wide range of use cases, such as digital art, collectibles, virtual goods, and more.

The standard allows for a series of operations that facilitate the management of non-fungible tokens, including deployment, minting, transferring. Each token is assigned a unique identifier, ensuring that each NFT is distinct and cannot be exchanged on a one-to-one basis with another NFT.

As an experimental standard, DRC-721 invites improvements and modifications to enhance its functionality and adapt it to the growing needs of the NFT ecosystem.

## reference
https://brc-721.gitbook.io/about-the-brc-721-experimental-proposal/

https://github.com/adshao/brc-721/blob/main/README_zh.md
