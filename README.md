# Module 3 | Project: Create and Mint Token - ExoToken

This Defines a smart contract for an ERC20 token named "ExoToken." This token adheres to the ERC20 standard, allowing users to transfer and manage balances. It also incorporates additional functionalities. The contract owner, specified during deployment, can mint new tokens using a restricted "mint" function. Furthermore, users can burn their own tokens thanks to the inheritance from ERC20Burnable. Ownership control is established through the Ownable contract, ensuring only the owner can mint new tokens. Overall, this code demonstrates the creation of a custom ERC20 token with features like controlled minting, burning capabilities, and ownership management.

## Description

This program crafts a smart contract for an ERC20 token dubbed "ExoToken." It faithfully adheres to the ERC20 standard, enabling users to seamlessly transfer tokens and keep track of their balances. Beyond the standard functionalities, it offers some additional features. The contract owner, designated during deployment, has the privilege of minting new tokens through a restricted "mint" function.


## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract ExoToken is ERC20, Ownable {
    constructor(address Owner) Ownable(Owner) ERC20("ExoToken", "ET") {
        _mint(msg.sender, 50 * 10**18);
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function transfer(address to, uint256 amount) public override returns (bool) {
        _transfer(msg.sender, to, amount);
        return true;
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }
}

```
Firstly, the contract ensures that only the contract owner can mint new tokens. This is implemented in the mint function, which uses the onlyOwner modifier. This modifier restricts access so that only the owner, which is the address that deployed the contract or the address set as the owner, can call the mint function. When called by the owner, the _mint internal function from the ERC20 standard is used to create new tokens and assign them to a specified address.

Secondly, the contract allows any user to transfer tokens. The transfer function, which overrides the default ERC20 transfer function, enables users to send tokens to another address. It uses the _transfer internal function from the ERC20 standard to handle the actual token transfer between addresses. This function ensures that tokens are moved from the sender's address to the recipient's address and returns a boolean value indicating whether the transfer was successful.

Lastly, the contract permits any user to burn their own tokens, reducing the total supply. The burn function allows users to destroy a specified amount of their tokens. It uses the _burn internal function from the ERC20 standard to remove tokens from the caller's balance and decrease the total supply.


Danz Andrew M. Permejo (61903258@ntc.edu.ph)


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
