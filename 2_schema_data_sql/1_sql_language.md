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
- Example statements: **`CREATE`**, **`ALTER`**, and **`DROP`**
  - **CREATE TABLE** defines the type of information stored in a database table by describing the data and its attributes. It does not actually manipulate any data, but instead manipulates the data definitions. As such, CREATE TABLE statements are part of the DDL sublanguage.
  - **ALTER TABLE** modifies the characteristics and attributes of a table. It does not actually manipulate any data, but instead manipulates the data definitions. As such, ALTER TABLE statements are part of the DDL sublanguage.
  - **DROP DATABASE** removes all data from the database, including any and all tables in the database. In this respect, it manipulates data, so some people think of it as part of DML. However, DROP DATABASE also deletes everything about the structure of the database and its tables. Furthermore, all variants of the DROP statement are generally treated as DDL. In these respects, DROP DATABASE manipulates how the data is structured, so it is considered part of the DDL sublanguage. For our purposes at Launch School, DROP DATABASE is DDL since its main purpose is to operate on data definitions; the deletion of data is merely a side-effect.


## DML: Data Manipulation Language
- This part of the SQL language is what allows a user to retrieve, or modify the data stored within a database.  Some databases consdier the retreival and manipulation as two separate languages themselves but PostgreSQL combines them.
- Example statements: **`SELECT`**, **`INSERT`**, **`UPDATE`**, and **`DELETE`**
  - **SELECT** merely queries (reads) the data in a database. Since it manipulates the data and not the structure of the data, SELECT is part of the DML sublanguage.
  - **INSERT** adds new rows of data into a database. Therefore, it is part of the DML sublanguage since it manipulates the data and not the structure of the data.
  - **UPDATE** modifies specific rows of data in a database. Therefore, it is part of the DML sublanguage since it manipulates the data and not the structure of the data.
  - **DELETE** statements delete specific rows of data in a database. Therefore, it is part of the DML sublanguage since it manipulates the data and not the structure of the data.

## DCL: Data Control Language
- Tasked with controlling the rights and access roles of the users interacting with a database or table. 
- Example statements: `GRANT` and `REVOKE`

- `CREATE SEQUENCE part_number_sequence;`
  - Modifies characteristics and attributes of a datbase by adding a sequence object to the database structure
  - Does not actually manipulate any data, instead manipulates the data definitions

## Truncated return an integer compute truncate
- Use SQL to compute surface area of a sphere with a radius of 26.3, truncated to return an integer


## psql console commands
- **`/d things`**
- This is a trick question. \d is a `psql` console command, not part of SQL. As such, it is not part of any SQL sublanguage. However, it does act something like a DDL statement -- it displays the schema of the named table.

## `CREATE SEQUENCE part_number_sequence;`
- **CREATE SEQUENCE** statements modify the characteristics and attributes of a database by adding a sequence object to the database structure. It does not actually manipulate any data, but instead manipulates the data definitions. As such, CREATE SEQUENCE statements are part of the DDL sublanguage.

- It could also be argued that CREATE SEQUENCE is DML; the sequence object it creates is a bit of data that is used to keep track of a sequence of automatically generated values, so it can be thought of as being part of the data instead of a characteristic of the data. However, all CREATE statements (not just CREATE SEQUENCE) are generally thought of as DDL