## KartikToken
The KartikToken Solidity program is a smart contract implementation for creating and managing a custom ERC20 token on the Ethereum blockchain. It demonstrates the basic functionality of creating, transferring, and burning tokens, as well as owner-restricted token minting.

## Description
The KartikToken contract extends the OpenZeppelin ERC20 implementation and includes the following functionalities:

## Minting Tokens: Only the contract owner can mint new tokens.
## Burning Tokens: Any token holder can burn their tokens, reducing the total supply.
## Transferring Tokens: Token holders can transfer tokens to other addresses with balance checks.

Getting Started

##Prerequisites
To work with this contract, you will need the following:

Solidity compiler version ^0.8.0
A development environment such as Remix, Truffle, or Hardhat

Using Remix
Open Remix: Go to Remix.
Create a New File: Click on the "+" icon in the left-hand sidebar and save the file with a .sol extension (e.g., KartikToken.sol).
Contract Code: Copy the KartikToken contract code into the file.
solidity

## code
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract KartikToken is ERC20, Ownable {
    
    constructor(string memory name, string memory symbol) ERC20(name, symbol) Ownable(msg.sender) {
    }

    function createTokens(address recipient, uint256 amount) public onlyOwner {
        _mint(recipient, amount);
    }

    function destroyTokens(uint256 amount) public {
        require(balanceOf(msg.sender) >= amount, "Insufficient tokens to burn");
        _burn(msg.sender, amount);
    }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        require(balanceOf(msg.sender) >= amount, "Insufficient tokens to transfer");
        return super.transfer(recipient, amount);
    }
}

## Compile the Contract: Click on the "Solidity Compiler" tab in the left-hand sidebar, select version 0.8.0 (or compatible version), and click on "Compile KartikToken.sol".
Deploy the Contract: Go to the "Deploy & Run Transactions" tab, select the KartikToken contract, and click "Deploy".
#Interacting with the Contract
Mint Tokens: Call the createTokens function with the recipient address and the amount of tokens to mint. This function can only be called by the contract owner.
Burn Tokens: Any user can call the destroyTokens function to burn their tokens, reducing the total supply.
Transfer Tokens: Users can transfer tokens by calling the transfer function, which includes a check to ensure sufficient balance.

## Authors
Kartik Raghuwanshi

## License
This project is licensed under the MIT License
