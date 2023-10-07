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
