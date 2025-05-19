# Question 
- Write a contract that manages a list of student records (name, roll number). Allow adding and retrieving student data.

## Deployment
<img src ='https://private-user-images.githubusercontent.com/180368689/445102691-83fa96f9-272a-4186-ba63-8f6a6f2ac14d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIyMTYsIm5iZiI6MTc0NzY1MTkxNiwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAyNjkxLTgzZmE5NmY5LTI3MmEtNDE4Ni1iYTYzLThmNmE2ZjJhYzE0ZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDUxNTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NGRiNzc5ZmQ3MTdmMjFiOTUyMTVhMzdlZjdjYTE2ZGUwZGMyZjA3ZTUwNzI0NjY4MGIyYjk0NDRjYjhkMmNlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.aHaluzJMhwJXe00-d1f8hIFYr5v-ygA_XtXmY5O31Mw' length='500' width='550'>
<img src ='https://private-user-images.githubusercontent.com/180368689/445102692-d6ec10fe-3136-4e16-a196-3865ff4e10e2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc2NTIyMTYsIm5iZiI6MTc0NzY1MTkxNiwicGF0aCI6Ii8xODAzNjg2ODkvNDQ1MTAyNjkyLWQ2ZWMxMGZlLTMxMzYtNGUxNi1hMTk2LTM4NjVmZjRlMTBlMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxOVQxMDUxNTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yODAwZTM1MGE0NjJjYTkxMzNkNzY4NzM2NzIwZWFiMDcwZjQ2OTJiZDFhYWEzYzVlYWY5NjE5MmQ4NWZjZWQwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.GIZMcS5ghgDx9mvGg84OC6ygCa4SsQ1QfwRXUBVK7ic' length='500' width='550'>

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
