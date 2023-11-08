# **Procedures and Functions**

## **Procedures**

Is a subprogram that do not return a value directly. The way to create a procedure, along with its parameters and then execute the procedure is as follows:


```
DECLARE 
   a number; 
   b number; 
   c number;
PROCEDURE calculateArea(x IN number, y IN number, z OUT number) IS 
BEGIN 
   z:=x*y;
END;   
BEGIN 
   c:= 2; 
   b:= 45; 
   calculateArea(z => a, y => b, x => c); 
   dbms_output.put_line(' The area is: ' || a); 
END; 
/
```
**IS** This is the description to denote that the BEGIN-END block corresponds to the body or development of the procedure.

**Note** Since the arrow symbol is used, the order of the parameters is not important because it is telling you what values each parameter should assume.

The following commands are very useful for working with procedures and functions:


```
DECLARE 
   a number; 
PROCEDURE squareNum(x IN OUT number) IS 
BEGIN 
  x := x * x; 
END;  
BEGIN 
   a:= 23; 
   squareNum(a); 
   dbms_output.put_line(' Square of (23): ' || a); 
END; 
```

## Functions

Is a subprogram that returns a single value. The way to create a function, along with its parameters and then execute the function is as follows:



```
CREATE OR REPLACE FUNCTION calculateArea(x IN number, y IN number)  
RETURN number 
IS 
    z number; 
BEGIN 
   z:=x*y; 
return z;
END; 
/
```
### The symbol */* is **IMPORTANT** to separete blocks

To call function 


```
DECLARE 
   a number :=12;
   b number :=2;
   c number; 
BEGIN 
   c := calculateArea(); 
   dbms_output.put_line('Total Area: ' || c); 
END; 
```
There is recursive functions like : 


```
CREATE OR REPLACE FUNCTION fibonacci(x number) 
RETURN number  IS 
   f number; 
BEGIN 
   IF x=0 THEN 
      f := 1; 
   ELSE 
      f := x + fibonacci(x-1); 
   END IF; 
RETURN f; 
END; 
/
```


|Comando|Descripcion|
| :-----: | :----:|
|`CREATE OR REPLACE`|Creates or replaces an existing procedure.|
|`EXCUTE`|Executes the procedure without calling it in a block.|
|`DROP`|Delete a procedure .|
|`IN`|Used for parameters that are read as input.|
|`OUT`|Used for parameters that are read as output.|
|`IN OUT`|Used for parameters that are read as input and output.|
|`=>`|Indica los valores que van a tomar los parametros.|