# Question 
- Write a contract that manages a list of student records (name, roll number). Allow adding and retrieving student data.

## Deployment
<img src ='https://github.com/user-attachments/assets/167c4838-dbf1-4ffe-a590-5a651249c59e' length='500' width='550'>
<img src ='https://github.com/user-attachments/assets/0752eba1-ab5c-4bbf-9f14-deadfcc9d04b' length='500' width='550'>

## Contract
  ```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract StudentRecords {
    struct Student {
        string name;
        uint roll;
    }

    Student[] public students;

    function addStudent(string memory _name, uint _roll) public {
        students.push(Student(_name, _roll));
    }

    function getStudent(uint _index) public view returns (string memory, uint) {
        require(_index < students.length, "Index out of bounds");
        Student memory s = students[_index];
        return (s.name, s.roll);
    }

    function getStudentCount() public view returns (uint) {
        return students.length;
    }
}
