# Working with cursor

Working with a cursor generally involves the following steps:
* Declare the cursor based on a query.
* Open the cursor.
* Fetch attribute values from the first cursor record into variables.
* As long as you haven’t reached the end of the cursor (while the value of a function called
@@FETCH_STATUS is 0), loop through the cursor records.
* Close the cursor.
* Deallocate cursor.

Let's examine example :)