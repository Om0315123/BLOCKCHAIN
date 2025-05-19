# QUESTION 1
- Create a voting system with multiple candidates. Each address can vote only once.
## DEPLOYMENT
<img src='https://github.com/user-attachments/assets/22710701-f1ca-4311-8b98-bbaf7caaf7c3' length='500' width='550'>
<img src='https://github.com/user-attachments/assets/41fd65a4-409b-4778-aeeb-3789820f8b7b' length='500' width='550'>

# CONTRACT
```SOLIDITY
    // SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VotingSystem {
    mapping(address => bool) public hasVoted;
    mapping(string => uint) public votes;
    string[] public candidates;

    constructor(string[] memory _candidates) {
        candidates = _candidates;
    }

    function vote(string memory _candidate) public {
        require(!hasVoted[msg.sender], "Already voted!");
        bool valid = false;
        for (uint i = 0; i < candidates.length; i++) {
            if (keccak256(bytes(candidates[i])) == keccak256(bytes(_candidate))) {
                valid = true;
                break;
            }
        }
        require(valid, "Invalid candidate");
        votes[_candidate]++;
        hasVoted[msg.sender] = true;
    }
}

