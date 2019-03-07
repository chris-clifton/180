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
- The syntax for a psql console meta-command is a backslash `\` followed y the command and any optional arguments
  - `\conninfo` is the command for connection information of curernt connection to database
- Meta-commands can be used for a number of different things, such as connecting to a different database, listing tables, describing the structure of a particular table, setting environment variables, etc.
- `\q` quits the psql console and returns to normal command line
- Meta commands do not need to be terminated with a colon

## SQL Statements
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

## Connecting to a Database
- When we are in the psql console itself, we can connect to a different databse by using the `\c` or `\connect` meta-commands
- You can check which database you are in with `SELECT current_database();` but you would never need to do this since the prompt just tells you...

## Deleting Databases
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
  column_1_name column_1_data_type [constraints, ...],
  column_2_name column_2_data_type [constraints, ...],
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
- Important to note the info returned by `\d` and `\dt` relate only to the schema of the db, not the data
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
