# Ex. No: 5 Creating Triggers using PL/SQL

# Date 

### AIM: 
To create a Trigger using PL/SQL.


### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```sql
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employedd values(1,'Shakthi','IT',1000000);
insert into employedd values(2,'Suji','SALES',500000)
```
### Create employee table
```sql
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```

### Create salary_log table
```sql
CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```
### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suji','SALES',500000);

-- Update the salary of an employee
UPDATE employedd
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employedd;

-- Display the salary_logg table
SELECT * FROM sal_logg;
```
### Output:
![271356292-6caf3238-451b-44b6-bf6c-a901cd1311b3](https://github.com/sivabalan28/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/113497347/4746d21f-7e3d-4a8b-ae75-455d346d1c9f)

### Result:
Thus , the output has been successfully verified.
