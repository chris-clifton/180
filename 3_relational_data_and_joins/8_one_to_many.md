# One to Many Relationships
- Work with db: https://raw.githubusercontent.com/launchschool/sql_course_data/master/sql-and-relational-databases/relational-data-and-joins/one-to-many-relationships/one-to-many.sql

- The table `calls` is a log of phone calls- a primary key, when call was made, first and last name of the contact, and the number the call was made to
- First thing to notice is there is duplicate data in the table
- Keeping the contact's first and last name in this table is poor design and could lead to **update anomaly**
  - If a contact's name of phone number needs to be changed, we'd need to update every row that contined the information about that contact.  This creates a situation where it would be easy to make the database inconsistent, which means it contains more than one answer for a given question.
- Other issues with this table's schema:
  - We can't store the info for a contact without having placed a call to them.  This is known as **insertion anomaly**.
  - Likewise, we lose all information about a contact if we delete the history of calls made to them.  This is known as **deletion anomany**.
- Duplicate data is usually a waste of space, and as amount of data increases, these kinds of duplications really add up.  But it's best not to worry about how much space it takes to store data when thinking about normalization and instead think about the three anomalies
  - Sometimes it is actually desirable to have data duplicated (or **denormalized**), as it can make some retrieval operations much more efficient.
- **Normalization** is the process of designing schema that minimize or eliminate the possible occurrence of these anomalies.  The basic procedure for normalization involves extracting data into additional tables and using foreign keys to tie it back to its associated data.
  - Recall that a **Foreign key column** is a column that stores references to a primary key elsewhere in the database. Foreign keys usually point to other tables, but there are cases where they will point to rows in the same table.

- Sometimes, when using `JOIN`'s, we want more control over what columns are returned.  For example, if both tables have `id` columns, showing both in the output could be confusing and unnecessary.
- By including a more specific **select list** in the query, the user has more contorl over what columns are returned.  The only downside is that the query becomes substantially larger.
- Consider these two queries:

- First is a regular inner join.  It has a short query but displays too much unnecessary data.
```sql
  SELECT * FROM calls INNER JOIN contacts ON calls.contact_id = contacts.id;

  id |        when         | duration | contact_id | id | first_name | last_name |   number   
  ----+---------------------+----------+------------+----+------------+-----------+------------
    1 | 2016-01-02 04:59:00 |     1821 |          6 |  6 | William    | Swift     | 7204890809
    2 | 2016-01-08 15:30:00 |      350 |         17 | 17 | Yuan       | Ku        | 2195677796
    3 | 2016-01-11 11:06:00 |      111 |         25 | 25 | Tamila     | Chichigov | 5702700921
    4 | 2016-01-13 18:13:00 |     2521 |         25 | 25 | Tamila     | Chichigov | 5702700921
    5 | 2016-01-17 09:43:00 |      982 |         17 | 17 | Yuan       | Ku        | 2195677796
```

- Second is a longer query that returns more specific results and the table is easier to read.
```sql
  SELECT calls.when, calls.duration, contacts.first_name, contacts.last_name, contacts.number
  FROM calls INNER JOIN contacts ON calls.contact_id = contacts.id;

          when         | duration | first_name | last_name |   number   
  ---------------------+----------+------------+-----------+------------
  2016-01-02 04:59:00 |     1821 | William    | Swift     | 7204890809
  2016-01-08 15:30:00 |      350 | Yuan       | Ku        | 2195677796
  2016-01-11 11:06:00 |      111 | Tamila     | Chichigov | 5702700921
  2016-01-13 18:13:00 |     2521 | Tamila     | Chichigov | 5702700921
  2016-01-17 09:43:00 |      982 | Yuan       | Ku        | 2195677796
  (5 rows)
```

# Practice Problems
1. Write a query to add following call data to db:
    |when	|duration	|first_name	|last_name	|number|
    |:----|:--------|:----------|:----------|:-----|
    |2016-01-18 14:47:00	|632	|William	|Swift|	7204890809|

    - Note: the column "when" is an SQL keyword and must be double-quoted to escape and use
    
    `INSERT INTO calls ("when", duration, contact_id) VALUES ('2016-01-18 14:47:00', 632, 26);`

2. Write a query to retrieve call times, duration, and first name for all calls **not** made to William Swift
    - First try: works but can do better.  It works in this case because there aren't two Williams.  We shoud have done first and last name to get best answer.
  `SELECT calls.when, calls.duration, contacts.first_name FROM calls INNER JOIN contacts ON calls.contact_id = contacts.id WHERE contacts.first_name <> 'William';`

  `SELECT calls.when, calls.duration, contacts.first_name FROM calls INNER JOIN contacts ON calls.contact_id = contacts.id WHERE (contacts.first_name || ' ' || contacts.last_name) != 'William Swift';`

  - Note: The use of the string concatenation operator in second example is super useful

3. Write SQL statements to add the following data to db:

    |when	|duration	|first_name	|last_name	|number|
    |:----|:--------|:----------|:----------|:-----|
    |2016-01-17 11:52:00|175|Merve|Elk|6343511126|
    |2016-01-18 21:22:00|79|Sawa|Fyodorov|6125594874|

    ```sql
    INSERT INTO contacts (first_name, last_name, number) VALUES ('Merve', 'Elk', 6343511126);

    INSERT INTO contacts (first_name, last_name, number) VALUES ('Sawa', 'Fyodorov', 6125594874);

    INSERT INTO calls ("when", duration, contact_id) VALUES ('2016-01-17 11:52:00', 175, 27);
    
    INSERT INTO calls ("when", duration, contact_id) VALUES ('2016-01-18 21:22:00', 79, 28);
    ```

4. Add a constraint to `contacts` to prevent duplicate value for `number` column
  `ALTER TABLE contacts ADD CONSTRAINT number_unique UNIQUE (number);`

5. Write statement that attempts to duplicate number for a new contact and fails.
  `INSERT INTO contacts (first_name, last_name, number) VALUES ('Bill', 'Gates', 7204890809);`