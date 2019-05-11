------------------------------------------------------------------------------------------------------
# Constraints

## NOT NULL

### Add not null constraint to existing column
`ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL`

### Add not null and foreign key to new column
`ALTER TABLE table_name ADD COLUMN column_name column_type NOT NULL REFERENCES other_table_name (other_column_name);`

### Create not null constraint in new column
`CREATE TABLE table_name (
  column_name column_type,
  colomn_name integer REFERENCES other_table_name (other_table_column)
);

## UNIQUE

### Add unique constraint to existing column
`ALTER TABLE table_name ADD CONSTRAINT column_name_is_unique UNIQUE (column_name);`

### Create unique constraint in new column
`CREATE TABLE table_name (
  column_name column_type UNIQUE
);

### Add unique constraint to a combination of volumns
#### Useful in JOIN tables
`ALTER TABLE table_name ADD UNIQUE (column1_name, column2_name);`

## Check Constraint

### Create check constraint in new table/column
`CREATE TABLE table_name (
  column_name column_type CHECK (column_name>0)
);`

### Force value to be in collection and add not null to existing column
`ALTER TABLE table_name ADD CHECK (column_name IN ('value1', 'value2', 'value3', 'value4', 'value5')), ALTER COLUMN column_name SET NOT NULL;`

### Force value using Enumerated data type
`CREATE TYPE column_name_type_enum AS ENUM ('value1', 'value2', 'value3', 'value4', 'value5')
`ALTER TABLE table_name ALTER COLUMN column_name TYPE column_type_enum USING column_name::column_name_enum;`

### Drop Constraint // Remove Constraint
`ALTER TABLE table_name DROP CONSTRAINT constraint_name;`

### Check Constraint Uppercase
`CREATE TABLE table_name (id serial primary key, column_name data_type CHECK (column_name ~ '^[A-Z]{8}$')); `

------------------------------------------------------------------------------------------------------
# Foreign Keys

## Add new column and create foreign key to existing table
`ALTER TABLE table_name ADD COLUMN column_name data_type REFERENCES other_table_name(other_table_column);`

## Add foreign key + on delete cascade to existing column
- Cannot add 'on delete cascade' on its own- if you already made column foreign key, drop the constraint, then add everything back together
`ALTER TABLE table_name ADD CONSTRAINT make_a_constraint_name FOREIGN KEY (column_to_make_into_fkey) REFERENCES other_table_name(other_table_column) ON DELETE CASCADE;


------------------------------------------------------------------------------------------------------
# Data type

## Change data type of existing column
`ALTER TABLE table_name ALTER COLUMN column_name TYPE new_data_type;`

-------------------------------------------------------------------------------------------------------
# String Functions

## string_agg
many_to_many=# 
```sql
select categories.name, count(books.id) as book_count, string_agg(books.title, ', ') as "book_titles" from categories
join books_categories on categories.id = books_categories.category_id
join books on books.id = books_categories.book_id
group by categories.name
order by categories.name;
```

name               | book_count |                                      book_titles      
-------------------+------------+------------------------------------------------------------------------------------------------------------------- 
 Biography         |          2 | Einstein: His Life and Universe, Sally Ride: America's First Woman in Space
 Classics          |          2 | A Tale of Two Cities, Jane Eyre
 Cookbook          |          1 | Vij's: Elegant and Inspired Indian Cuisine
 Fantasy           |          1 | Harry Potter
 Fiction           |          3 | A Tale of Two Cities, Harry Potter, Jane Eyre
 Nonfiction        |          3 | Einstein: His Life and Universe, Sally Ride: America's First Woman in Space, Vij's: Elegant and Inspired Indian Cuisine
 Physics           |          1 | Einstein: His Life and Universe
 South Asia        |          1 | Vij's: Elegant and Inspired Indian Cuisine
 Space Exploration |          1 | Sally Ride: America's First Woman in Space

## Using LIKE on non-string data
` SELECT * FROM table_name WHERE column_name::text LIKE '%parameters'; `

------------------------------------------------------------------------------------------------------
# ALTER TABLE

## Multiple
### Alter data type, add not null constraint, add check > 0, add not null constraint to different column
- Use commas
```sql
ALTER TABLE table_name 
ALTER COLUMN column_name TYPE column_type,
ALTER COLUMN column_name SET NOT NULL,
ADD CHECK (column_name > 0.0),
ALTER COLUMN column2_name2 SET NOT NULL:
```
------------------------------------------------------------------------------------------------------
# Aggregate Functions
- Query that displays description for every service subscribed to by at least 3 customers
```sql
SELECT description, COUNT(service_id)
FROM services
INNER JOIN customers_services
             ON services.id = service_id
GROUP BY description
HAVING COUNT(customers_services.customer_id) >= 3
ORDER BY description;
```
`SELECT column1, COUNT(column2) FROM table1 INNER JOIN table 2 ON join_clause GROUP BY column 1 HAVING COUNT(column2) >= number_desired ORDER BY column 1;`
------------------------------------------------------------------------------------------------------
# Cross Join
- https://launchschool.com/exercises/07237f00
```sql
SELECT sum(price)
FROM customers
CROSS JOIN services
WHERE price > 100;
```
------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------