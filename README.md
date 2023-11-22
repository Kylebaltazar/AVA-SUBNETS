# Solidity by Example ERC-20 Token (Code Version)

## Overview

This repository contains a simple implementation of an ERC-20 token in Solidity, adhering to version ^0.8.17. The ERC-20 standard defines a set of rules for creating tokens on the Ethereum blockchain. The token, named "Solidity by Example" (symbol: SOLBYEX), includes standard functions such as `transfer`, `approve`, `transferFrom`, `mint`, and `burn`.

## Contract Details

- **Name:** Solidity by Example
- **Symbol:** SOLBYEX
- **Decimals:** 18
- **Total Supply:** Variable, initialized to 0

## Functions

### `transfer`

```solidity
function transfer(address recipient, uint amount) external returns (bool);
```

Transfers `amount` tokens from the caller's account to the `recipient`. Emits a `Transfer` event.

### `approve`

```solidity
function approve(address spender, uint amount) external returns (bool);
```

Allows `spender` to withdraw from the caller's account multiple times, up to the `amount` set. Emits an `Approval` event.

### `transferFrom`

```solidity
function transferFrom(address sender, address recipient, uint amount) external returns (bool);
```

Transfers `amount` tokens from `sender` to `recipient`, given the allowance. Emits a `Transfer` event.

### `mint`

```solidity
function mint(uint amount) external;
```

Mints (creates) `amount` new tokens and adds them to the caller's balance. Emits a `Transfer` event from the zero address.

### `burn`

```solidity
function burn(uint amount) external;
```

Burns (destroys) `amount` tokens from the caller's balance. Emits a `Transfer` event to the zero address.

## Events

### `Transfer`

```solidity
event Transfer(address indexed from, address indexed to, uint value);
```

Emitted when tokens are transferred between addresses.

### `Approval`

```solidity
event Approval(address indexed owner, address indexed spender, uint value);
```

Emitted when the allowance of a spender is set by the owner.

```

Make sure to replace the placeholder `[LICENSE](LICENSE)` with the appropriate link or text for your license file. Save this content in a file named `README.md` in the root directory of your repository.
