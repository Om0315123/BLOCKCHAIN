# Question
- Implement a simple auction system where users can place bids, and the highest bidder wins.
# Deployment
<img src='https://private-user-images.githubusercontent.com/180368689/445097078-b8e4af40-5a33-4418-8753-d4c298533e45.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTEyMTcsIm5iZiI6MTc0NzY1MDkxNywicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDk3MDc4LWI4ZTRhZjQwLTVhMzMtNDQxOC04NzUzLWQ0YzI5ODUzM2U0NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDM1MTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02YzUzZmQzZDI4MDI4MGIzNmE1M2JjODc1NWIxMjBmZWI4YTcxMThiYTUwYzIyYjA1ZGM3MGY4OTMyMGRlN2I5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.FksB40IPjy3Jyij1ACRoyJSZv9tCwmSw5lQ0-sirWHw' length='500' width='550'>
<img src='https://private-user-images.githubusercontent.com/180368689/445097079-caee92ca-ac55-46df-b36d-390427914187.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTEyMTcsIm5iZiI6MTc0NzY1MDkxNywicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDk3MDc5LWNhZWU5MmNhLWFjNTUtNDZkZi1iMzZkLTM5MDQyNzkxNDE4Ny5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDM1MTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zMTViOTg2MmRjYjljNGUyOGVjNDI4ZjgwMDRjZmI1NzBkMjI3MTA5MGVmZDEyN2M1OGEyNzhiZTllMjAwOWFjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.YaNdPZDURXVEz_nAQxsmDNQreQ1a5HrbL5zHSr7_HDc' length='500' width='550'>

## Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract Auction {
    address public highestBidder;
    uint public highestBid;

    mapping(address => uint) public bids;

    function bid() public payable {
        require(msg.value > highestBid, "Bid too low");

        if (highestBidder != address(0)) {
            // Refund previous bidder
            payable(highestBidder).transfer(bids[highestBidder]);
        }

        highestBid = msg.value;
        highestBidder = msg.sender;
        bids[msg.sender] = msg.value;
    }

    function getWinner() public view returns (address, uint) {
        return (highestBidder, highestBid);
    }
}
