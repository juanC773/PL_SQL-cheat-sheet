# **Triggers**
Triggers are stored programs, which are automatically executed or fired when some events occur. Triggers are, in fact, written to be executed in response to any of the following events:
  - A database manipulation (DML) statement (DELETE, INSERT, or UPDATE)
  - A database definition (DDL) statement (CREATE, ALTER, or DROP).
  - A database operation (SERVERERROR, LOGON, LOGOFF, STARTUP, or SHUTDOWN).

## **Creating Triggers**
The syntax for creating a trigger is

```
CREATE [OR REPLACE ] TRIGGER trigger_name  
{BEFORE | AFTER | INSTEAD OF }  
{INSERT [OR] | UPDATE [OR] | DELETE}  
[OF col_name]  
ON table_name  
[REFERENCING OLD AS o NEW AS n]  
[FOR EACH ROW]  
WHEN (condition)   
DECLARE 
   Declaration-statements 
BEGIN  
   Executable-statements 
EXCEPTION 
   Exception-handling-statements 
END; 
```
Where

  - **CREATE [OR REPLACE] TRIGGER trigger_name** − Creates or replaces an existing trigger with the trigger_name.

  - **{BEFORE | AFTER | INSTEAD OF}** − This specifies when the trigger will be executed. The INSTEAD OF clause is used for creating trigger on a view.

  - **{INSERT [OR] | UPDATE [OR] | DELETE}** − This specifies the DML operation.

  - **[OF col_name]** − This specifies the column name that will be updated.

  - **[ON table_name]** − This specifies the name of the table associated with the trigger.

  - **[REFERENCING OLD AS o NEW AS n]** − This allows you to refer new and old values for various DML statements, such as INSERT, UPDATE, and DELETE.

  - **[FOR EACH ROW]** − This specifies a row-level trigger, i.e., the trigger will be executed for each row being affected. Otherwise the trigger will execute just once when the SQL statement is executed, which is called a table level trigger.

  - **WHEN (condition)** − This provides a condition for rows for which the trigger would fire. This clause is valid only for row-level triggers.

For example, the following program creates a row-level trigger for the customers table that would fire for `INSERT` or `UPDATE` or `DELETE` operations performed on the CUSTOMERS table. This trigger will display the salary difference between the old values and new values

```
CREATE OR REPLACE TRIGGER display_salary_changes 
BEFORE DELETE OR INSERT OR UPDATE ON customers 
FOR EACH ROW 
WHEN (NEW.ID > 0) 
DECLARE 
   sal_diff number; 
BEGIN 
   sal_diff := :NEW.salary  - :OLD.salary; 
   dbms_output.put_line('Old salary: ' || :OLD.salary); 
   dbms_output.put_line('New salary: ' || :NEW.salary); 
   dbms_output.put_line('Salary difference: ' || sal_diff); 
END; 
```

When the above code is executed at the SQL prompt, it produces the following result
```
Trigger created.
```
The following points need to be considered here

  - `OLD` and `NEW` references are not available for table-level triggers, rather you can use them for record-level triggers.

  - If you want to query the table in the same trigger, then you should use the `AFTER` keyword, because triggers can query the table or change it again only after the initial changes are applied and the table is back in a consistent state.

  - The above trigger has been written in such a way that it will fire before any `DELETE` or `INSERT` or `UPDATE` operation on the table, but you can write your trigger on a single or multiple operations, for example `BEFORE DELETE`, which will fire whenever a record will be deleted using the `DELETE` operation on the table.