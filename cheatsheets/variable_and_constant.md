# **Variable and Constant**

## **Variable**
A variable is as you know is a name given to a storage area that our programs can manipulate.

The way to declare a variable is by means of the following code together with the block:

```
DECLARE
my_variable Varchar(10) := 'Hola mundo';
--OR
my_variable Varchar(10) DEFAULT 'Hola mundo';
BEGIN
 --this space is necesary otherwise there will be an error.
 --TO print the information use the next command.
 dbms_output.put_line('Literal text ',my_variable);
END;
```
*Note*
It is important that there is at least one line break between the Begin and End commands, otherwise an error may occur.

Into *BEGIN* and *END* block you can set values, operate or use command *SELECT* with tables. For example:


```
DECLARE
a Integer := 10;
b Integer := 25;
c Integer;
BEGIN
 --set value.
  a=21;
 --Operate.
c := a+b;
dbms_output.put_line('value = ',c);
 --Use in SELECT with tables.
 --SELECT * FROM ExampleTable WHERE id = a;  

END;
```

Within a blockchain, global variables and local variables can be presented.



```
Following example shows the usage of Local and Global variables in its simple form −

DECLARE 
   -- Global variables  
   num1 number := 95;  
   num2 number := 85;  
BEGIN  
   DECLARE  
      -- Local variables 
      num3 number := 195;  
      num4 number := 185;  
   BEGIN  

   END;  
END; 
```

## **Constant**

The constant is a value that cannot be changed and is declared as follows:



```
DECLARE 
   pi constant number := 3.141592654;
BEGIN  
-process
END
```
The most important is the "constant" command because it is the one that will allow distinguishing variables from constants.







