# SOLIDITY

This solidity program was created for educational purposes only!

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract has two main fucntions, to mint and burn, basically will add and subract things.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

```javascript
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
