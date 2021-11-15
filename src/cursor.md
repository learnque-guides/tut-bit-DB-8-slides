# Cursor

* A cursor—a nonrelational result with order guaranteed among rows.
* For example, query with *ORDER BY* clause returns a so called cursor.
* T-SQL supports an object called cursor which you can use to process rows from a result of a query one at a time and in a requested order.

Disadvantages of cursor:

* When you use cursors you pretty much go against the relational model, which is based on set theory.
* The record-by-record manipulation done by the cursor has overhead. A certain extra cost is associated with each record manipulation by the cursor compared to set-based manipulation.
* With cursors, you write imperative solutions.