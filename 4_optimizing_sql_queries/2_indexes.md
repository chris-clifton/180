# Indexes
- A potential way to optimize database-backed apps is to use indexes to database tables.

## What are Indexes?
- A mechanism that SQL engines use to speed up queries.  They do this by storing indexed data in a table-like structure which can be quickly searched using particular search algorithms
- The results of the search provide a link back to the records to which the indexed data belongs
- Using an index means the database engine can locate column values more efficiently since it doesn't have to search through every record in a table in sequence

## When to use an Index
- Indexing every column in a table ends up with slower tables
  - When you build an index of a field, reads become faster, but every time a row is updated or inserted, the index must be updated as well
  - Now you're updating not only the table but the index as well so thats a performance cost
- As with many other database optimization decisions, there are a lot of choices involved in how to decide whether or not a column should be designated an index
- This conversation is all about trade-offs but there are some useful rules of thumb to help assessing what those trade-offs are:
  - Indexes are best used in cases where sequential reading is inadequate
    - Columns that aid in mapping relationships (such as foreign key columns) or columns frequently used as part of an `ORDER BY` clause are good candidates for indexing
  - They are best used in tables/columns where the data will be read much more frequently than it is created or updated

## Types of Index
- Another decision is which type of index to use
- Different types of indexes use different data structures and different search algorithms

## Creating Indexes
- When you define a `PRIMARY KEY` constraint or a `UNIQUE` constraint, you automatically create an index on that column
- The index is the mechanism by which these constraints enforce uniqueness
- `FOREIGN KEY` constraints do not automatically create an index on a column so you ned to explicitly add one

## Syntax
`CREATE INDEX index_name ON table_name (field_name):`
- If index_name is omitted, postgres automatically generates a unique name for the index.  If you specify your own it must not have been used already.
- Ex: `CREATE INDEX ON books (author_id);`

## Unique and Non-Unique
- When an index is created via `PRIMARY KEY` or `UNIQUE` constraints, it is considered a *unique* index.
- When an index is unique, multiple table rows with equal values for that index are not allowed
- The `books_author_id_idx` we created, for example, is an index that doesn't enforce uniqueness, meaning the same value can occur multiple times in an indexed column (and known as non-unique index).

## Multicolumn Indexes
- Indexes can also be created on more than one column
- Instead of specifying a single column name, you specify more than one:
  `CREATE INDEX index_name ON table_name (field_name_1, field_name_2);`

## Partial Indexes
- Partial indexes are built from a subset of data in a table
- Subset of data is defined by a conditional expression and the index contains entries only for the rows rom the table where the value in the indexed column satisfies the condition
- Can be useful but most of the time you'll use single-column indexes

## Deleting Indexes
- DROP INDEX works by referring to index by name
- Use `\di` to find and display all named indexes in a table
- `DROP INDEX books_author_id_idx;`