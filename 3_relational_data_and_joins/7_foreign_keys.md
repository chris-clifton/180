# Using Foreign Keys
- A foreign key can be two different, but related things
  - A column that represents a relationship between two rows by pointing to a specific row in another table using its *primary key*.  A complete name for these columsn is foreign key columns
  - A constraint that enforces certain rules about what values are permitted in these foreign key relationships.  A complete name for this type of constraint is foreign key constraint.

## Creating Foreign Key Columns
- To create a foreign key column, just create a column of the same type as primary key column t will point to.  If `products` table uses an `integer` type for it's primary key column, then the `orders` table should also use an `integer` type for `orders.product_id`

## Creating Foreign Key Constraints
- To create foreign key constraint, there are two syntaxes that can be used.  
- First is to add a `REFERENCES` clause to the description of a column in a `CREATE TABLE` statement

  ```sql
    CREATE TABLE orders (
      id serial PRIMARY KEY,
      product_id integer REFERENCES products (id),
      quantity integer NOT NULL
    );
  ```
- Second way is to add foreign key constraint separately, as you would any other constraint (note the use of FOREIGN KEY instead of CHECK)

  ```sql
    ALTER TABLE orders ADD CONSTRAINT orders_product_id_fkey FOREIGN KEY (product_id) REFERENCES product(id);
  ```

## Referential Integrity
- One of main benefits of using foreign key constraints is to preserve the *referential integrity* of the data in database.  It does this by ensuring that every value in a foreign key column exists in the primary key column of the referenced table.  Attempts to insert rows that violate the tables constraints will be rejected.

