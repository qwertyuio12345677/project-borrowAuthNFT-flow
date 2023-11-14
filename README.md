
# CryptoPoops Smart Contract Readme

## Overview

The CryptoPoops smart contract is a Non-Fungible Token (NFT) implementation on the Flow blockchain. It utilizes the 0x06 version of the NonFungibleToken contract as a base and extends its functionality to create a collection of unique NFTs called CryptoPoops.

## Contract Structure

### CryptoPoops Contract

The `CryptoPoops` contract is the main entry point and inherits from the `NonFungibleToken` contract (0x06 version). It introduces the concept of CryptoPoops NFTs, each represented by the `NFT` resource. Additionally, it defines a public resource interface `MyCollectionPublic` and a resource called `Collection` that implements various NFT-related functionalities.

### NFT Resource

The `NFT` resource represents a CryptoPoop NFT. Each NFT has an ID, a name, a family name, and an age. NFTs are created using the `init` function, and their data cannot be modified after creation.

### Collection Resource

The `Collection` resource is a container for CryptoPoop NFTs. It implements the `NonFungibleToken.Provider`, `NonFungibleToken.Receiver`, `NonFungibleToken.CollectionPublic`, and `MyCollectionPublic` interfaces. The collection keeps track of owned NFTs and provides functions for depositing, withdrawing, and accessing NFTs.

### Minter Resource

The `Minter` resource facilitates the creation of new CryptoPoop NFTs. It includes functions to create a new NFT and instantiate a Minter.

## Public Interface

### Deposit and Withdraw Events

- `Deposit`: Triggered when an NFT is deposited into a collection. Includes the ID of the deposited NFT and the address of the recipient.
  
- `Withdraw`: Triggered when an NFT is withdrawn from a collection. Includes the ID of the withdrawn NFT and the address of the sender.

### MyCollectionPublic Interface

- `deposit`: Deposits an NFT into the collection.
  
- `getIDs`: Retrieves the IDs of owned NFTs.
  
- `borrowNFT`: Borrows a reference to a specific NFT.
  
- `borrowAuthNFT`: Borrows an authenticated reference to a specific NFT.
  
- `withdraw`: Withdraws an NFT from the collection.

### Minter Functions

- `createNFT`: Creates a new CryptoPoop NFT with the provided name, family name, and age.
  
- `createMinter`: Creates a new Minter instance.

### Contract Initialization

The contract initializes by setting the total supply to 0 and emitting a `ContractInitialized` event. Additionally, it creates a Minter instance and saves it to storage.

## Usage

1. **Creating a CryptoPoop NFT:** Use the `createNFT` function of the Minter to create a new CryptoPoop NFT by providing a name, family name, and age.

2. **Depositing NFTs:** Call the `deposit` function on a Collection to deposit a CryptoPoop NFT into the collection.

3. **Withdrawing NFTs:** Call the `withdraw` function on a Collection to withdraw a CryptoPoop NFT from the collection.

4. **Accessing NFTs:** Use the functions in the `MyCollectionPublic` interface to interact with the owned NFTs within a collection.

## Example

```cadence
// Example of contract interaction

// Assuming contract instance is deployed and stored in the 'contract' variable

// Create a new CryptoPoop NFT
let newNFT <- contract.createMinter().createNFT("John", "Doe", 25)

// Create a new empty collection
let collection <- contract.createEmptyCollection()

// Deposit the created NFT into the collection
collection.deposit(token: <-newNFT)

// Withdraw the NFT from the collection
let withdrawnNFT <- collection.withdraw(withdrawID: 1)
```

## Notes

- Ensure that you have the required Flow tokens to execute transactions.
  
- This contract is designed for educational purposes, and the code may require modifications for production use.

Feel free to explore and modify the contract to suit your specific use case or project requirements. Happy coding!
