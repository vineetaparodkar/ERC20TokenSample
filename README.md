# Basic ERC20 token sample

This project demonstrates a basic ERC20 token sample. It comes with a sample contract, a sample script that deploys that contract, and an example of a task implementation, which simply lists the available accounts.

## ERC20 Notes

- A token is a type of cryptocurrency that represents an asset that can be used for payment or investment purposes.

- In the blockchain world, a token is very similar to those you use in carnivals. First, you use fiat currency to change into a cryptocurrency, such as ether. Then, you use ether to change into a token. The token can then be used as payments for smart contracts running on the Ethereum blockchain

- Token vs coin

    - A coin operates on its own blockchain.A coin also acts like money, where it can replace fiat currencies for payment purposes. Finally, a coin can be mined on the blockchain.A coin is essentially digital versions of money

    - A token, on the other hand, does not have its own blockchain. Instead, it runs on an existing blockchain, such as Ethereum. A token usually uses a smart contract to maintain records of who owns what. Unlike coins which are generally accepted for various services on the Blockchain, tokens are much more restrictive in their uses and specific tokens are only accepted for specific services. a token can represent more than just money; it may represent assets or deeds.You can buy tokens with coins, but not the other way round

- Token Contract 

    - Tokens are created using smart contracts in Ethereum. A token smart contract is essentially a smart contract that contains a map of account addresses and their balances

- Token Representation

    - ERC20 tokens can have up to 18 decimal places of precision. That means that your token can have denominations as little as 0.000000000000000001.
    Consider the following example. You have a one dollar coin — $1. But the smallest denomination is 1 cent, which is equal to $0.01. So your $1 can go right down to 2 decimal places, and is equal to 1 x 10² cents (where 2 is the number of decimal places):

    - When you record your money, you record it in dollars. For example, if you have 5 dollars, you record it as $5 — you don’t record it as 500 cents. However, for Solidity, here is the problem. Solidity does not support floating point numbers, so when you record your token counts, Solidity cannot store it using floating point numbers, say 2.5 tokens. Instead, you have to store the token based on the smallest denomination. For example, say you want your token to support up to 18 decimal places. So the smallest token is 0.000000000000000001. Internally in your token contract, you will store this as 1. For one token you would need to store this as 1 x 10¹⁸:


## Reference

- ERC20 overview: https://levelup.gitconnected.com/minting-your-own-erc-20-tokens-in-ethereum-a477bd38c135


## Setup

- Add metamask account secret key in `ERC20TOKENSAMPLE/.secret` file.

- Add Ropsten or Polygon RPC URL's, burner/minter account addresses.

- Compile Solidity ERC20 contract with below command

    ` npx hardhat compile`

- Deploy ERC20 smart contract with below command

    `node scripts/deploy.js`

