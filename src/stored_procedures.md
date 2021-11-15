# Stored procedures

Stored procedures are routines that encapsulate code. They can have input and output parameters, they can return result sets of queries, and they are allowed to have side effects. Not only can you modify data through stored procedures, you can also apply schema changes through them.

* Stored procedures encapsulate logic. 
* Stored procedures give you better control of security. You can grant a user permissions to execute the procedure without granting the user direct permissions to perform the underlying activities.
* You can incorporate all error-handling code within a procedure, silently taking corrective action where relevant.
* Stored procedures give you performance benefits.

```sql
DROP PROCEDURE IF EXISTS spCalculateOutput;

CREATE PROCEDURE spCalculateOutput
    @Value1 float
    ,@Value2 float
    ,@Operator char(10)
    ,@Result float Output
AS
    IF @Operator = 'Add'
        SET @Result = @Value1 + @Value2
    ELSE IF @Operator = 'Subtract'
        SET @Result = @Value1 - @Value2
    ELSE IF @Operator = 'Multiply'
        SET @Result = @Value1 * @Value2
    ELSE IF @Operator = 'Divide'
        SET @Result = @Value1 / @Value2;

Declare @Out float

Execute spCalculateOutput 123, 456, 'Add', @Result = @Out Output

Print @Out
```