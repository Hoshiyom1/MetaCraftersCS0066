# Functions and Errors - ETH + AVAX, part of the ETH + AVAX PROOF: 

This Solidity program, part of the ETH + AVAX PROOF series, is designed for educational purposes.

## Description

The Solidity programming language, which is primarily used to generate smart contracts for the Ethereum blockchain, is demonstrated here in the form of a simple smart contract. There are two major functions in the contract: "withdraw" and "deposit," both of which have different restrictions. In particular, because the owner's position is exclusive, the contract forbids the owner from making withdrawals or deposits. The code also uses "asserts" and "reverts" illustratively to demonstrate various error-handling scenarios. Notably, a contract reversal occurs for any input of 0. 

## Getting Started

### Running program

To execute this program, Remix, an online Solidity Integrated Development Environment (IDE), is recommended. Here's how to begin:

1.) Visit the Remix website at Remix Ethereum.

2.) On the Remix website, create a new file by clicking the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., Crowdfunding.sol).

3.) Copy and paste the provided Solidity code into the file.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract Crowdfunding {
    address public owner;
    uint256 public fundingGoal;
    uint256 public deadline;
    mapping(address => uint256) public CONTRIBUTIONS;
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

    function CONTRIBUTE() public payable beforeDeadline {
        require(msg.value > 0, "Contribution must be greater than 0 ether.");
        CONTRIBUTIONS[msg.sender] += msg.value;

        if (address(this).balance >= fundingGoal) {
            fundingGoalReached = true;
        }
    }

    function CLOSE_CROWD_FUNDING() public onlyOwner {
        crowdfundingClosed = true;
    }

    function WITHDRAW_FUNDS() public onlyOwner afterDeadline {
        require(fundingGoalReached, "Funding goal not reached.");
        payable(owner).transfer(address(this).balance);
    }

    function REFUND_FUNDS() public beforeDeadline {
        require(crowdfundingClosed, "Crowdfunding is still open.");
        require(!fundingGoalReached, "Funding goal has been reached.");

        uint256 contribution = CONTRIBUTIONS[msg.sender];
        require(contribution > 0, "No contribution to refund.");
        CONTRIBUTIONS[msg.sender] = 0;
        require(payable(msg.sender).send(contribution), "Refund failed.");
    }

    function ASSERT_EXAMPLE(uint256 a, uint256 b) public pure returns (uint256) {
        assert(a + b > a);  // This should always be true, otherwise, it's a critical bug.
        return a + b;
    }

    function REVERT_EXAMPLE(uint256 x) public pure returns (string memory) {
        require(x >= 10, "Value must be greater than or equal to 10.");
        if (x < 20) {
            revert("Value must be greater than or equal to 20.");
        }
        return "Operation successful.";
    }
}





```

1.) Compile the code by accessing the "Solidity Compiler" tab in the left-hand sidebar. Ensure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click the "Compile functionsanderrors.sol" button.

2.) After successful compilation, deploy the contract by clicking the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "ExceptionHandlingDemo" contract from the dropdown menu, and click the "Deploy" button.

3.) Once the contract is deployed, you are free to interact with the program as desired.

## Authors

Sally P. Segundo jr.   
@https://github.com/Hoshiyom1


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
