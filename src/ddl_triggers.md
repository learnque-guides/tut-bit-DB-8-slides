# DDL triggers

You create a database trigger for events with a database scope, such as CREATE TABLE. You create an all server trigger for events with a server scope, such as CREATE DATABASE. SQL Server supports only after DDL triggers; it doesn’t support instead of DDL triggers.

```sql
DROP TABLE IF EXISTS dbo.AuditDDLEvents;

CREATE TABLE dbo.AuditDDLEvents
(
    audit_lsn        INT          NOT NULL IDENTITY,
    posttime         DATETIME2(3) NOT NULL,
    eventtype        sysname      NOT NULL,
    loginname        sysname      NOT NULL,
    schemaname       sysname      NOT NULL,
    objectname       sysname      NOT NULL,
    targetobjectname sysname      NULL,
    eventdata        XML          NOT NULL,
    CONSTRAINT PK_AuditDDLEvents PRIMARY KEY(audit_lsn)
);
```

Eventdata has an XML data type. In addition to the individual attributes that the trigger extracts from the event information and stores in individual attributes, it also stores the full event information in the eventdata column.

```sql
CREATE TRIGGER trg_audit_ddl_events
  ON DATABASE FOR DDL_DATABASE_LEVEL_EVENTS
AS
SET NOCOUNT ON;

DECLARE @eventdata AS XML = eventdata();

INSERT INTO dbo.AuditDDLEvents(
  posttime, eventtype, loginname, schemaname,
  objectname, targetobjectname, eventdata)
  VALUES(
    @eventdata.value('(/EVENT_INSTANCE/PostTime)[1]',         'VARCHAR(23)'),
    @eventdata.value('(/EVENT_INSTANCE/EventType)[1]',        'sysname'),
    @eventdata.value('(/EVENT_INSTANCE/LoginName)[1]',        'sysname'),
    @eventdata.value('(/EVENT_INSTANCE/SchemaName)[1]',       'sysname'),
    @eventdata.value('(/EVENT_INSTANCE/ObjectName)[1]',       'sysname'),
    @eventdata.value('(/EVENT_INSTANCE/TargetObjectName)[1]', 'sysname'),
    @eventdata);
GO
```

where (/EVENT_INSTANCE/TargetObjectName)[1] is XQuerey expression ([https://en.wikipedia.org/wiki/XQuery](https://en.wikipedia.org/wiki/XQuery))

Test trigger:

```sql
CREATE TABLE dbo.T1(col1 INT NOT NULL PRIMARY KEY);
ALTER TABLE dbo.T1 ADD col2 INT NULL;
ALTER TABLE dbo.T1 ALTER COLUMN col2 INT NOT NULL;
CREATE NONCLUSTERED INDEX idx1 ON dbo.T1(col2);
```

Select result from auditing table:

```sql
SELECT * FROM dbo.AuditDDLEvents;
```
