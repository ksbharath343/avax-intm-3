# UniqueToken Smart Contract

## Overview

The `UniqueToken` contract is an ERC20 token implementation using the OpenZeppelin library. It allows an administrator to mint new tokens, and users to transfer and burn tokens. The token has customizable name, ticker, decimals, and initial allocation.

## Features

1. **Token Initialization**: Set the name, ticker, decimals, and initial allocation of the token upon deployment.
2. **Minting Tokens**: The administrator can mint new tokens to any address.
3. **Burning Tokens**: Users can burn their own tokens.
4. **Transferring Tokens**: Users can transfer tokens to other addresses.

## Contract Details

### Inheritance
- Inherits from `ERC20` from the OpenZeppelin library.

### State Variables
- `administrator`: The address of the contract administrator, set during deployment.

### Constructor

```solidity
constructor(
    string memory tokenName,
    string memory tokenTicker,
    uint8 decimalUnits,
    uint256 initialAllocation
) ERC20(tokenName, tokenTicker) {
    _mint(msg.sender, initialAllocation * (10**decimalUnits));
    administrator = msg.sender;
}
```
- **Parameters**:
  - `tokenName`: The name of the token (e.g., "My Token").
  - `tokenTicker`: The ticker symbol of the token (e.g., "MTK").
  - `decimalUnits`: The number of decimal places the token uses.
  - `initialAllocation`: The initial number of tokens allocated to the administrator.
- **Functionality**:
  - Mints the initial allocation of tokens to the deployer.
  - Sets the deployer as the administrator.

### Functions

#### `mintTokens`

```solidity
function mintTokens(address giftee, uint256 mass) public {
    require(msg.sender == administrator, "Only the administrator can mint tokens.");
    _mint(giftee, mass);
}
```
- **Parameters**:
  - `giftee`: The address to receive the minted tokens.
  - `mass`: The number of tokens to mint.
- **Requirements**:
  - Only the administrator can call this function.

#### `burnTokens`

```solidity
function burnTokens(uint256 mass) public {
    _burn(msg.sender, mass);
}
```
- **Parameters**:
  - `mass`: The number of tokens to burn from the caller's account.

#### `transfertokens`

```solidity
function transfertokens(address giftee, uint256 mass) public returns (bool) {
    _transfer(msg.sender, giftee, mass);
    return true;
}
```
- **Parameters**:
  - `giftee`: The address to transfer the tokens to.
  - `mass`: The number of tokens to transfer.
- **Returns**:
  - `true` on successful transfer.

## Usage

### Deployment

Deploy the contract using any Ethereum development environment like Remix, Hardhat, or Truffle. Provide the required parameters during deployment.

### Minting Tokens

The administrator can mint new tokens to any address.

```solidity
mintTokens(addressOfRecipient, amount);
```

### Burning Tokens

Users can burn their own tokens.

```solidity
burnTokens(amount);
```

### Transferring Tokens

Users can transfer tokens to other addresses.

```solidity
transfertokens(addressOfRecipient, amount);
```

## Notes

- Ensure that the correct address is used for the administrator during deployment.
- Only the administrator can mint new tokens, ensuring controlled supply.
- Users have the ability to transfer and burn tokens, providing flexibility in token management.

## License

This project is licensed under the MIT License.
