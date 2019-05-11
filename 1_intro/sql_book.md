# Intro
## The Importance of Structured Data
- "The more we can organize, find and manage information, the more effectively we can function in our modern world." - Vint Cerf
- **Unstructured Data:**  data that contains information without any structure, like content in emails, books, and images.
- **Structured Data:**  data that can be structured, and organized, such as in tabular format, allowing us to find the data easily and also manage it better.
  - A common way of storing data in a structured manner is to use a relational database
- **Database:**  a structured set of data held in a computer.
- **Table:**  a list of individual but related data entries (table rows), each of which store values for a set of defined, shared attributes (table columns)
  - Each row represents a single set of related data
  - Each column represents a standardized way to store all data for that particular attribute

## Relational Database Management Systems
- **Relational Database**:  a database organized according to the *relational model* of data.
  - The Relational Model defines a set of relations (analogous to tables) and describes the relationships, or connections between them in order to deterine how the data stored in them can interact.
  - Using the relational model elevates our database from data that is represented in a flat, two-dimensional table, to one where we can describe the data in a more complex and detailed way
  - Using a relational DB helps us cut down on duplicated data and provides a much more useful data structure for us to interact with
- A **Relational Database Management System** or **RDBMS**, is esentially a software application, or system, for managing relational databases. An RDBMS allows a user, or another application, to interact with a database by issuing commands using syntax that conforms to a certain set of conventions or standards
  - Many examples: SQLite, MySQL, PostgreSQL, etc.
  - Some are lightweight, easy to install and use, while other are robust, scalable, but are complex to install
  - There are slight variations in commands and syntax but, at their heart, they all use SQL

## SQL
- **SQL**, which stands for *Structured Query Language*, is the programming language used to communicate with a relational database.
- Chose PostgreSQL because of its wide applicability and open source roots
- SQL is a declarative language: when you write an SQL statement you describe what needs to be done, but not exactly how to do it- the exact details of how the query is executed are handled internally by the RDBMS
- **SQL Statement**: An SQL command used to access/use the database or the data within that database via the SQL language
- **SQL Query**: A subset of an SQL Statement.  A query is a way to search, or lookup data within a database, as opposed to updating or changing data.
- No matter which language you uuse, the database and its data will most likely out-live most of the application code in your program.
- Creating a well-designed database is like laying the foundations of a house, and learning SQL and relational database concepts will help you build your applications on a strong foundation

--------------------------------------------------------------------------------------------------------------------

# Interacting With PostgreSQL
- There are many interfaces, or clients, you can use to interact with a RDBMS such as PostgreSQL
  - GUI app, CLI, a programming language, etc.
  - Thing they have in common is they all issue a request, or declaration, and receive a response in return.
  - This is known generallyy as the "client-server" architecture

## PostgreSQL Client Applications
- PostgreSQL comes packaged with a number of client apps.  These are used to interact with PostgreSQL in different ways by issuing a command via the command line
- Some commonly used PostgreSQL client apps are `createdb`, `dropdb`, `pg_dump`, `pg_restore`, and `pg_bench`.
  - Some of these client apps are essentially wrappers around SQL commands
  - `createdb` is a wrapper for SQL command `CREATE DATABASE`.
- One client app we will be using is `psql`.  
- `psql` is PostgreSQL interactive console, or a terminal-based front-end to a PostgreSQL database.
  - It allows you to write queries in SQL syntax, issue those queries to a PostgreSQL database, and see the results of those queries in the terminal window.
  - In that sense, the `psql` console is essentially a REPL, like IRB.
- One thing to be aware of is that PostgreSQL is more tightly coupled to the UNIX environment than some other db systems.
  - It uses native user accounts to determine who is connecting to it (by default)
- Two different types of commands you can issue from the psql console prompt:
  1. Issue psql console meta-commands
  2. SQL queries using standard SQL syntax

## Meta-Commands
- Start Postgress ` psql postgres `
- The syntax for a psql console meta-command is a backslash `\` followed y the command and any optional arguments
  - `\conninfo` is the command for connection information of curernt connection to database
- Meta-commands can be used for a number of different things, such as connecting to a different database, listing tables, describing the structure of a particular table, setting environment variables, etc.
- `\q` quits the psql console and returns to normal command line
- Meta commands do not need to be terminated with a colon

## SQL Statements - Select Statement
- SQL statements are commands issued to the db using SQL syntax
- Always terminate in a semi-colon, meaning you can actually write statements over multiple lines and postgresql will not execute the statement until it reaches the semi-colon
- The `SELECT` statement is used to retrieve data from a database

# SQL Sub-Languages
- SQL can be thought of as comprising of three separate sub-languages, each concerned with a specific aspect of manipulating or interacting with a database.  Three sublanguages are:
  1. **DDL**: Data Definition Language - Used to define the structure of a database and the tables/columns within it.
  2. **DML**: Data Manipulation Language - Used to retrieve or modify data stored in a database. `SELECT` queries are DML.
  3. **DCL**: Data Control Language - Used to determine what various users are allowed to do when interacting with a database.
- This book is concerned with the first two- DDL and DML.

----------------------------------------------------------------------------------------------------------------

# SQL Basics Tutorial

## Set Up
- Create a database we can work with.  
  1. From regular command line enter `createdb ls_burger`
  2. Create a file called `ls_burger.sql` and copy contents from LS course into it
  3. From same directory, run `psql -d ls_burger < ls_burger.sql`
    - This creates a database called `ls_burger`, which contains a table called `orders` with some generic data
  4. Connect to database we created with `psql -d ls_burger`
    - Now in the psql console, are connected to db, and should have a prompt that reads `ls_burger=#`

## Select All
- The `SELECT` keyword is used in a statement to access data from a database.
  - `ls_burger=# SELECT * FROM orders;`
  - Returns all columns from the orders table
- Here's the breakdown  

| Command | Purpose|  
|:--------|:-------|  
| `SELECT`| Keyword identifying type of statement being used.  Retrieves data. |
| `*`     | Wild card. Acts as identifier for all columns in a given table. |
| `FROM`  | Keyword used as clause in `SELECT` statement to identify table data's coming from. |
| `orders'| Name of table from which data is being retrieved. |

- Most of the time when interrogating a database, retrieving all of the data in all the columns is unlikely to be what you want to do. Usually you just want a subset of that data.
  - You can achieve this by only selecting specific columns, or by using criteria to select specific rows.

## Selecting Columns
- Give an argument to `SELECT` to choose a column
  - `ls_burger=# SELECT side FROM orders;`
    - Column `side` is passed to `SELECT` method and it returns all data in the `side` column
  - `ls_burger=# SELECT side, drink FROM orders;`
    - Selects two columns, ordered based on order they are passed in

## Selecting Rows
- Each row has a unique value in the `id` column.  Database tables will often use a column such as this as a means of uniquely identifying a particular row of data.  
- If we wanted to return the data from all the columns for the row where the `id` is `, we can add a `WHERE` constraint to a `SELECT` statement like this:
  - `ls_burger=# SELECT * FROM orders WHERE id = 1;`
- The keyword `WHERE` informs the `SELECT` statement that only rows that match the condition should be returned.
  - The condition must return `true` in order for the row to be returned
  - `=` is treated as an equality operator, not as assignment

## Selecting Columns and Rows
- Combine the syntax for specifying columns and rows to write queries that return very specific data.
- Strings have to use single quotes, double quotes don't work
  -`ls_burger=# SELECT customer_name FROM orders WHERE side = 'Fries';`

## Data vs Schema
- The queries we've messed with so far issue requests to database in form of SQL statements and get back some data as a response
- PostgreSQL knows what the pieces of our queries are because of the strict syntax as well as the roles schema and data play in a database
- **Schema** is concerned with the *structure* of a database.  This structure is defined by things such as the names of tables and table columns, the data types of those columns, and any constraints they may have.
- **Data** is concerned with the *contents* of a database.  These are the actual values associated with specific rows and columns in a database.
- Schema and Data work together in order to let us interact with a database in useful ways.  Schema without data would just be a bunch of empty tables.  Data without schema would bring us back to the idea of unstructured data.

---------------------------------------------------------------------------------------------------------------

# Create and View Databases
- In order to work with tables, we need a place for them to exist: a database
- The database is part of the schema- sort of like the 'outer shell' of a building, with the tables in the database being various rooms
  - Rooms are different sizes and have different things in them, and some might be connected, but all exist in the same building

## Create a Database
- At command line: `createdb sql_book`
- This creates the db and now we can open psql and connect to the db with `psql -d sql_book`
  - `-d` flag specifies the db
- You can view current list of all databases with `\list` command
  - You start with four DB's: `template0`, `template1`, `postgres`, and one for currently logged in user.

### Using a SQL Statement
- The `createdb` command is a "wrapper" for actual SQL syntax
- Could do the same with actual SQL: `CREATE DATABASE a_new_db_name;`
  - The name parameter is mandatory
  - Other optional parameters: db encoding, collation, connection limit, etc.
    - When omitted, PostgreSQL uses default settings
- SQL is not actually case sensitive, but its a good idea to follow the convention since most SQL developers 

### Database Naming
- Keep name self-descriptive
- Names written in snake_case

## Connect to a Database
- When we are in the psql console itself, we can connect to a different databse by using the `\c` or `\connect` meta-commands
- You can check which database you are in with `SELECT current_database();` but you would never need to do this since the prompt just tells you...

## Deleting Databases // Delete Database
- SQL command `DROP DATABASE database_name;`, basically the opposite of `CREATE DATABASE`
- You can't drop the database you are currently connected to this way

### Using dropdb
- `dropdb database_name` issued from the terminal does he same thing
- Obviously these commands require extreme care to use as they cannot be undone

# Summary

| PSQL Command | Notes |
|:-------------|:----- |  
| `\l` or `\list`| Displays all datbases | 
| `\c sql_book` or `\connect sql_book` | Connects to the `sql_book` db |  
| `\q`    | Exits PostgreSQL session and returns to terminal |

| Command-Line Commands | Notes |
|:----------------------|:------|
| `psql -d sql_book` | Starts a `psql` session and connects to the db `sql_book` |
| `createdb sql_book` | Creates a db called `sql_book` |
| `dropdb my_database` | Permanently deletes db named `my_database` and all its data |

| Wrapper Command | SQL Syntax | Notes |
|:----------------|:-----------|:------|
| `createdb sql_book` | `CREATE DATABASE sql_book;` | Creates db named `sql_book`|
| `dropdb sql_book` | `DROP DATABASE sql_book:` | Deletes `sql_book` db and all its data |

------------------------------------------------------------------------------------------------

# Create and View Tables
- `sql_book` database gives us our "outer shell" but we want to get some tables in there
- Database tables, sometimes referred to as relations, and the relationships between those tables are what really provide the strucutre we ned to house our data
- Tables can be used to represent real world abstractions of business logic of an app, such as a customer or an order
- Once created, these tables can be used to store data relevant to that particular abstraction

## Table Creation Syntax
- `CREATE TABLE table_name();`
  - Only difference between table and databse is the empty parenthesis following table name
  - The empty parenthesis is where we place column definitions
    - Each column defintion is generally written on a separate line, separated by a comma
    - Basic format is:
```sql
CREATE TABLE table_name (
  column_1_name column_1_data_type CONSTRAINTS, ...,
  column_2_name column_2_data_type CONSTRAINTS, ...,
  .
  .
  .
  constraints
);
```
- Column names and data-types are a required part of each column definition; constraints are optional
  - Contraints can be defined either at the column level or the table level.

## Creating a `users` table
- In the `sql_book` database, we want to store a list of users; for each user we want to store an id for that user, their username, and whether their account is `enabled` or not.
- In order to have somewhere to contain these different pieces of user data, we need to create a table with an appropriate column for each piece of data
```sql
CREATE TABLE users (
  id serial UNIQUE NOT NULL,
  username CHAR(25),
  enabled boolean DEFAULT TRUE
);
```
- Break this down:
  1. `CREATE TABLE` creates table named users
  2. `id, username, enabled` are the three columns of the table
  3. serial, CHAR(25), boolean: these are the datatypes of the columns
  4. UNIQUE NOT NULL, DEFAULT TRUE: these are constraints

## Data Types
- A data type classifies particular values that are allowed for that column
  - This can help protect db from data of an invalid type being entered

## Common Data Types:
| Column Data Type | Description |
|:-----------------|:------------|
| serial  | Used to create identifier columns for a PostgreSQL db.  They are auto-incrementing integers and cannot contain null value |
| char(N) | Column can contain string of up to N characters in length.  If less than N, filled with space characters |
| varchar(N) | Sting up to N characters in length.  If less than N, remaining string length not used |
| boolean | True or false, displayed as t or f |
| integer or INT | Whole number |
| decimal(precision, scale) | Two args, first being total number of digits in entire number on both sides of decimal.  Second is number of igits in fractional part of number to right of decimal point |
| timestamp | YYYY-MM-DD HH:MM:SS format |
| date | Date but no time |

## Keys and Constraints
- Data types are mandatory part of column definition and constraints are optional but extremely useful
- Keys and constraints are rules that define what data values are allowed in certain columns
- Defining keys and constraints is part of db design process and ensures the data within a db is reliable and maintains its integrity
- Constraints can apply to a specific column, an entire table, more than one table, or an entire schema

## Common Constraints
| Constraint | Notes |
|:-----------|:------|
| UNIQUE | Column is prevented from any duplicate values |
| NOT NULL | Value must be specified and cannot be left empty |
| DEFAULT | If no value is set in this field when record is created, a default is used |

## View the Table
- In a large db with lots of tables, we might want to view a list of all the tables that exist in the db
- `\dt` meta-command shows us a list of all the tables, or relations, in the db
  - Pretty high level and limited amount of info
- Use `\d table_name` to see a snapshot of a table (columns, etc.)
  - Shows column names, data type, collation, nullable, and default values

## Schema and DCl
- Important to note the info returned by `\d` and `\dt` relate only to the schema of the db, not the data ( \dt to see owner of table re: security)
- Some parts of a database's schema are controller and managed by another SQL sub-language DCL(Data Control Language)
- DCL is concerned with controlling who is allowed to perform certain actions within a database, or in other words, the security of a database
- The security settings determined by DCL are also part of the schema
- The `owner` column of a table, for example, could have restrictions added to it so that other users can add, read, update, and elete data from the table, but only the owner can alter the structure of the table or delete the table entirely

## Summary
- Tables created using the `CREATE TABLE` command
- Column definitions go between parenthesis and on separate lines
- Column definitions consist of a column name, data type, and optional constraints
- There are many different data types and they can be used to restrict the data that can be input to a column
- Constraints can also be used on the data that is input to a particular column
- We can view a list of tables or the structures of a particular table in the psql console using meta-commands
- Although database schema is largely a DDL(Data Definition Language), parts of it (like access and permissions) are determined by DCL (Data Control Language)
-----------------------------------------------------------------------------------------

# Alter a Table
- Existing tables can be altered with an `ALTER TABLE` statement
- Part of DDL and is for altering a table schema only
- Basic syntax:  
  `ALTER TABLE table_to_change HOW TO CHANGE THE TABLE additional arguments;`

## Rename a Table
- `ALTER TABLE users RENAME TO all_users;`

## Renaming a Column
- `ALTER TABLE table_name RENAME COLUMN column_name TO new_column_name;`
- `ALTER TABLE all_users RENAME COLUMN username TO full_name;`

## Changing Column's Datatype // alter datatype // change datatype // alter column
- `ALTER TABLE table_name ALTER COLUMN column_name TYPE datatype;`
- `ALTER TABLE all_users ALTER COLUMN full_name TYPE VARCHAR(25);`
- When converting data types, if there is no implicit conversion from the old type to the new type, you need to add a `USING` clause to the statement with an expression that specifies how to compute the new column value from the old.  Sometimes these expressions can be quite complex but a simple form would be something like:
  ```SQL
  ALTER COLUMN column_name
  TYPE new_data_type
  USING column_name::new_data_type
  ```
- Can use comma separated statements and do multiple things at once:
  ```SQL
  ALTER TABLE celebrities
  ALTER COLUMN date_of_birth TYPE date
  USING date_of_birth::date,
  ALTER COLUMN date_of_birth SET NOT NULL;
  ```

## Adding a Constraint
- Instead of altering constraints, like we do columns and datatypes, **we add to or remove constraints** from the column definition.
- Differences constraints column names data types: names/types required, constraints optional. Columns can have only one name/datatype but cna have more than one constraint.
- The syntax for constraints can vary depending on the type of constraint
  - Some types of constraints are considered 'table constraints' (even if they apply to a specific column) and others, such as `NOT NULL` and `DEFAULT` are considered 'column constraints'
  - Column constraints: NOT NULL, DEFAULT
- Adding a column constraint:  
  `ALTER TABLE table_name ALTER COLUMN column_name SET constraint clause;`
- Adding a table constraint:
  `ALTER TABLE table_name ADD CONSTRAINT constraint_name clause;`
  `ALTER TABLE table_name ADD CONSTRAINT constraint_name CONSTRAINT_TYPE (column_name);`

## Removing a Constraint
- Removing constraints also has a couple of forms
- Removing a column constraint:
  `ALTER TABLE table_name ALTER COLUMN column_name DROP CONSTRAINT;
- Removing a table constraint:
  `ALTER TABLE table_name DROP CONSTRAINT constraint_name;
  Example: `ALTER TABLE animals ADD CONSTRAINT unique_binomial_name UNIQUE (binomial_name);`
- If constraint has a name you can use that to drop it without identifying column 
  Example: `ALTER TABLE animals DROP CONSTRAINT unique_binomial_name`

## Adding a Column
- `ALTER TABLE table_name ADD COLUMN new_column_name new_data_type new_constraints;`
- `ALTER TABLE all_users ADD COLUMNS last_login timestamp NOT NULL DEFAULT NOW();`
- `NOW()` is an SQL function that provides the current date and time when it is called
  - alias = `CURRENT_TIMESTAMP`

## Removing a Column
- `ALTER TABLE table_name DROP COLUMN column_name;`

## Dropping Tables
- `DROP TABLE table_name;`
--------------------------------------------------------------------------------------------

# Inserting Data into a Table
- Last section was all about schema: creating db, and how to create, alter, and delete the tables and columsn in it.

## Data and DML
- DML: Data Manipulation Language to add, query, change, and remove data
- DML categorized into four main types:

| DML Type | Purpose |
|:---------|:--------|
| `INSERT` | Add new data into table |
| `SELECT` | AKA Queries to retrieve existing data |
| `UPDATE` | Update existing data |
| `DELETE` | Delete existing data |

## A Bit about Crud
- CREATE, READ, UPDATE, DELETE are analogous to INSERT, SELECT, UPDATE, DELETE

## Insertion Statement Syntax
- `INSERT INTO table_name (column1_name, column2_name,...) VALUES (data_col1, data_col2,...);`
  - Must provide three peices of info: 
    - Table name
    - Names of columns we're adding data to
    - Values we wish to store in the columns
  - For each column specified you must supply a value

## Adding Rows (AKA Tuples)
- Each row is an individual entity, or the logical equivalent of a record, and has a corresponding value for each column in the table
- First digit after `INSERT` return is the `oid`, second is the `count` of rows that were inserted.
  - OID's are basically deprecated and no longer around

## Adding Multiple Rows
- If you're adding lots of data, you don't want to add each record individually
- Syntax is similar except each row of values is comma separated
- You don't need to have each row on a separate line, but its generally good practice
- `INSERT INTO users (full_name) VALUES ('Jane Smith'), ('Harry Potter');`
- `INSERT INTO users (full_name, favorite_color, birthday) VALUES ('Harry Potter', 'red', 06/06/66), ('Jane Smith', 'blue', 08/31/87);`

## Constraints and Adding Data
- Constraints are at the level of stable structure/schema/DDL, but they are primarily concerned with controlling what data can be added to a table.

### Default Values
- Setting a `DEFAULT` value for a column ensures that if a value is not specified for that column in an insert statement, then the default value will be used instead.

### NOT NULL Constraints
- It doesn't always make sense for a column to have a default value- like a column that is specific to each user record, rather than some generic, default name
- NOT NULL ensures that when a new row is added, a value must be specified for that column

### UNIQUE Constraints
- Sometimes, rather than simply ensuring a column has a value, we also want to ensure the value added for that column is unique

### CHECK Constraints
- Some columns don't need unique values, but may need to adhere to some other specific rules
- Limits the type of data that can be included in a column and each new record is checked first to ensure the data conforms to the rules
- `ALTER TABLE users ADD CHECK (full_name <> '');`
  - `<>` in SQL works like `!=` and means 'not equal'

### Escaping Quote Marks
- In the string `'O'leary'`, for example, the single quote would terminate a string in PostreSQL
   - This can be fixed by using two single quotes so that the second escapes the first
   - `'O''Leary'`

-------------------------------------------------------------------------------------

# Select Queries
- `SELECT` Statements are how we query databases
- `SELECT column_name FROM table_name;`
- `SELECT column_name FROM table_name WHERE condition;`
- Things to note:
  - Order of columns in response is order column names are specified in query
  - Keywords tell SQL to do something specific
  - Identifiers tell SQL what to do it to
  - You can use identifiers with the same name as keywords by wrapping them in double quotes like "year"
  - Identifiers and Key Words
      - In a SQL statement such as SELECT enabled, full_name FROM users; there are identifiers and keywords. The identifiers, such as enabled, full_name, and users, identify tables or columns within a table. The keywords, such as SELECT and FROM, tell PostgreSQL to do something specific.
      - SQL is case insensitive so it depends on the assumption that anything that is not a keyword (operator, or function) is an identifier.
      - Best to avoid naming columns the same as keywords but you can double quote them if you have to ex "year"

## ORDER BY
- Instead of just returning only certain rows, you could also want to display the results in a particular sort of order
- `SELECT column_name FROM table_name WHERE condition ORDER BY column_name;`
- Things to note:
  - When ordering booleans, `false` comes before `true`
  - If sort value is the same, the order is arbitrary
- Can specify which way to order as well
- ` SELECT column_name FROM table_name WHERE condition ORDER BY column_name 'ASC'/'DESC';`

## Multiply ORDER BY
- You can order rows by one thing and then *within* any sets of rows which have identical values for that first rule, you can set a second level of ordering (comma separated)
- `SELECT column_name FROM table_name ORDER BY column_1 DESC, column_2 DESC;`
- Just like a `WHERE` clause, you can `ORDER BY` a column even if you aren't including it in column list
- We can set sort direction for each column we are using to order our results (meaning we can switch between `ASC` and `DESC`)

## Operators
- Generally used as part of expression in a `WHERE` clause
- Types: comparison, logical, and string matching

### Comparison Operators
- Used to compare one value to another, usually numerical. 
- Normal operators:  
  - `<`, `>`, `<=`, `>=`, `=`, and `<>` or `!=`
- Also include *comparison predicates* which behave like operators with a special syntax
  - `BETWEEN`, `NOT BETWEEN`, `IS DISTINCT FROM`, `IS NOT DISTINCT FROM`, `IS NULL`, and `IS NOT NULL`
- `NULL` is special value in SQL that represents an **unknown value** (like `nil` in Ruby)
- You can't say `WHERE column_name = NULL`.
- When identifying `NULL`, you must use `IS NULL` or `IS NOT NULL`

### Logical Operators
- `AND`, `OR`, and `NOT`
- `SELECT * FROM users WHERE full_name = 'Harry Potter' OR enabled = 'false';`

### String Matching Operators
- Allows you to add flexibility to conditional expressions by searching for a sub-set of the data within a column
- Search for users with last name Smith in a column of `full_name`
  - `SELECT * FROM users WHERE full_name LIKE '%Smith';`
  - Use `LIKE` about where we'd use an `=` for comparison
  - Use `%` as a wildcard (matches any user with any number of characters followed by Smith)
  - An `_` can be used as a wildcard also, but only represents a single character

## Summary
- `SELECT` statement probably most commonly used statement in SQL



---------------------------------------------------------------------------------------
# More On Select
- Further filter our data with `LIMIT`, `OFFSET`, and `DISTINCT`.

## LIMIT and OFFSET
- Sometimes we don't want *all* the results a `SELECT` statement might return
  - Common in pagination
- `SELECT * FROM users LIMIT 1;`
  - Returns one record from users table
- `SELECT * FROM users LIMIT 1 OFFSET 1;`
  - Returns one record from users table BUT it skips however many rows specified by `OFFSET`, which is in this case 1 meaning we will get the second row returned

## DISTINCT
- Sometimes you have duplicate data and you only want to return unique query results
- `SELECT DISTINCT column_name FROM table_name;`
- `DISTINCT` can be super useful when used in conjunction with other SQL functions like `count()`
  - `SELECT count(full_name) FROM users;`  VS. `SELECT count(DISTINCT full_name) FROM users;`
    - The first option doesn't handle duplicate data while the second does

## Functions
- Functions are a way of working with data in SQL- they are a set of commands included as part of the RDBMS that perform particular operations on fields or data
- Some functions provide data transformations that can be applied before returning results
- Others simply return information on the operations carried out
- Common types: String, Date/Time, Aggregate

### String Functions
- Perform some sort of operation on values whose data type is String

| Function | Example | Notes |
|:---------|:--------|:------|
| `length` | `SELECT length(full_name) FROM users;` | Returns length of every user's name. Can also use in a where clause to filter name | 
| `trim`  | `SELECT trim(leading ' ' from full_name) FROM users;` | If any data in `full_name` column had space in front of the name, `trim` would remove it |

### Date/Time Functions
- Perform operations on date and time data- many take time or timestamp inputs

| Function | Example | Notes |
|:---------|:--------|:------|
| `date_part`| `SELECT full_name, date_part('year', last_login) FROM users;` | Allows us to view a table that only contains a part of a user's timestamp taht we specify.  This query only allows us to see a user's name and the year of their `last_login`.  Sometimes data down to the second is not needed |
|`age`|`SELECT full_name, age(last_login) FROM users;`| The `age` function when passed a single timestamp as an argument calculates the time elapsed between timestamp and current time.  This query allows us to see how long its been since each use last logged in.|

- Example date_part:
  ```sql
  encyclopedia=# SELECT first_name
  encyclopedia-# FROM celebrities
  encyclopedia-# WHERE date_part('year', date_of_birth) = 1958;
  ```

### Aggregate Functions
- Perform aggregation- that is they compute a single result from a set of input values

| Function | Example | Notes |
|:---------|:--------|:------|
|`count`|`SELECT count(id) FROM users;`| Returns number of values in column passed in as argument.  Could find number of users who have enabled account, or have certain last names, etc.|
|`sum`|`SELECT sum(id) FROM users;`| Not to be confused with count- this adds the values of all rows being selected|
|`min`|`SELECT min(last_login) FROM users;`| Returns lowest value in a column for all rows being selected|
|`max`|`SELECT max(last_login) FROM users;`| Returns highest value in a column for all rows being selected|
|`avg`|`SELECT avg(id) FROM users;`| Returns average of numeric type values for all rows being selected.

- Aggregate functions really start to be useful when grouping table rows together (GROUP BY)

### GROUP BY
- Sometimes you need to combine data results together to form more meaningful information
- The GROUP BY statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns
- Ex: count number of users who have accounts that are enabled
- `SELECT count(id) FROM users WHERE enabled = true;` - only shows records where enabled = true
- Using GROUP BY, we can split the query and have it return two separate groups
  - `SELECT enabled, count(id) FROM users GROUP BY enabled;`
  - We don't technically need to include the enabled column in our query but it m akes the output more meaningful as we can clearly see the correlation between the count and the values in enabled.
- If you include columns in the column list alongside the function then those columns **must** also be included in a GROUP BY clause

-------------------------------------------------------------------------
# Update Table

## Updating Data
- Update specific columns
  - ```SQL
    UPDATE table_name SET column_name1 = value1, column_name2 = value2 WHERE expression;
    ```
- Update all rows in a column
  - ```SQL
    UPDATE table_name SET column_name = value;
    ```
- Update specific rows
  - ```SQL
    UPDATE table_name SET column_name = value WHERE expression AND/OR another expression;
    ```

# Deleting Data // Delete Data
- ` DELETE FROM table_name WHERE expression `
- ` DELETE FROM table name` to delete all rows
## Update vs Delete
- Update can update one or more columns within one or more rows using the SET clause.  With Delete, you can only delete one or more entire rows and not particular pieces of data from within those rows.
- Though its not possible to delete specific values within a row, you can approximate this by using NULL.  If you use Update statements to set a specific value to NULL, although its not technically deleting it, we are effectively removing that value.
- In a SET clause you can use `= NULL` since its not being used as comparison and is actually setting the value to NULL.
- If column has a not null constraint, then it is no tpossible to set its value to NULL and an error will be thrown.


# Multiple Tables

## Normalization
- The process of splitting up data across multiple tables, and creating relationships between them is normaliation
  - Purpose: remove duplication and improve data integrity
- Normalization is a deep topic with complex sets of rules to dictate the extent to which a database is judged as normalized.  These rule-sets are known as "normal forms"
- Two main things to know:
  - **The reason for normalization** is to reduce data redundancy and improve data integrity
  - **The mechanism for carrying out normalization** is arranging data in multiple tables and defining relationships between them
- In order to determine which relationships should exist and what the table should be, it's best to "zoom out" and think at a higher level of abstraction (database design)

## Database Design
- The process of Database Design involves defining **entities** to represent different sorts of data and designing **relationships** between those entities.

### Entities
- An entity represents a real world object, or a set of data that we want to model within our database; we can often identify these as the major nouns of the system we're modeling.

### Relationships
- Once the entities are decided, and table schema is pretty much set up, we can start to form the relationships between the entities.
- Create a diagram to show an abstract representation of our various entities and also the relationships between them: this diagram is a simple Entity Relationship Diagram (**ERD**)
- An ERD is a graphical representation of entities and their relationships to each other, and is a commonly used tool in database design.

## Keys
- Keys are a special type of constraint used to establish relationships and uniqueness
- Keys can be used to identify a specific row in the current table, or to refer to a specific row in another table (primary keys and foreign keys)

### Primary Keys
- A unique identifier for a row of data
- Making a column a primary key is essentially equivalent to adding `NOT NULL` and `UNIQUE` constraints to the column
- Syntax to explicitly set primary key in existing table:
  `ALTER TABLE table_name ADD PRIMARY KEY (column_name);`
- Although any table can have `UNIQUE` and `NOT NULL` constraints applied to them, each table can only have one primary key
- It is common practice for the Primary Key to be a column named `id`.

### Foreign Key
- Allows us to associate a row in one table to a row in another table by setting a column in one table as a foreign key and having that column reference another table's primary key column
- This is accomplished using the `REFERENCES` keyword
  `FOREIGN KEY (foreignkey_column_name) REFERENCES target_table_name (primarykey_column_name);`
- By setting up this reference, we're ensuring *referential integrity*
  - Referential integrity is the assurance that a column value within a record must reference an existing value; it it doesn't then an error is thrown
  - In other words, PostgreSQL won't allwo you to add a value to the Foreign Key column of a table if the Primary Key column of the table it's referencing does not already contain that value
- **Add foreign keys to existing table**:
  - ` ALTER TABLE countries ADD FOREIGN KEY (column_name) REFERENCES other_table(other_table_primary_key); `
  
  - ` ALTER TABLE child_table ADD CONSTRAINT constraint_name FOREIGN KEY (c1) REFERENCES parent_table (p1); `
  - ` ALTER TABLE order_items ADD CONSTRAINT order_items_order_id_fkey FOREIGN KEY (order_id) REFERENCES orders (id) ON DELETE CASCADE; `

### Entity Relationships
- One to One
- One to Many
- Many to Many

## One-to-One
- The id that is the primary key of the other table is used as both the primary key and the foreign key of the other table
- Exists when a particular entity instance exists in one table and it can only have one associated entity instance in another table
- Example: a user can only have one address and an address can only belong to one user
- ```sql
  CREATE TABLE addresses (
    user_id int, -- Both a primary and foreign key
    street varchar(30) NOT NULL,
    city varchar(30) NOT NULL,
    state varchar(30) NOT NULL,
    PRIMARY KEY (user_id),
    FOREIGN KEY (user_id) REFERENCES users (id) ON DELETE CASCADE );
  ```

## Referential Integrity
- Concept used when discussing relational data which states that table relationships must always be consistent.
- Different RDBMSes might enforce referential integrity rules differently, but the concept is the same..
- If you try to use an address for a user that already has one, for example, PostgreSQL will thrown an error
- If you try to use an address for a user that doesn't exist, that will also throw an error
- Modality of the relationship allows us to be able to add a user without an address but can't add an address without a user

### The ON DELETE Clause
- `ON DELETE CASCADE` clause means that if the row being referenced is deleted, the row referencing it is also deleted.
- Alternatives to `CASCADE` are `SET NULL` or `SET DEFAULT` which do just sets a new value in appropriate column for that row.
- Determining what to do in situations where you delete a row that is referenced by another row is an important design decision and is part of the concept of maintaining referential integrity.

## One-to-Many
- A one-to-many relationsihp exists between two entities if an entity instance in one of the tables can be associated with multiple records in the other table and the opposite relationship does not exist
  - Ex: a book has many reviews, but a review belongs to only one book
- Unlike one-to-one relationship- primary keys and foreign keys reference different columns
- Primary key will reference it's own ID column usually
- Foreign key will be assigned to a column called `other_table_id` and reference `othertable(othercolumn)`
  - The foreign key column won't be bound to the unique constraint of the primary key so the same value from the id column of the other table will be able to appear multiple times in this column.  In other words, a book can have many reviews.
- Must setup the table being referenced first.  If you try to set up a table and it references another table that doesn't exist or isn't populated with the data, you will get an error.

## Many-to-Many
- Many-to-many relationship exists between two entities when if for one entity instance there may be multiple records in the other table, and vice versa.
- Ex: A user can checkout many books and a book can be checked out by many users (over time)
- In order to implement this sort of relationship, we need to introduce a third, cross-reference table.
  - This table holds the relationship between the two entities, by having two foreign keys, each of which reference the primary key of one of the tables for which we want to create this relationship
  - These tables can have additional columns that provide additional context to the relationship and the association between the two entities
- Can be thought of as combining two one-to-many relationships

------------------------------------------------------------------------------------------------------

# SQL JOINS
- SQL handles queries across more than one table through use of JOINs.
- JOINs are clauses in SQL statements that link two tables together, usually based on the keys taht define the relationship between those two tables.
- Types of JOINS:
  - INNER
  - LEFT OUTER
  - RIGHT OUTER
  - FULL OUTER
  - CROSS
- They all do slightly diferent things but the basic theory behind them all is the same

### JOIN Syntax
- `SELECT [table_name1.column_name1, table_name1.column_name2] join_type JOIN table_name2 ON (join_condition);`
- The first part is essentially the SELECT column_list FROM form we've already seen with slight difference that columnb names are prepended by table names in column list.
- Second part that joins tables : `table_name1 join_type JOIN table_name2 ON (join_condition)`
  - In order to join one table to another, PostgreSQL needs to know several pieces of info:
    - The name of the first table to join
    - The type of join to use
    - The name of the second table to join
    - The join condition
  - This info is combined together using JOIN and ON keywords
  - The part that comes after the `ON` keyword is the *join condition* which defines the logic by which a row in one table is joined to a row in another table
    - In most cases, this join is created using the primary key of one table and the foreign key of table we want to join it with

## Types of Joins

### INNER JOIN
- Returns a result set that contains the common elements of the tables, i.e. the intersection where they match on the joined condition.
- INNER JOINS are the most frequently used JOINS, and are default join type

### LEFT JOIN
- Takes all the rows from one table, defined as the LEFT table, and joins it with a second table
- The JOIN is based on the conditions supplied in the parenthesis
- A LEFT JOIN will always include the rows from the LEFT table, even if there are no matching rows in the table it is JOINed with

### RIGHT JOIN
- Similar to a LEFT JOIN except that the roles between the two tables are reversed and all the rows on the second table are included along with any matching row from the first table

### FULL JOIN
- Combination of LEFT JOIN and RIGHT JOIN
- This type of join contains all of the rows from both of the tables
- Where the join cnodition is met, the rows of the two tables are joined
- Any rows where the join condition is not met, the oclumns for the other table have NULL values for that row

### CROSS JOIN
- Cartesian JOIN returns all rows from one table crossed with every row from the second table
- In other words, the join table of a cross join contains every possible combination of rows from the tables that have been joined.  Since it returns all combos, a CROSS JOIN does not need to match rows using a join condition, therefore it does not have an ON clause
- `SELECT * FROM users CROSS JOIN addresses;`

## Multiple Joins
- It is posisble and common to join more than two tables together
- To join multiple tables together, there must be a logical relationship between the tables involved
- Ex: Users, Checkouts, and Books tables
- ` SELECT users.full_name, books.title, checkouts.checkout_date FROM users INNER JOIN checkouts ON (users.id = checkouts.user_id) INNER JOIN books ON (books.id = checkouts.book_id); `
- Join is implemented by using Primary Key of one table and the Foreign key of that table in a different table

## Aliasing
- Aliasing allows us to specify another name for a column or table and use that name in later parts of query to allow for more concise syntax
- The AS keyword allows us to alias
  ```sql
      SELECT u.full_name, b.title, c.checkout_date
      FROM users AS u
      INNER JOIN checkouts AS c ON (u.id = c.user_id)
      INNER JOIN books AS b ON (b.id = c.book_id);
  ```
- You can get even shorter by leaving out the AS keyword entirely
  - `FROM users u`
  - `FROM users AS u`
  - Both equivalent SQL clauses

### Column Aliasing
- Aliasing isn't just useful for shortening SQL queries, you can also use it to display more meaningful info in our result table
- ` SELECT count(id) AS "Number of Books Checked Out" FROM checkouts; `
  - Gives us more helpful output

## Subqueries
- Although joining tables together is probably the most common way of working with mulitple tables, you can often achieve the same results through use of a subquery
- Imagine executing a SELECT query and then using the results of that SELECT query as a condition in *another* SELECT query
- This is called nesting and the query that is nested is referred to as a **subquery**.
- Example: select users that have no books checked out
  - Find users who's user_id is not in the checkouts table
  - `SELECT u.full_name FROM users u WHERE u.id NOT IN (SELECT c.user_id FROM checkouts c);`
- The `NOT IN` clause compares current user_id to all rows in result of the subquery.  If that ID number isn't part of the subquery results, then the full_name for the current row is added to the results et.
- Other useful Subquery expressions: `IN`, `NOT IN`, `ANY`, `SOME`, and `ALL`.

### Subqueries vs Joins
- As a general rule, JOINS are faster to run than subqueries

## Summary
- One of the most important things to remember about how joins work is that we set a condition that compares a value from the first table (usually a primary key), with one from the second table (usually a foreign key).  If the condition that uses these two values evaluates to true, then the row that holds teh first value is joined with the row that holds the second value.

| JOIN TYPE | Notes |
|:----------|:------|
| INNER | Combines rows from two tables whenever join condition is met |
| LEFT | Same as inner, except rows from first table are added to join table, regardless of evaluation of condition|
| RIGHT | Same as inner, exccept rows from second table are added to join table, regardless of evaluation of condition |
| FULL | A combination of left and right joins |
| CROSS | No join condition- a result of matching of every row from first table with the second table, cross product of all rows across both tables |

- Alias a table to better manage column names and shorten queries
-------------------------------------------------------------------------------------

# JOIN/SUBQUERIES EXERCISES

## 2. Write query to return names and capitals of all European countries
### JOIN with WHERE 
  ```sql
  encyclopedia=# SELECT countries.name, countries.capital
  encyclopedia-# FROM countries JOIN continents
  encyclopedia-# ON countries.continent_id = continents.id
  encyclopedia-# WHERE continents.continent_name = 'Europe';
  ```

## 7. Return a list of all orders and their associated product items
### multiple joins
  ```sql
  encyclopedia=# SELECT countries.name, countries.capital
  encyclopedia-# FROM countries JOIN continents
  encyclopedia-# ON countries.continent_id = continents.id
  encyclopedia-# WHERE continents.continent_name = 'Europe';
  ```

## 8. Return ID of any order that includes Fries. Use table aliasing in query.
### join where alias
  ```sql
  ls_burger=# SELECT o.id
  ls_burger-# FROM orders AS o JOIN order_items AS oi
  ls_burger-# ON o.id = oi.order_id
  ls_burger-# JOIN products AS p
  ls_burger-# ON oi.product_id = p.id
  ls_burger-# WHERE p.product_name LIKE 'Fries';
  ```

## 9. Build on previous query - return name of any customer who ordered fries as "Customers who like fries"- don't repeat same customer name more than once in results
### multiple join
  ```sql
  ls_burger=# SELECT DISTINCT c.customer_name AS "Customers who like Fries"
  ls_burger-# FROM customers AS c JOIN orders as o
  ls_burger-# ON c.id = o.customer_id
  ls_burger-# JOIN order_items AS oi
  ls_burger-# ON o.id = oi.order_id
  ls_burger-# JOIN products AS p
  ls_burger-# ON oi.product_id = p.id
  ls_burger-# WHERE p.product_name = 'Fries';
  ```

## 10. Write query to return total cost of Natash O'Shea orders
### sum multiple join
  ```sql
  ls_burger=# SELECT sum(p.product_cost)
  ls_burger-# FROM customers AS c JOIN orders as o
  ls_burger-# ON c.id = o.customer_id
  ls_burger-# JOIN order_items AS oi
  ls_burger-# ON o.id = oi.order_id
  ls_burger-# JOIN products AS p
  ls_burger-# ON oi.product_id = p.id
  ls_burger-# WHERE c.customer_name = 'Natasha O''Shea';
  ```

## 11. Query to return name of every product included in an order alongside number of times it has been ordered (add order by desc for clarity)
  ```sql
  ls_burger=# SELECT p.product_name, COUNT(oi.id)
  ls_burger-# FROM products AS p JOIN order_items AS oi
  ls_burger-# ON p.id = oi.product_id
  ls_burger-# GROUP BY p.product_name;
  ls_burger-# ORDER BY count DESC;
  ```
  ### same with aliasing
  ```sql
  ls_burger=# select p.product_name AS "Product Name", COUNT(oi.id) as "Total Orders"
  ls_burger=# FROM products p JOIN order_items oi 
  ls_burger=# ON p.id = oi.product_id 
  ls_burger=# GROUP BY p.product_name
  ls_burger=# ORDER BY "Total Orders" DESC;
  ```