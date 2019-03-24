# Comparing SQL Statements
- Though the details of how a query is actually run are abstracted away by the database engine, it is possible to influence this process by the way you structure your SQL statements

## Assessing a Query with EXPLAIN
- `EXPLAIN` command gives a step by step analysis of how the query will be run intenrally by postgres
- In order to execute each query, postgres devises a plan called a query plan.  The creation of this plan is one step in the path of executing a query
- `EXPLAIN` allows you to access and read the query plan
   - Query plan is structured as a node-tree.  The more 'elements' there are to your query, the more nodes there will be in the tree.
   - Each node consists of the node type along with estimated cost for the node (start-up cost + total cost), estimated number of rows to be output by the node, and estimated average width of rows in bytes
- Cost values calculated by using arbitrary units determined by planner's cost parameters and represent the estimated amount of effort or resources required to execute the query as planned.

## EXPLAIN ANALYZE
- When you use EXPLAIN, the query is not actually run.  The values output are estimates based on planner's knowledge of the schema and assumptions based on postgres system statistics.
- In order to acces a query string actual data you can use ANALYZE option to an EXPLAIN command
- `EXPLAIN ANALYZE SELECT book.title FROM books JOIN authors ON books.author_id = authors.id WHERE authors.name = 'William Gibson';`
- ANALYZE option actually runs the query and in addition to  normal output it includes actual time (in milliseconds) required to run query and its constituent parts