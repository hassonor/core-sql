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

__`FROM` Clause__:











