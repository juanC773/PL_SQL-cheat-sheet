# **Cursors**
Contains information about rows returned by a statement. Two types of cursors are known:
  - Implicit
  - Explicit

##  **Implicit Cursors**

They are created by oracle when instructions are executed and are not called but assigned to a cursor. They are sql commands that allow you to see the information of the instruction, such as whether or not it affected the table and how much it affected it.

|Command|Description|
| :-----: | :----:|
|**sql%found**|Returns true if it affected one or more rows, false otherwise.|
|**sql%notfound**|Returns true if it affected any rows, false otherwise.|
|**sql%isOpen**|Returns false for implicit cursors.|
|**sql%rowCount**|Return the number of affected rows.|

We have the next table Employee:

|NAME|ID|SALARY|
| :-----: | :----: | :----:|
|JHON| 1 | 1500|
|KAREN | 2 | 756000|
|LUIS | 3 | 8500|
|DIOMEDES | 4 | 26000|
|FERNANDO | 5 | 30400|

Then

```
DECLARE  
   total_rows number(2); 
BEGIN 
   UPDATE Employee 
   SET salary = salary + 500; 
   IF sql%notfound THEN 
      dbms_output.put_line('no employee selected'); 
   ELSIF sql%found THEN 
      total_rows := sql%rowcount;
      dbms_output.put_line( total_rows || ' employee selected '); 
   END IF;  
END; 
/    
```
## **Explicit Cursors**
Cursors can be declared, opened, gotten, and closed, as follows:

Considering the above table

**Declaration**
```
CURSOR e_employee IS 
   SELECT name, id, salary FROM employee; 
```

**Open**
```
OPEN e_employee; 
```

**Get**
```
FETCH e_employee INTO nameE, idE, salaryE; 
```


**Close**
```
CLOSE e_employee;
```

We provide an example

```
DECLARE 
   nameE employee.name%type; 
   idE employee.id%type; 
   salaryE employee.salary%type; 
   CURSOR e_employee is 
      SELECT name, id, salary FROM customers where salary>20000; 
BEGIN 
   OPEN e_employee; 
   LOOP 
   FETCH e_employee into nameE, idE, salaryE; 
      EXIT WHEN e_employee%notfound; 
      dbms_output.put_line(idE || ' ' || NameE || ' ' || salaryE); 
   END LOOP; 
   CLOSE e_employee; 
END; 
/
```
