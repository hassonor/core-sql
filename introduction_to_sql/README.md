## Introduction to SQL
___
Structured Query Language (SQL) is a special-purpose programming language. <br><br>
__SQL's Purpose__
* To manipulate sets of data
* Typically, from a relational database <br><br>

__Relational__: A way to describe data and the relationships between data entities. <br><br>

_*Normalization*_ Example:

Contacts Table 

| id | first_name    | last_name      |
|-----|------|--------|
| 1   | Or   | Hasson |
| 2   | John | Nash   |

Emails Table 

| Key | person_id | Email                 |
|-----|-----------|-----------------------|
| 1   | 2         | hassonor@gmail.com    |
| 2   | 1         | orhasson777@gmail.com |
| 3   | 1         | orhasson@yahoo.com    |

___

### Basic SQL Commands
___
__*SELECT*__ - Retrieves one or more rows from one or more tables. <br>
example: `SELECT first_name,last_name FROM contacts;`

__*INSERT*__ - Adds one or more rows into a table <br>
example: `INSERT INTO contacts (first_name, last_name) VALUE ('Avi', 'Raul');` <br>

Contacts Table -> (After INSERT)

| id | first_name    | last_name      |
|-----|------|--------|
| 1   | Or   | Hasson |
| 2   | John | Nash   |
| 3   | `Avi` | `Raul`   |

__*UPDATE*__ - Modifies one or more rows in a table. <br>
example: `UPDATE contacts SET last_name = 'Cohen' WHERE id=1;`

Contacts Table ->  (After UPDATE)

| id   | first_name    | last_name |
|-----|------|-----------|
| 1   | Or   | `Cohen`         |
| 2   | John | Nash      |
| 3   | Avi | Raul      |


__*DELETE*__ - Removes one or more rows from one table. <br>
example: `DELETE FROM contancts WHERE id = 2;`


| id | first_name    | last_name |
|-----|------|-----------|
| 1   | Or   | `Cohen`         |
| 3   | Avi | Raul      |

### Querying Data with the `SELECT` Statement 
___
__Example Questions:__
* Who are all my contacts?
* Who are all my contacts with a first name of Avi?
* How many contacts do I have?

__The `SELECT` List__:
* Most of the time it contains a list of columns
* from a table we want to query
* A `FROM` clause is required
* After every column comes a comma
* No comma after the last column

FORMULA: `SELECT <COLUMN_NAME>,<COLUMN_NAME> FROM <TABLE_NAME>;`
example: SELECT first_name, last_name FROM contacts;

__Qualifying Column Name with Table Name__: <br> (GOOD PRACTICE) <br>
`SELECT contacts.first_name, contacts.last_name FROM contacts;`

__Aliasing the Table Name__: <br> (BEST PRACTICE) <br>
`SELECT c.first_name, c.last_name FROM contacts c;`
<br><br>

__*`NOT DISTINCT`*__: <br>
"What are the first names of all the people I know?" <br>
`SELECT c.first_name FROM contacts c;`
<br><br>
__*`DISTINCT`*__: <br>
"What are all **unique** first names of the people I know?"
`SELECT DISTINCT c.first_name FROM contacts c;`

### Filtering Results with the `WHERE` Clause:
___
* Constrains the result set
* Comes after the `FROM` clause
* Contains boolean expressions
* Only matching rows are in the result set

"What is the last name of all the people I know whose first name is Or?" <br>
`SELECT c.last_name FROM contacts c WHERE c.first_name = 'Or';` <br>

__Boolean Operators__:
![Twitter](https://github.com/hassonor/core-sql/blob/master/screenshots/boolean_operators.png)
<br>


`AND`:
* Combines two expressions
* if both are TRUE, row is included
* if either is FALSE, row is excluded

"Who are all the people in my contact list that have the first name Or and have a birthday later than 1987"? <br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.first_name = 'OR' AND c.dob > '31/12/1986';`

`OR`:
* Also combines two expressions
* If either are TRUE, row is included
* If both are FALSE, row is excluded

"Who are all the people in my contact list that have the first name 'Or' or a last name of 'Hasson'"? <br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.first_name = 'Or' OR c.last_name= 'Hasson';`

`BETWEEN`:
* Acts on column and two values
* TRUE if column value is between two values
* inclusive - includes two values (like >= & <=)

"Who are all the people in my contact list that I have contacted at least once but no more than 30 times"?<br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.contacted BETWEEN 1 AND 30;

`LIKE`:
* A more fuzzy version of `=`
* String with special characters inside
* If the match is TRUE, the row is returned

"Who are all the people in my contact list that have a first name that begins with the letter O"?<br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.first_name LIKE "O%";`

`IN`:
* Like a multi-value = operator
* List of potential values
* True if any of the values in the list "hit"

"Who are all the people in my contact list that are name 'Or' or 'Avi'"?<br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.first_name IN('Or','Avi');`

`IS`:
* Special operator
* Like a equals operator
* But just for values that might be NULL

"Who are all the people in my contact list that don't have a last name"?<br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.last_name IS NULL;`

`IS NOT`:
* Just for NULL
* Like a "NOT EQUALS" operator

"Who are all the people in my contact list that have a last name"?<br>
`SELECT c.first_name, c.last_name FROM contacts c WHERE c.last_name IS NOT NULL;`





