# Question
- Develop a contract that only allows the deployer (owner) to call a specific function (use modifiers).

# Deployment
<img src='https://github.com/user-attachments/assets/fb15606e-2bbc-4c27-9678-d4ef3998eb17' length='500' width ='550'>
<img  src ='https://github.com/user-attachments/assets/be87aa45-ccd0-49ca-972d-d77d9ecd8239' length='500' width ='550'>

## Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract OnlyOwner {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner!");
        _;
    }

    function sensitiveFunction() public onlyOwner {
        // Only owner can do this
    }

    function getOwner() public view returns (address) {
        return owner;
    }
}
