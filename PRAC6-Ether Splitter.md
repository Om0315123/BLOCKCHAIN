# Question
 - Create a contract that splits incoming Ether between 3 fixed addresses.

# Deployment
<img src='https://github.com/user-attachments/assets/a78face6-d413-4c6f-95dc-d79ef6e34add' length='500' width='550'>
<img src='https://github.com/user-attachments/assets/c337aaf6-6ce7-4547-876e-79b3af595dd7' length='500' width='550'>

## Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract EtherSplitter {
    address payable public addr1;
    address payable public addr2;
    address payable public addr3;

    constructor(address payable _a1, address payable _a2, address payable _a3) {
        addr1 = _a1;
        addr2 = _a2;
        addr3 = _a3;
    }

    receive() external payable {
        uint share = msg.value / 3;
        addr1.transfer(share);
        addr2.transfer(share);
        addr3.transfer(msg.value - (share * 2)); // Remainder to last
    }
}
