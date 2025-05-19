# Question
- Implement a simple auction system where users can place bids, and the highest bidder wins.
# Deployment
<img src='https://github.com/user-attachments/assets/ae65f1ad-8615-49e1-ae13-b118e4c20472' length='500' width='550'>
<img src='https://github.com/user-attachments/assets/cf837b76-f0e5-4be2-bc56-0a90fccb4c5a' length='500' width='550'>

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
