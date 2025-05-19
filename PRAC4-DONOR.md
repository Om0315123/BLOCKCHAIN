# Question
Write a contract where people can donate Ether and the top 3 donors are tracked.
# DEPLOYMENT
<img src='https://github.com/user-attachments/assets/38b9097e-0bb1-4894-9a4c-e7faa0bfd6aa' length='500' width='550'>
<img src='https://github.com/user-attachments/assets/31599a60-78c1-43b2-82a6-e7c9609a76c6' length='500' width='550'>

# Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract TopDonors {
    struct Donor {
        address addr;
        uint amount;
    }

    Donor[3] public topDonors;

    function donate() public payable {
        require(msg.value > 0, "Send some Ether!");

        for (uint i = 0; i < 3; i++) {
            if (msg.value > topDonors[i].amount) {
                for (uint j = 2; j > i; j--) {
                    topDonors[j] = topDonors[j - 1];
                }
                topDonors[i] = Donor(msg.sender, msg.value);
                break;
            }
        }
    }

    function getTopDonors() public view returns (Donor[3] memory) {
        return topDonors;
    }
}
