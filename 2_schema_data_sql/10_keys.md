# Using Keys
- SQL databases provide keys to solve the problem of uniquely identifying a row in a database table.

## Natural Keys
- Natural keys are an existing value in a dataset than can be used to uniquely identify each row of data in the dataset.  On the surface, there appear to be a lot of values that *might* be satisfactory for this use: a person's phone number, email address, SSN, or product number.
- Not a good solution as all of these things can change or should not be made available to everyone
- Adding several of these values together makes a composite key, but also doesn't solve the problem.

## Surrogate Keys
- A Surrotage key is a value that is created soley for the purpose of identifying a row of data in a database table
- Most common is the auto-incrementing integer and its common to call the surrogate key for a table **id**.
  `CREATE TABLE colors (id serial, name text);`
- We don't need to create ID values for new rows, they happen automatically
- Serial columns are actuall short-hand for a column definition that is much longer
- A **sequence** is a special kind of relation that generates a series of numbers.  A sequence will remember the last number it generated, so it will generate numbers in a predetermined sequence automatically.
- Once a number is returned by `nextval` for a standard sequence it will not be returned again, regardless of whether the value was stored in a row or not

## Primary Keys
- PostgreSQL can use Primary Keys to create columns with a default auto-incrementing value
  `CREATE TABLE more_colors (id int PRIMARY KEY, name text);`
- By specifying `PRIMARY KEY`, PostgreSQL will create an index on that column that enforces it holding unique values in addition to preventing the column from holding NULL values.
- It is, for the most part, the same as:
  `CREATE TABLE more_colors (id int NOT NULL UNIQUE, name text);`
- The difference between the two is documenting your intention as a database designer.  By  using Primary Key, the fact that a certain column can be relied upon as a way to identify specific rows is baked into the table's schema
- Following conventions in software development saves time, reduces confusion, and minimizes the amount of time needed to get up to speed on a new project

## Primary Key Conventions:
1. All tables should have a primary key column called `id`
2. The `id` column should automatically be set to a unique value as new rows are inserted into the table.
3. The `id` column will often be an integer, but there are other data types (such as UUIDs) that can provide specific benefits

### UUUID
- Universally Unique Identifiers are very large numbers that are used to identify individual objects or, when working witha database, rows in a database
- Often represented using hexadecimal strings (super big, as well)