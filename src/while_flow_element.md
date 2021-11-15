# The WHILE flow element

* T-SQL provides the WHILE element, which you can use to execute code in a loop. 
* The WHILE element executes a statement or statement block repeatedly while the predicate you specify after the WHILE keyword is TRUE. When the predicate is FALSE, the loop terminates.

```sql
DECLARE @i AS INT = 1;
WHILE @i <= 10
BEGIN
  PRINT @i;
  SET @i = @i + 1;
END;
```

* If at some point in the loop’s body you want to break out of the current loop and proceed to execute the statement that appears after the loop’s body, use the BREAK command.

```sql
DECLARE @i AS INT = 1;
WHILE @i <= 10
BEGIN
  IF @i = 6 BREAK;
  PRINT @i;
  SET @i = @i + 1;
END;
```

* If at some point in the loop’s body you want to skip the rest of the activity in the current iteration and evaluate the loop’s predicate again, use the CONTINUE command.

```sql
DECLARE @i AS INT = 0;
WHILE @i < 10
BEGIN
  SET @i = @i + 1;
  IF @i = 6 CONTINUE;
  PRINT @i;
END;
```
