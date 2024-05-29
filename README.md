# Module 3 | Project: Create and Mint Token

This Defines a smart contract for an ERC20 token named "EcoCoin." This token adheres to the ERC20 standard, allowing users to transfer and manage balances. It also incorporates additional functionalities. The contract owner, specified during deployment, can mint new tokens using a restricted "mint" function. Furthermore, users can burn their own tokens thanks to the inheritance from ERC20Burnable. Ownership control is established through the Ownable contract, ensuring only the owner can mint new tokens. Overall, this code demonstrates the creation of a custom ERC20 token with features like controlled minting, burning capabilities, and ownership management.

## Description

This program crafts a smart contract for an ERC20 token dubbed "EcoCoin." It faithfully adheres to the ERC20 standard, enabling users to seamlessly transfer tokens and keep track of their balances. Beyond the standard functionalities, it offers some additional features. The contract owner, designated during deployment, has the privilege of minting new tokens through a restricted "mint" function.


## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract EcoCoin is ERC20, ERC20Burnable, Ownable {

  constructor(uint256 initialSupply, string memory name, string memory symbol, address initialOwner) 
    ERC20(name, symbol) Ownable(initialOwner) {
    _mint(initialOwner, initialSupply * 10**uint(decimals()));
  }

  function mint(address to, uint256 amount) public onlyOwner {
    _mint(to, amount);
  }

  
  function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
    _spendAllowance(sender, address(this), amount); 
    _transfer(sender, recipient, amount);
    return true;
  }
}

```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.20" (or another compatible version), and then click on the "Compile MyTypesofFunctions-ETH+AVAX" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "MyTypesofFunctions-ETH+AVAX" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the sayHello function. Click on the "MyTypesofFunctions-ETH+AVAX" contract in the left-hand sidebar, and then input the desired transaction function.

## Authors

Danz Andrew M. Permejo (61903258@ntc.edu.ph)


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
