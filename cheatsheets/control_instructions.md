# **Control Instructions**

## **Conditional**
Almost every piece of code you write will require conditional control, that is, the ability to direct the flow of execution through your program, based on a condition. You do this with `IF`-`THEN`-`ELSE` and `CASE` statements.

Each `IF` statement is finished with `END IF` and each `CASE` statement is finished with `END CASE`. There are several types of the `IF` statement:
  - `IF THEN`
  - `IF THEN ELSE`
  - `IF THEN ELSIF ELSE`

Aswell, there are two types of the `CASE` statement:
  - **Simple:** This one associates each of one or more sequences of PL/SQL statements with a value. The simple CASE statement chooses which sequence of statements to execute, based on an expression that returns one of those values.
  - **Searched:** This one chooses which of one or more sequences of PL/SQL statements to execute by evaluating a list of Boolean conditions. The sequence of statements associated with the first condition that evaluates to TRUE is executed.

Then:

| Statement | Description | 
| :----: | :---- |
| `IF THEN` | The IF statement associates a condition with a sequence of statements enclosed by the keywords THEN and END IF. If the condition is true, the statements get executed and if the condition is false or NULL then the IF statement does nothing. |
| `IF THEN ELSE` | IF statement adds the keyword ELSE followed by an alternative sequence of statement. If the condition is false or NULL, then only the alternative sequence of statements get executed. It ensures that either of the sequence of statements is executed. |
| `IF THEN ELSIF ELSE` | Selects a condition that is TRUE from a series of mutually exclusive conditions and then executes the set of statements associated with that condition. |
| Simple `CASE` | selects one sequence of statements to execute. However, to select the sequence, the CASE statement uses a selector rather than multiple Boolean expressions. A selector is an expression whose value is used to select one of several alternatives. |
| Searched `CASE` | The searched CASE statement has no selector, and it's WHEN clauses contain search conditions that yield Boolean values. |

We will provide an example for each conditional.
  - **IF THEN**
    ````
    IF l_salary > 40000 OR l_salary 
    IS NULL
    THEN
      give_bonus (l_employee_id,500);
    END IF;
    ````
  - **IF THEN ELSE**
    ````
    IF NVL(l_salary,0) <= 40000
    THEN
      give_bonus (l_employee_id, 0);
    ELSE
      give_bonus (l_employee_id, 500);
    END IF;
    ````

    The `NVL` function will return 0 whenever salary is NULL, ensuring that any employees with a NULL salary will also get no bonus (those poor employees).

  - **IF THEN ELSIF ELSE**
    ````
    IF l_salary BETWEEN 10000 AND 20000
    THEN
      give_bonus(l_employee_id, 1000);
    ELSIF l_salary > 20000
    THEN
      give_bonus(l_employee_id, 500);
    ELSE
      give_bonus(l_employee_id, 0);
    END IF;
    ````

  - **SIMPLE CASE**
    ````
    CASE l_employee_type
    WHEN 'S' 
    THEN
        award_bonus (l_employee_id);
    WHEN 'H' 
    THEN
        award_bonus (l_employee_id);
    WHEN 'C' 
    THEN
        award_commissioned_bonus (
            l_employee_id);
    ELSE
        RAISE invalid_employee_type;
    END CASE;
    ````

  - **SEARCHED CASE**
    ````
    CASE
    WHEN l_salary 
    BETWEEN 10000 AND 20000 
    THEN
      give_bonus(l_employee_id, 1500);
    WHEN salary > 20000 
    THEN
      give_bonus(l_employee_id, 1000);
    ELSE
      give_bonus(l_employee_id, 0);    
    END CASE;
    ````

    Use searched CASE statements when you want to use Boolean expressions as a basis for identifying a set of statements to execute. Use simple CASE statements when you can base that decision on the result of a single expression.

## **Loop**
PL/SQL provides three kinds of loop constructs:

  - **The `FOR` loop (numeric and cursor):**  With the numeric FOR loop, you specify the start and end integer values, and PL/SQL does the rest of the work for you, iterating through each integer value between the start and the end and then terminating the loop:
  - **The simple (or infinite) loop:** It’s called simple for a reason: It starts simply with the LOOP keyword and ends with the END LOOP statement. The loop will terminate if you execute an `EXIT`, `EXIT WHEN`, or `RETURN` within the body of the loop (or if an exception is raised).
  - **The `WHILE` loop:** The WHILE loop is very similar to the simple loop; but a critical difference is that it checks the termination condition up front. That is, a WHILE loop might not even execute its body a single time.

Loops can be labeled. The label should be enclosed by double angle brackets (`<<` and `>>`) and appear at the beginning of the LOOP statement. The label name can also appear at the end of the LOOP statement.

To finish loops, it's important to know two things:
  1. **DO NOT** use `EXIT` or `EXIT WHEN` statements within `FOR` and `WHILE` loops. You should use a `FOR` loop **only when you want to iterate through all the values** (integer or record) specified in the range. An `EXIT` inside a `FOR` loop disrupts this process and subverts the intent of that structure. A `WHILE` loop, on the other hand, specifies its termination condition in the `WHILE` statement itself. We only use `EXIT` or `EXIT WHEN` in simple (or infinite) loops.
  2. **DO NOT** use `RETURN` or `GOTO` statements within a loop—these cause the premature, unstructured termination of the loop.

We will provide an example for each loop:
  - **FOR**
    ````
    PROCEDURE display_multiple_years (
    start_year_in IN PLS_INTEGER
    ,end_year_in   IN PLS_INTEGER
    )
    IS
    BEGIN
    FOR l_current_year 
    IN start_year_in .. end_year_in
      LOOP
        display_total_sales 
                (l_current_year);
      END LOOP;
    END display_multiple_years;
    ````
  
  - **SIMPLE (OR INFINITE) LOOP**
    ````
    PROCEDURE display_multiple_years (
    start_year_in IN PLS_INTEGER
    ,end_year_in   IN PLS_INTEGER
    )
    IS
    l_current_year PLS_INTEGER := start_year_in;
    BEGIN
      LOOP
        EXIT WHEN l_current_year > end_year_in;
        display_total_sales (l_current_year);
        l_current_year :=  l_current_year + 1;
      END LOOP;
    END display_multiple_years;
    ````

  - **WHILE**
    ````
    PROCEDURE display_multiple_years (
    start_year_in IN PLS_INTEGER
    ,end_year_in   IN PLS_INTEGER
    )
    IS
      l_current_year PLS_INTEGER := start_year_in;
    BEGIN
      WHILE (l_current_year <= end_year_in)
      LOOP
          display_total_sales (l_current_year);
          l_current_year :=  l_current_year + 1;
      END LOOP;
    END display_multiple_years;
    ````