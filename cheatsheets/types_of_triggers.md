# **Diference Triggers (BEFORE, AFTER  and  INSTEAD OF)**
We have the next table to do de example: 

|NAME|ID|SALARY|
| :-----: | :----: | :----:|
|JHON| 1 | 1500|
|kAREN | 2 | 756000|
|lUIS | 3 | 8500|
|DIOMEDES | 4 | 26000|
|FERNANDO | 5 | 30400|

## **BEFORE**

Usually it is use to validation and update.
```
create table employee ( 
  name varchar(10), 
  id_employee number,
  salary number, 
  primary key (id_employee)
  );
```
```
CREATE OR REPLACE TRIGGER min_Salary
BEFORE INSERT or UPDATE on employee
FOR EACH ROW 

DECLARE
  exception_minimunSalary EXCEPTION;
BEGIN
    
  if(:NEW.salary<1000) then
    RAISE exception_minimunSalary;  
  END IF;
EXCEPTION 

   WHEN exception_minimunSalary THEN 
   RAISE_APPLICATION_ERROR(-20001, 'Employee must have at least a minimun salary');
END;    

```

when it insert in table 

```
Insert into employee values ('kevin',7,450);
```
The result would be :  

```
ORA-20001: Employee must have at least a minimun salary ORA-06512: at "SQL_PWHOMPNQNMYNZNWJJGOJJBXZS.MIN_SALARY", line 11
```

## **AFTER**
In an example to use *AFTER* is to receive a record to update another table in which it also stores information, in this case a trigger is used for the moment that the information of a product is inserted, also in another table an "automatic" *INSERT* of the product with its respective price is made:

```
CREATE OR REPLACE TRIGGER TR_PRODUCTOS_01
  AFTER INSERT ON PRODUCTOS  
  FOR EACH ROW
DECLARE
  -- local variables 
BEGIN
  INSERT INTO PRECIOS_PRODUCTOS
  (CO_PRODUCTO,PRECIO,FX_ACTUALIZACION)
  VALUES
  (:NEW.CO_PRODUCTO,100,SYSDATE);
END ; 
```

## **INSTEAD OF**

**One important information:** In Oracle, you can create an *INSTEAD* OF trigger for a view only. You cannot create an *INSTEAD*  OF trigger for a table. So the command to declarete a trigger is: 

first we create a view and new table called departments:

```
create table departments (
    name varchar(10),
    id_D number,
    location varchar(10),
    id_employee number,
    primary key (id_D),
    foreign key (id_employee) references employee (id_employee)
);
```
And the view:

```
CREATE VIEW vw_employee AS
    SELECT 
        employee.name, 
        salary
    FROM 
        employee
    INNER JOIN departments USING (id_employee);
```
**(Before to do the view, the table that are referenced must be exist).**

```
CREATE OR REPLACE TRIGGER new_customer_trg
    INSTEAD OF INSERT ON vw_customers
    FOR EACH ROW
DECLARE
    l_customer_id NUMBER;
BEGIN
    -- insert a new customer first
    INSERT INTO customers(name, address, website, credit_limit)
    VALUES(:NEW.NAME, :NEW.address, :NEW.website, :NEW.credit_limit)
    RETURNING customer_id INTO l_customer_id;
    
    -- insert the contact
    INSERT INTO contacts(first_name, last_name, email, phone, customer_id)
    VALUES(:NEW.first_name, :NEW.last_name, :NEW.email, :NEW.phone, l_customer_id);
END;
```
Then when it insert in a view, the insert *INSTEAD OF* to do it in the view, it will do in the respective *TABLE(s)*

