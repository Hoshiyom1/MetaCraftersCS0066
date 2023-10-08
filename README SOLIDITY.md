# Simple Token Contract Project
This project aims to create a simple program that will do the following with said features: (for educational purposes only)

### Key Features:

- **Token Name:** This contract represents an example token with the name "ExampleToken."
- **Token Symbol:** The token is identified by the symbol "EXT."
- **Token Balances:** It keeps track of user balances using a mapping that associates addresses with token amounts.
- **Mint Function:** The `mint` function allows adding tokens to a user's balance, increasing the total token supply.
- **Burn Function:** The `burn` function subtracts tokens from a user's balance and decreases the total token supply when the user has enough tokens.


## Description

This Solidity program is a simple smart contract for educational purposes, focusing on two core functions: minting (adding) and burning (subtracting) assets. It serves as a practical example for learning about Ethereum smart contract development.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract MyToken {
    string public coinName = "MYPRECIOUS";
    string public coinSymbol = "MYP";
    uint public totalCoinSupply = 0;
    
    mapping(address => uint) public balances;

    function mint(address user, uint amount) public {
        totalCoinSupply += amount;
        balances[user] += amount;
    }

    function burn(address user, uint amount) public {
        if (balances[user] >= amount) {
            totalCoinSupply -= amount;
            balances[user] -= amount;
        }
    }
}


```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile Solidity.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "Solidity" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with the two main functions in there, the burn to basically burn eth (subract) and mint to basically add things (on a surface level).

## Authors

Sally P. Segundo jr.   
@https://github.com/Hoshiyom1


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
