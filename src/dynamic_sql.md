# Dynamic SQL

You can construct a batch of T-SQL code as a character string and then execute that batch. This capability is called dynamic SQL. SQL Server provides two ways of executing dynamic SQL: using the EXEC (short for EXECUTE) command, and using the sp_executesql stored procedure.

Dynamic SQL is useful for:

* *Automating administrative tasks*: For example, querying metadata and constructing and executing a BACKUP DATABASE statement for each database in the instance.
* *Improving performance of certain tasks*: For example, constructing parameterized ad-hoc queries that can reuse previously cached execution plans.

```sql
DECLARE @sql AS VARCHAR(100);
SET @sql = 'PRINT ''This message was printed by a dynamic SQL batch.'';';
EXEC(@sql);
```

*EXEC* is dangerous for SQL inject attacks. It is safe to use *sp_executesql*

The *sp_executesql* stored procedure is an alternative tool to the EXEC command for executing dynamic SQL code.

```sql
DECLARE @sql AS NVARCHAR(100);

SET @sql = N'SELECT orderid, custid, empid, orderdate
FROM Sales.Orders
WHERE orderid = @orderid;';

EXEC sp_executesql
  @stmt = @sql,
  @params = N'@orderid AS INT',
  @orderid = 10248;
```
