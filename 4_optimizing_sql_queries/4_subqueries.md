# Subqueries
- When comparing different queries as part of an optimization process, it can sometimes be useful to test out some subqueries.
- Key thing to understand is that you are using the nested query to generate a set of one or more values, you then use those values as part of an outer query (usually as part of a condition).

## Subquery Expressions
- Subquery expressions are a special set of operators for use specifically within subqueries, most commonly within a conditional subquery

### EXISTS
- Checks whether any rows at all are returned by nested query.  If at least one row is returned, EXISTS is true otherwise it is false.
  `SELECT 1 WHERE EXISTS (SELECT id FROM books WHERE isbn = '9780316005488');`
  - This would return 1 if there is a row within books table with an isbn of 978... and return no rows otherwise.
  - Useful in correlated subqueries

### IN
- IN compares an evaluated expression to every row in the subquery result.  If a row equal to the evaluated expression is found, then the result of IN is true, otherwise it is false.
  `SELECT name FROM authors WHERE id IN (SELECT author_id FROM books WHERE title LIKE 'The%');`

### NOT IN
- Result of NOT IN is true if an equal row is not found, false otherwise
  `SELECT name FROM authors WHERE id NOT IN (SELECT author_id FROM books WHERE title LIKE 'The%');`

### ANY/SOME
- Synonyms and can be used interchangeably.
- Used along with an operator (=, <, >)
- Result is true if any true result is obtained when the expression to the left of the operator is evaluated using theat operator against the results of the nested query
  `SELECT name FROM authors WHERE length(name) > ANY (SELECT length(title) FROM books WHERE title LIKE 'The%');`
- Note that when the = is used, it is equivalent to IN

### ALL
- Result of ALL is true only if all of the results are true when the expression to the left of the operator is evaluated
- When <> or != are used it is equivalent to NOT IN

## When to use Subqueries
- When first formulating queries, you probably aren't testing them for speed.  Optimization usually comes as a later step in a project.
- Before you get to optimization stage, it will just come down to personal preference
- If you need to return data from one table conditional on data from another table but you don't need to return any data from the second table, a subquery may make more logical sense and be more readable. 
- If you need to return data from both tables then you would need to use a join.
