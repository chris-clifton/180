# The SQL Language
- SQL is a language used to manipulate the structure and values of datasets stored in a relational database
  - Described as a special purpose language because it is typically used only for a very specific purpose: interacting with databases
- SQL is predominantly a declarative language
  - This means that it describes what needs to be done, but does not detail how to accomplish this objective
  - For the most part the SQL database engine will select the most efficient way to execute a query, but in some circumstances a few hints from a human user can improve performance dramatically
- SQL is really three languages in one, containing many sub-languages for data definition, data manipulation, and data control

  | Sub Language | Controls | SQL Constructs |
  |:-------------|:---------|:---------------|
  |DDL for Data definition language| Relation structure and rules | `CREATE`, `DROP`, `ALTER`|
  |DML for data manipulation language| Values stored within relations|`SELECT`, `INSERT`, `UPDATE`, `DELETE`|
  |DCL for data control language| Who can do what| `GRANT`|

## DDL: Data Definition Language
- Data definition parts of SQL are what allow a user to create and modify the schema stored within a database.  It includes the statements that modify the structure of or rules that govern the data held within the database

## DML: Data Manipulation Language
- This part of the SQL language is what allows a user to retrieve, or modify the data stored within a database.  Some databases consdier the retreival and manipulation as two separate languages themselves but PostgreSQL combines them.

## DCL: Data Control Language
- Tasked with controlling the rights and access roles of the users interacting with a database or table.  

- `CREATE SEQUENCE part_number_sequence;`
  - Modifies characteristics and attributes of a datbase by adding a sequence object to the database structure
  - Does not actually manipulate any data, instead manipulates the data definitions