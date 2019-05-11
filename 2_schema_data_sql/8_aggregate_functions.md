# length
``` SELECT * FROM films WHERE length(title) < 12; ```

# current year
``` SELECT title, extract("year" from current_date) - "year" AS age FROM films ORDER BY age ASC; ```

# count
- Write query to list ten states with most rows in `people` table in descending order
``` SELECT state, count(id) FROm people GROUP BY state ORDER BY count DESC LIMIT 10; ```

# string functions and count
- Write query to list each domain used in an email address in `people` table and how many people have email containing domain
- strpos substr

# UPPER LOWER uppercase lowercase
``` UPDATE people SET given_name = UPPER(given_name) WHERE email LIKE '%teleworm.us'; ```

# AVG average mean round
- Select mean temp from days between march 2 and march 8 rounding decimal to one decimal place
``` select date, round((low + high) / 2.0, 1) from temperatures where date between '2016-03-02' AND '2016-03-08'; ``` 

# Each day, it rains one millimeter for every degree the average temperature goes above 35. Write a SQL statement to update the data in the table temperatures to reflect this. rainfall
  ```sql
  UPDATE temperatures
    SET rainfall = (high + low) / 2 - 35
  WHERE (high + low) / 2 > 35;
  ```

# Create dump
pg_dump -d sql-course -t weather --inserts > dump.sql

# Add unique constraint to existing column
``` alter table films add constraint unique_title unique (title);```

# drop unique constraint on existing column
``` alter table films drop constraint unique_title; ```

# length constraint
``` ALTER TABLE films ADD CONSTRAINT title_length CHECK (length(title) >= 1); ```

# between constraint
``` ALTER TABLE films ADD CONSTRAINT year_range CHECK (year BETWEEN 1900 AND 2100); ```

# Value at least space character constraint
``` ALTER TABLE films ADD CONSTRAINT director_name CHECK (length(director) >= 3 AND position(' ' in director) > 0); ```

# Three ways to use schema to restrict values stored in a column 
  - Data type (wihch can include length limitation)
  - NOT NULL constraint
  - Check constraint