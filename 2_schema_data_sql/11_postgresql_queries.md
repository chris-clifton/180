# How PostgreSQL Executes Queries

- The exact way this is done depends on many variables, but the high-level process that each query goes through can be described as a series of steps.

## Breaking down a `SELECT` query
1. Rows are collected into a virtual derived table
  - You can think of this step as the db creating a new temporary table using the data from all tables listed in the querys `FROM` clause. Includes tables used in `JOIN` clauses.
2. Rows are filtered using `WHERE` conditions
  - All the conditions in the `WHERE` clause are evaluated for each row, those that don't meet the requirements are removed
3. Rows are divided into groups
  - If the query includes a `GROUP BY` clause, the remaining rows are divided into appropriate groups
4. Groups are filtered using `HAVING` conditions
  - `HAVING` conditions are similar to `WHERE` conditions, only they are applied to the values that are used to create groups, not individual rows.
5. Compute values to return using select list
  - Each element in the select list is evaluated, including any functions, and the resulting values are associated witht he name of the column they are from or the name of the last function evaluated, unless a different name is specified with `AS`.
6. Sort results
  - The result set is sorted as specified in an `ORDER BY` clause.  Without this clause, the results are returned in an order that is the result of how the database executed the query and the rows' order in the original tables. Its best to always specify an explicit order if it matters at all
7. Limit results
  - If `LIMIT` or `OFFSET` are included, these are used to adjust which rows in the result are returned.

## From PostgreSQL Docs
1. Conection from app program to PostgreSQL server established- app program transmits query to server and waits to receive results back by server
2. *Parser stage* checks query for correct syntax and creates a query tree
3. *Rewrite system* takes query tree and looks for any rules (stored in system catologs) to apply to query tree.  Performs transformations given rule bodies.
4. *Planner/Optimizer* takes query tree and creates a query plan that will be the input to the executor
5. Executor recursively steps through the plan tree and retrieves rows in the way represented by the plan.  Executor makes use of storage system while scanning relations, performs sorts and joins, evaluates qualifications and finally hands back rows derived.