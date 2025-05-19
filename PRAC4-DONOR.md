# Question
Write a contract where people can donate Ether and the top 3 donors are tracked.
# DEPLOYMENT
<img src='https://private-user-images.githubusercontent.com/180368689/445098471-097cbd1f-f166-4919-ad1a-08c23afa143c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTE0NTcsIm5iZiI6MTc0NzY1MTE1NywicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDk4NDcxLTA5N2NiZDFmLWYxNjYtNDkxOS1hZDFhLTA4YzIzYWZhMTQzYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDM5MTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03MTI4YzdjMTEzODkyNTQ3NjMwM2YyY2JlOWFiNjU1OTBkZGFmYmVlZmQwMzYzNDUwOGE4N2UyNjkzYTY2MDc5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.vKclmfIBdsrMl5XcCJKekE-cUSTuiufB7l9bUwJ2wjQ' length='500' width='550'>
<img src='https://private-user-images.githubusercontent.com/180368689/445098472-c2787a05-1ce3-48fe-a4d4-c52031c06d38.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTE0NTcsIm5iZiI6MTc0NzY1MTE1NywicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MDk4NDcyLWMyNzg3YTA1LTFjZTMtNDhmZS1hNGQ0LWM1MjAzMWMwNmQzOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDM5MTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iYmQxMmNjNTIyMGNjNjc0ZTA4M2EyMjAyNWM0ZGQxOWQ5ZjNkNTVjNjdmZTk0ZTU5ZTQzMTY4MGZmNzk2MDYwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.CPBcAFJ0_ONXgV1eDNgY0gsqsp8KdCAkUwpC0bRHmCw' length='500' width='550'>

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
