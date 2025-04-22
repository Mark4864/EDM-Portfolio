# Final Lab Task 2 - Transforming ER MODEL to Relational Tables

## $\color{orange}{\textsf{Student}}$ Table:
- **username**: String (VARCHAR),up to 50 characters.
## $\color{orange}{\textsf{Assignment}}$ Table:
- **shortname**: String (VARCHAR),up to 50 characters.
- **due_date**: Date, cannot be null.
- **url**: String (VARCHAR),up to 255 characters, can be null.
## $\color{orange}{\textsf{Submission}}$ Table:
- **username**: String (VARCHAR),up to 50 characters.
- **shortname**: String (VARCHAR),up to 50 characters.
- **version**: Integer, represents the version of the submission.
- **submit_date**: Date, cannot be null.
- **data**: Text.
## Query Statements & Table Structure:
### Student:
#### Query:
![screenshot](Images/Student.png)
#### Table:
![screenshot](Images/Student_tbl.png)
### Assignment:
#### Query:
![screenshot](Images/Assignment.png)
#### Table:
![screenshot](Images/Assignment_tbl.png)
### Submission:
#### Query:
![screenshot](Images/Submission.png)
#### Table:
![screenshot](Images/Submission_tbl.png)
## ER Diagram:
![screenshot](Images/ER-DIAGRAM.png)
