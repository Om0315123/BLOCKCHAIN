# QUESTION 1
- Create a voting system with multiple candidates. Each address can vote only once.
## DEPLOYMENT
<img src='https://private-user-images.githubusercontent.com/180368689/445101641-a4e9cfbb-1a42-4450-9a9e-97704b4bc785.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIwMjQsIm5iZiI6MTc0NzY1MTcyNCwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAxNjQxLWE0ZTljZmJiLTFhNDItNDQ1MC05YTllLTk3NzA0YjRiYzc4NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDQ4NDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lODlkYjRkODVhYjE3MTQ2MWMyYTcyNDkwNGNjOTYwNjRmZGYwZjk3NDhjZmNkZDhhNjNlMGJmZjRiZDI2NzE4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.PUu69J7WFfw4qMe5JrNxkKeTTXo62Up7zdaeEXrw-bA' length='500' width='550'>
<img src='https://private-user-images.githubusercontent.com/180368689/445101642-fa382ddc-9878-4dcf-b303-de7e7e966dbc.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIwMjQsIm5iZiI6MTc0NzY1MTcyNCwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAxNjQyLWZhMzgyZGRjLTk4NzgtNGRjZi1iMzAzLWRlN2U3ZTk2NmRiYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDQ4NDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Y2ExYjlmMGE3ZWYzZDYyYzRmMTBkY2UzYjZhNDYzZmE2Y2Q0ZWYxYzU3YzI3NWI0ZDgwYTkxYWZkNmUxODVlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.nAmPz50ggb8W2MUVRgvOjlYi7UZHVbtJoVH3vSzA5gI' length='500' width='550'>

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

