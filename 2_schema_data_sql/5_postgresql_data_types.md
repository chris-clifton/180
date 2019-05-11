# PostgreSQL Data Types
- Integer values limited at +/- 2 billion
- **NULL**: Most important thing is it behaves different than the nothing value in other languages
  - When `NULL` appears on either side of any ordinary comparison operator (=, <, >), the operator will return NULL instead of true or false.
  - psql displays empty output for NULL values so always use `IS NULL` AND `IS NOT NULL` constructs
  
## Aggregate functions
- Write query to determine average, minimum, and maximum wingspan for birds shown in table
  ```sql
  SELECT round(avg(wingspan), 1), min(wingspan), max(wingspan) FROM birds;
  ```

- Using table (database: practice, table: menu_items)
- Write query to determine which menu item is most profitable based on cost of its ingredients, returning name and its profit
- ``` SELECT round(avg(wingspan), 1), min(wingspan), max(wingspan) FROM birds; ```

- Write query to determine how profitable each item on the menu is based on amount of time it takes to prepare. Assume $13/hr for labor.  List most profitable items first.
  ```sql
  SELECT item, menu_price, ingredient_cost,
       round(prep_time/60.0 * 13.0, 2) AS labor,
       menu_price - ingredient_cost - round(prep_time/60.0 * 13.0, 2) AS profit
  FROM menu_items
  ORDER BY profit DESC;
  ```
  - Notes: must convert integers into floating points in order to work
  - Cannot access alias 'profit' later in same select list and must repeat in query twice