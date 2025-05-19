# Question
 - Create a contract that splits incoming Ether between 3 fixed addresses.

# Deployment
<img src='https://private-user-images.githubusercontent.com/180368689/445093445-f26cde68-c9a7-45f8-b75d-3a58f1c6d0b6.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTEwMzksIm5iZiI6MTc0NzY1MDczOSwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDkzNDQ1LWYyNmNkZTY4LWM5YTctNDVmOC1iNzVkLTNhNThmMWM2ZDBiNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDMyMTlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wNmUwZGE2NmYyOTMxYTAwNzJhYzJlNGZiNmNjM2ZmNWVmNDJjYTFmOTM4MTk1YTU1NDdiMjhkZmY2YzkzZTM4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.gUHwCnmSUBuXbzJwDxNM3NXRZuDmGh4D1Zra2pG6L4w' length='500' width='550'>
<img src='https://private-user-images.githubusercontent.com/180368689/445093472-a5dbed33-c276-4ea1-84af-a47f205bbaa1.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTEwMzksIm5iZiI6MTc0NzY1MDczOSwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDkzNDcyLWE1ZGJlZDMzLWMyNzYtNGVhMS04NGFmLWE0N2YyMDViYmFhMS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDMyMTlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xMTE1YWE5MDQ2YzY1NWZiMjcwODIxYTVkNmYwNmJlNzZmYWZhYzkzODAyN2RjYjFkNzg5NTQ5OWQ2ZWMxMTc1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Ml-26_Lq4J3n2XVJtfFkrcF7bgaAbFZ1e7_rSFoGGdc' length='500' width='550'>

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
