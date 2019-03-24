# Extracting a 1:M Relationship From Existing Data
- Work with db: https://raw.githubusercontent.com/launchschool/sql_course_data/master/sql-and-relational-databases/relational-data-and-joins/extracting-a-1m-relationship-from-existing-data/films3.5.sql

- We'll walk through process of separating data in a single table into two tables and creating a foreign key to connect values that are now stored in two tables instead of one
- Issues with this tables current schema:
  - We can't store a director in DB without adding a film
  - If we remove a film, we remove the director from system
  - Name of director is duplicated in each row
  - When director's name changes, we have to update every row
- Solution
  - Create table to store data for directors
  - Create relationship between new `directors` table and `films` table
    `ALTER TABLE films ADD COLUMN director_id integer REFERENCES directors (id);`
  - Set director_id individually in films table
  - Now set films.director_id to be NOT NULL now that rows contain an value in that column
    `ALTER TABLE films ALTER COLUMN director_id SET NOT NULL;`
  - Drop the `director` column from `films` table as its now redundant
  - Restore the constraint taht was on `films.director` column to `directors.name`
    `ALTER TABLE directors ADD CONSTRAINT valid_name CHECK (length(name) >= 1 AND "position"(name, ' ') > 0);`
  - By using an INNER JOIN and specifying a particular select list, we can retrieve same data in original structure
    `SELECT films.title, films.year, directors.name AS director, films.duration FROM films INNER JOIN directors ON directors.id = films.director_id;`

# NOT NULL or NULL
- In this case we set `films.director_id` to `NOT NULL` to prevent it from ever holding a `NULL` value.  There are some cases though where the value in a foreign key column can be `NULL`.
- A system similar to ours might need to store information about a movie without having a director attached. For example, if this section was part of an internal tool used at a movie studio, many movies typically being process of production before a director is selected, or a director could change and temporarily leave a film with no director
- Usually a good idea to try to keep a table's schema restrictive in order to help preserve the integrity of the data within it.  But keep in mind that the same constraints can help ensure this integrity can also limit what data is stored, and often more importantly, how data can be added and modified.
- Sometimes its necessary to a hve the db in an "invalid" state temporarily while performing certain operations, but this should only be done if there is no other way to proceed.
