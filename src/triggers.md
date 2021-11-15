# Triggers

A trigger is a special kind of stored procedure—one that cannot be executed explicitly. Instead, it’s attached to an event. Whenever the event takes place, the trigger fires and the trigger’s code runs.

SQL Server supports the association of triggers with two kinds of events: 
* Data manipulation events (DML triggers) such as INSERT, 
* Data definition events (DDL triggers) such as CREATE TABLE.
