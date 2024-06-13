// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyToken {

  
    string public name;
    string public symbol;
    uint256 public totalSupply;

    
    mapping(address => uint256) public balances;

    
    function mint(address recipient, uint256 amount) public {
        require(msg.sender == address(this), "Only contract can mint tokens"); 

        
        uint256 newTotalSupply = totalSupply + amount;
        require(newTotalSupply >= totalSupply, "Mint amount would cause overflow");

        totalSupply = newTotalSupply;
        balances[recipient] += amount;
    }

    function burn(uint256 amount) public {
        require(msg.sender == address(this), "Only contract can burn tokens"); 

        require(balances[msg.sender] >= amount, "Insufficient balance to burn"); 

        
        uint256 newTotalSupply = totalSupply - amount;
        require(newTotalSupply <= totalSupply, "Burn amount would cause underflow");

        totalSupply = newTotalSupply;
        balances[msg.sender] -= amount;
    }



    constructor(string memory _name, string memory _symbol, uint256 _initialSupply) {
       
    }

    
}



