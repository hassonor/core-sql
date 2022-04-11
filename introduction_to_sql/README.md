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


### Filtering Results with the `ORDER BY` and `GROUP BY`:

`ORDER BY`:
* Allows sorting of results set
* After the `WHERE` clause (if there is one)
* Specify one or more columns
* Separate columns by commas
* ASC (default) or DESC

"Who are all the people in my contact list, ordered by last name?"
`SELECT c.last_name, c.first_name FROM contacts c ORDER BY c.last_name;`

#### Set Function: 
* Computes new values from column values
* Use in place of columns in `SELECT` clause
* Passes column name to function
* Helps us to ask more interesting questions
* Often used with the `DISTINCT` qualifier
___
* `COUNT` - Count of the column specified (includes NULL values if * is used)
* `NAX` - Maximum value of the column (does not include NULL values).
* `MIN` - Minimum value of the column (does not include NULL values).
* `AVG` - Average value of the column (does not include NULL values, only numeric column).
* `SUM` - Sum value of the column (does not include NULL values, only numeric column).

___
"What is the total number of times I've contacted my contacts?"
`SELECT SUM(p.contacted_number) FROM person p;` <br>
"What is the count of unique first names among my contacts?"
`SELECT COUNT(DISTINCT p.first_name) FROM person p;` <br>
___
`GROUP BY`:
* Allows multiple columns with a set function
* Break result set into subsets
* Runs set function against each subset
* Result set returns 1 row per subset
* Subset is dictated by column in `GROUP BY`
* Column must appear in the SELECT LIST
* Appears after `FROM` and/or `WHERE` Clauses

"What is the count of every unique first name among my contacts?"
`SELECT COUNT(p.first_name), p.first_name FROM person p GROUP BY p.first_name;`

`HAVING`:
"What is the count of unique first names among my contacts that appear at least 5 times?"
`SELECT COUNT(DISTINCT p.first_name), p.first_name FROM person p GROUP BY p.first_name
HAVING COUNT(DISTINCT p.first_name) >=5;`
___
#### INNER JOIN
* Most typical `JOIN`
* Emphasizes relation nature of database
* Matches column in first table to second
* Primary key to foreign key is most common

"What are my contacts' email addresses?" <br>
`SELECT p.first_name, p.last_name, e.email_address FROM person p INNER JOIN email_address e ON p.person_id = e.email_address_person_id;`
___
#### OUTER JOIN
* `INNER JOIN` doesn't deal with `NULL` values
* `OUTER JOIN` works even when no match
* `NULL` columns if no match in second table
* `FULL OUTER JOIN` return all joined rows
* `NULL` when no match in either table
___
#### LEFT OUTER JOIN
* Another `NULL`-related `JOIN`
* All rows from the left side will be returned
* `NULL` for non-matching right side table
"What are my contacts and their email addresses, including those I don't have an email for?" <br>
`SELECT p.first_name, p.last_name, e.email_address FROM person p LEFT OUTER JOIN email_address ON 
p.person_id = e.email_address_person_id;`

___
#### RIGHT OUTER JOIN
* Opposite of `LEFT OUTER JOIN`
* All rows from the right side will be returned
* `NULL` for non-matching left side table
"What are the email addresses i have included those emails i don't have a person for?"<br>
`SELECT p.first_name, p.last_name, e.email_address FROM person p RIGHT OUTER JOIN email_address 
ON p.person_id = e.email_address_person_id;`
___
#### FULL OUTER JOIN
"What are all my contacts and their email addresses, including the ones missing an email address and the ones with an email address but missing a contact name?"<br>
`SELECT p.first_name, p.last_name, e.email_address FROM person p FULL OUTER JOIN email_address
ON p.person_id = e.email_address_person_id;`
___

### Adding, Changing and Removing Data
___
#### All the commands - AKA CRUD
* SELECT(i.e read)
* INSERT (i.e. create)
* UPDATE 
* DELETE
___
`INSERT`:
* Command is actually INSERT INTO
* Table name after command
* Only one table allowed
* List of columns in parens
* `VALUES` keyword
* List of values in parens
* Values and columns must be equal
`INSRT INTO person (person_id, first_name, last_name, contacted_number, date_last_contacted, date_added)
VALUES (1, 'Or','Hasson',0, NULL, 2000-05-14 11:12:34');`
___
`BULK INSERT`:
* `INSERT` allows only one table and column list
* Insert multiple rows with one statement
* Either multiple values lists or
* `SELECT` statement following table name
`INSERT INTO person p SELECT * FROM old_person op WHERE op.person_id > 300;`
___

`UPDATE`:
* Modifies column(s) in a single table
* `WHERE` clause dictates which rows
  * `SET` keyword follows table name
  `UPDATE email_address e SET e.email_address = 'hassonor@gmail.com' WHERE e.email_address_id = 4;` <br>
___
`DELETE`:
* DELETES one or more rows in a table
* Permanent!
* `DELETE FROM` is actual full command
* `WHERE` clause is __critical__! 
`DELETE FROM person p WHERE p.id=5;`
___
#### Creating Database Tables
`CREATE DATABASE`:
* Oddly not part of the SQL Standard
* Is supported by most implementations
* `USE DATABASE` to scope future queries
* Can also fully qualify table name to database <br>
Example: <br>
  1. `CREATE DATABASE Contact;` 
  2. `USE DATABASE Contact;`<br>`SELECT * FROM person p;` 
  3. `SELECT * FORM Contact.person p;` (FULLY QUALIFIED TABLE NAME)
___
`CREATE TABLE`:
* Is part of SQL Standard
* Followed by table name
* Then list of column definitions
* At minimum column name and type <br>
Create Table Example: <br>
`CREATE TABLE email_address(email_address_id INTEGER, email_address_person_id INTEGER,
email_address VARCHAR(55));` <br>
![Twitter](https://github.com/hassonor/core-sql/blob/master/screenshots/StandardSQLDataTypes.png)
___
`NULL VALUES`:
* `NULL` is a special value in SQL
* indicates lack of a value
* Columns can be required or not required
* Required is `NOT NULL`
___
`NULL` or `NOT NULL`: <br>

#### `NULL`: 
 - Default for column definition
 - Inserting `NULL` value ok


#### `NOT NULL`:
  - Must be specified on column definition
  - Inserting `NULL` value is an error

___
#### `PRIMARY KEY`:
  * Must be a unique value per row
  * Must be `NOT NULL`
  * Can be multiple columns (compound key)
```sql
   CREATE TABLE email_address
   (
    email_address_id
    INTEGER PRIMARY KEY,
    email_address_person_id
    INTEGER,
    email_address
    VARCHAR(55) NOT NULL 
    );
  ```
___
#### `CONSTRAINT`:
 * Way to add keys in one grouping
 * Primary or foreign keys
```SQL
CREATE TABLE phone_number
(
  phone_number_id
  INTEGER NOT NULL,
  phone_number_person_id
  INTEGER NOT NULL,
  phone_number
  VARCHAR(55) NOT NULL,
  CONSTRAINT
  PK_phone_number
  PRIMARY KEY
  (phone_number_id)
)
 ```
___
#### `ALTER TABLE`:
  * Used to change an existing table
  * Add/remove column
  * Change column data type
  * Change column constraints
  * Must comport with current data
  ```StandardSQLDataTypes
  ALTER TABLE 
  email_address
  ADD CONSTRAINT
  FK_email_address_person
  FOREIGN KEY
  (email_address_person_id)
  REFERENCES
  person
  (person_id);
  ```
___
#### `DROP TABLE`:
* Removes table and all data from database
* __BE CAREFUL!__
* Error If table is a foreign key to another table <br>
`DROP TABLE person` 