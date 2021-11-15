# Table type

It is possible to create a table type if you want to reuse some table schema in your code.

```sql
DROP TYPE IF EXISTS dbo.OrderTotalsByYear;

CREATE TYPE dbo.OrderTotalsByYear AS TABLE
(
  orderyear INT NOT NULL PRIMARY KEY,
  qty       INT NOT NULL
);
```

Now you can declare a variable:

```sql
DECLARE @MyOrderTotalsByYear AS dbo.OrderTotalsByYear;
```