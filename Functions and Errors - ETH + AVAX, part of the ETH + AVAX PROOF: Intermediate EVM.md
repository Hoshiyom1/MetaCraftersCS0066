# Functions and Errors - ETH + AVAX, part of the ETH + AVAX PROOF: 

This solidity program was created for educational purposes only!

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. This program has 2 main function the withdraw and deposit, but has alot of conditionals such as the owner must not be able to withdraw or deposit becuase its the owner basically. Other than those there are also asserts to have example scenarios etc. And lastly if it is inputted 0 it would revert.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract Crowdfunding {
    address public owner;
    uint256 public fundingGoal;
    uint256 public deadline;
    mapping(address => uint256) public contributions;
    bool public fundingGoalReached;
    bool public crowdfundingClosed;

    constructor(uint256 _goalInEther) {
        owner = msg.sender;
        fundingGoal = _goalInEther * 1 ether;
        deadline = block.timestamp + 30 days; 
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function.");
        _;
    }

    modifier beforeDeadline() {
        require(block.timestamp < deadline, "The crowdfunding deadline has passed.");
        _;
    }

    modifier afterDeadline() {
        require(block.timestamp >= deadline, "The crowdfunding deadline has not passed yet.");
        _;
    }

    function contribute() public payable beforeDeadline {
        require(msg.value > 0, "Contribution must be greater than 0 ether.");
        contributions[msg.sender] += msg.value;

        if (address(this).balance >= fundingGoal) {
            fundingGoalReached = true;
        }
    }

    function closeCrowdfunding() public onlyOwner {
        crowdfundingClosed = true;
    }

    function withdrawFunds() public onlyOwner afterDeadline {
        require(fundingGoalReached, "Funding goal not reached.");
        payable(owner).transfer(address(this).balance);
    }

    function refund() public beforeDeadline {
        require(crowdfundingClosed, "Crowdfunding is still open.");
        require(!fundingGoalReached, "Funding goal has been reached.");

        uint256 contribution = contributions[msg.sender];
        require(contribution > 0, "No contribution to refund.");
        contributions[msg.sender] = 0;
        require(payable(msg.sender).send(contribution), "Refund failed.");
    }

    function assertExample(uint256 a, uint256 b) public pure returns (uint256) {
        assert(a + b > a);  // This should always be true, otherwise, it's a critical bug.
        return a + b;
    }

    function revertExample(uint256 x) public pure returns (string memory) {
        require(x >= 10, "Value must be greater than or equal to 10.");
        if (x < 20) {
            revert("Value must be greater than or equal to 20.");
        }
        return "Operation successful.";
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
