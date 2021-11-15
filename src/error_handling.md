# Error handling

SQL Server provides you with tools to handle errors in your T-SQL code. The main tool used for error handling is a construct called TRY. . .CATCH.

No error example:

```sql
BEGIN TRY
  PRINT 10/2;
  PRINT 'No error';
END TRY
BEGIN CATCH
  PRINT 'Error';
END CATCH;
```

Error example:

```sql
BEGIN TRY
  PRINT 10 / 0;
  PRINT 'No error';
END TRY
BEGIN CATCH
  PRINT 'Error';
END CATCH;
```

Let's look at more complicated example :)
