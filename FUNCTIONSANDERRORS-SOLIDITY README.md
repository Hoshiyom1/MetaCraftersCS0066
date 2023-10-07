# SOLIDITY

This solidity program was created for educational purposes only!

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. This program has 2 main function the withdraw and deposit, but has alot of conditionals such as the owner must not be able to withdraw or deposit becuase its the owner basically. Other than those there are also asserts to have example scenarios etc. And lastly if it is inputted 0 it would revert.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract ExceptionHandlingDemo {
    address public owner;
    uint256 public value;
    mapping(address => uint256) public balances;

    constructor() {
        owner = msg.sender;
    }

    function deposit(uint256 amount) public {
        require(msg.sender != owner, "Owner cannot deposit");
        value += amount;
        balances[msg.sender] += amount;
    }

    function withdraw(uint256 amount) public {
        require(msg.sender != owner, "Owner cannot withdraw");
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        value -= amount;
    }

    function assertExample(uint256 x) public pure returns (uint256) {
        assert(x != 0);
        return x;
    }

    function requireExample(uint256 x) public pure returns (uint256) {
        require(x != 0, "Input must be non-zero");
        return x;
    }

    function revertExample(uint256 x) public pure returns (uint256) {
        if (x == 0) {
            revert("Input cannot be zero");
        }
        return x;
    }
}



```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile functionsanderrors.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "ExceptionHandlingDemo" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with the program as you see fit.

## Authors

Sally P. Segundo jr.   
@https://github.com/Hoshiyom1


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
