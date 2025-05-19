# Question
- Develop a contract that only allows the deployer (owner) to call a specific function (use modifiers).

# Deployment
<img src='https://private-user-images.githubusercontent.com/180368689/445103397-e7c77922-6e5a-4807-b9ef-feeb0d22dc82.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIzNDYsIm5iZiI6MTc0NzY1MjA0NiwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAzMzk3LWU3Yzc3OTIyLTZlNWEtNDgwNy1iOWVmLWZlZWIwZDIyZGM4Mi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDU0MDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xMWNjMDhiMzA1NGJhYTM5ZTUwMzdkMGNiMWRkYzk0NTIxY2I2NzVhYTgyY2QxYThlMzdjYTU5M2VmODlkYmI2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.hntdDqLzJSqsawdprjuGa4prOLgZLhkju3eumTxBHwU' length='500' width ='550'>
<img  src ='https://private-user-images.githubusercontent.com/180368689/445103396-1323a869-b7f5-4d52-bec9-dfb404866f9c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIzNDYsIm5iZiI6MTc0NzY1MjA0NiwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAzMzk2LTEzMjNhODY5LWI3ZjUtNGQ1Mi1iZWM5LWRmYjQwNDg2NmY5Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDU0MDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wN2NkOTQ4N2E2MjViOTk5ZWQwMWVhMmU5MjQyMjUwNzkwOGM4OTJiYzkyOWI3YWM0NTFjNTEwZDU3MjZlZjg4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ryAFuJgAu1tD_HCEbtl6DAeUbOn7hOYWjWk46bGKGB4' length='500' width ='550'>

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
