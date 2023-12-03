# Degen Gaming Token (DGT) - Solidity Smart Contract

## Overview

The Degen Gaming Token (DGT) is an ERC-20 compliant token implemented as a Solidity smart contract on the Ethereum blockchain. It extends the functionality of the OpenZeppelin ERC-20, Ownable, and ERC20Burnable contracts, providing additional features specific to the Degen Gaming ecosystem.

## Features

### Minting Tokens

The contract owner can mint new DGT tokens and assign them to a specific beneficiary using the `mintTokens` function. This function is restricted to the contract owner.

```solidity
function mintTokens(address beneficiary, uint volume) public onlyOwner {
    _mint(beneficiary, volume);
}
```

### Transferring Tokens

Users can transfer DGT tokens to other addresses using the `transferTokens` function. This function ensures that the sender has sufficient tokens for the transfer.

```solidity
function transferTokens(address acceptor, uint volume) external {
    require(balanceOf(msg.sender) >= volume, "INSUFFICIENT TOKENS!!");
    _transfer(msg.sender, acceptor, volume);
}
```

### Redeeming Tokens for Stock

Users can redeem their DGT tokens for various types of gym equipment stock, each associated with a specific token amount. The `redeemForTokens` function calculates the redeemed stock type based on the provided token amount.

```solidity
function redeemForTokens(uint256 tokenAmount) public {
    recentRedeemedStock = determineRedeemedStock(tokenAmount);
    require(stockRates[recentRedeemedStock] > 0, "Invalid stock type");
    require(balanceOf(msg.sender) >= stockRates[recentRedeemedStock], "INSUFFICIENT TOKENS!!");
    _burn(msg.sender, stockRates[recentRedeemedStock]);
    emit LogMessage("Redemption is Successful");
}
```

### Burning Tokens

Users can burn their DGT tokens, reducing the total supply. This is facilitated by the `burnTokens` function.

```solidity
function burnTokens(uint256 volume) external {
    require(balanceOf(msg.sender) >= volume, "INSUFFICIENT TOKENS!!");
    _burn(msg.sender, volume);
    emit LogMessage("Tokens burned successfully");
}
```

### Additional Information

- The contract defines an enumeration `StockType` representing different types of gym equipment stock.
- The contract owner can initialize the contract with specific stock rates for each type of equipment.
- The contract emits a `LogMessage` event for important state changes.

## Author 

Praveen 

p0555319@gmail.com
