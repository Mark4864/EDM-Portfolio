# Final Lab Task 1 - MySQL Basics

## Step 1: Create a table named $\color{orange}{\textsf{employee}}$ with the following fields:
- **employee_id**: Unique integer, auto-increment, primary key.
- **employee_name**: String (VARCHAR) with up to 255 characters, not null.
- **manager_id**: Integer, foreign key referencing **employee_id** in the same table (**employees)**.
## Step 2: Create a table named $\color{orange}{\textsf{departments}}$ with the following fields:
- **department_id**: Unique interger, auto-increment,primary key.
- **department_name**: String (VARCHAR) with up to 255 characters, not null.
## Step 3: Create a table named $\color{orange}{\textsf{employee departments}}$ with the following fields:
- **employee_id**: Interger, foreign key referencing **employee_id** in **employees**.
- **department_id**: Interger, foreign key referencing **department_id** in **departments**.
- Composite primary key (**employee_id**, **department_id**).
## Step 4: Create a table named $\color{orange}{\textsf{employee projects}}$ with the following fields:
- **employee_id**: Interger, foreign key referencing **employee_id** in **employees**.
- **project_name**: String (VARCHAR) with up to 255 characters, not null.
## Step 5: Create a table named $\color{orange}{\textsf{managers}}$ with the following fields:
- **manager_id**: Unique interger, auto_increment, primary key.
- **employee_id**: Interger, foreign key referencing **employee_id** in **employees**.
