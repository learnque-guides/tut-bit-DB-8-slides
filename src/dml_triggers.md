# DML triggers

SQL Server supports two kinds of DML triggers: after and instead of. 
* An after trigger fires after the event it’s associated with finishes and can be defined only on permanent tables. 
* An instead of trigger fires instead of the event it’s associated with and can be defined on permanent tables and views.

In the trigger’s code, you can access pseudo tables called inserted and deleted that contain the rows that were affected by the modification that caused the trigger to fire.

```sql
DROP TABLE IF EXISTS dbo.T1_Audit, dbo.T1;
GO

CREATE TABLE dbo.T1
(
    keycol  INT         NOT NULL PRIMARY KEY,
    datacol VARCHAR(10) NOT NULL
);
GO

CREATE TABLE dbo.T1_Audit
(
    audit_lsn  INT          NOT NULL IDENTITY PRIMARY KEY,
    dt         DATETIME2(3) NOT NULL DEFAULT(SYSDATETIME()),
    login_name sysname      NOT NULL DEFAULT(ORIGINAL_LOGIN()),
    keycol     INT          NOT NULL,
    datacol    VARCHAR(10)  NOT NULL
);
GO

CREATE TRIGGER trg_T1_insert_audit ON dbo.T1 AFTER INSERT
AS
BEGIN
    SET NOCOUNT ON;

    INSERT INTO dbo.T1_Audit(keycol, datacol)
    SELECT keycol, datacol FROM inserted;
END
GO

INSERT INTO dbo.T1(keycol, datacol) VALUES(10, 'a');
INSERT INTO dbo.T1(keycol, datacol) VALUES(30, 'x');
INSERT INTO dbo.T1(keycol, datacol) VALUES(20, 'g');

SELECT * FROM [dbo].[T1_Audit]
```