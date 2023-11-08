# **Blocks and Basic Syntax**

## **Blocks**

We know that PL/SQL is a block-structured language. A PL/SQL block is defined by the keywords `DECLARE`, `BEGIN`, `EXCEPTION`, and `END`, which break up the block into three sections:
  - Declarativo: Statements that declare variables, constants and other elements. The declared elements can be used in that block. They are started with the keyword `DECLARE
  - Executable: Statements that are run when the block is executed. They are started with the `BEGIN` keyword and ended with the `END` keyword.
  - Exception handling: Statements to 'catch' any exception that occurs when an executable is run. They are started with the keyword `EXCEPTION`.

Now, to create a block you only need the 'Executable' section, this means that a block by itself can be executed. Every PL/SQL statement (minus the keywords `DECLARE`, `BEGIN` and `EXCEPTION`) ends with a semicolon (;). The following structure is the basic structure of a block:

```
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

An example with the classic 'Hello World' is the following:

```
DECLARE 
   message  
   VARCHAR2(100):= 'Hello, World!'; 
BEGIN 
   DBMS_OUTPUT.put_line (message); 
END; 
```

We can notice that we do not use the 'Exception' section, because as we already mentioned, only the 'Executable' section is necessary to create a block. Now, in the 'Declare' section, we declare a variable to print later with the `dbms_output.put_line(message)` function. We will see this in more depth later.

This next example block adds an exception section that traps any exception (`WHEN OTHERS`) that might be raised and displays the error message, which is returned by the `SQLERRM` function (provided by Oracle):

```
DECLARE
  message  
  VARCHAR2 (100) := 'Hello World!';
BEGIN
  DBMS_OUTPUT.put_line (message);
EXCEPTION
  WHEN OTHERS
  THEN
    DBMS_OUTPUT.put_line (SQLERRM);
END;
```

## **Delimiters**

A delimiter is a symbol with a special meaning. The following are the delimiters:

| Delimiter | Description | 
| :----: | :----: |
| +, -, *, / | Addition, subtraction/negation, multiplication, division |
| % | Attribute indicator |
| ' | Character string delimiter |
| . | Component selector |
| (,) | Expression or list delimiter |
| : | Host variable indicator |
| , | Item separator |
| " | Quoted identifier delimiter |
| = | Relational operator |
| @ | Remote access indicator |
| ; | Statement terminator |
| := | Assignment operator |
| >= | Association operator |
| || | Concatenation operator |
| ** | Exponentiation operator |
| <<, >> | Label delimiter (begin and end) |
| /*, *, */ | Multi-line comment delimiter (begin and end) |
| -- | Single-line comment indicator |
| .. | Range operator |
| <, >, <=, >= | Relational operators |
| <>, '=, ~=, ^= | Different versions of NOT EQUAL |
