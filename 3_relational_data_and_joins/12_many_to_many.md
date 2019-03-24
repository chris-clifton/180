# Many to Many Relationships
- Relationships where there can be multiple instances on both sides of the relationship.  You can think of them as one-to-many relationships that go from the first table to the second **and** from the second table to the first
- They make use of **join tables** to connect the two entities/relations/tables
- Join tables in Rails have primary keys and treats these tables as first-class entities in the system

- Work with db: https://raw.githubusercontent.com/launchschool/sql_course_data/master/sql-and-relational-databases/relational-data-and-joins/many-to-many-relationships/many_to_many.sql

# Converting a 1:M Relationship to a M:M Relationship
- As apps grow and requirements change, its fairly common for relationships to change as well.
- Sometimes we need to change a 1:M to M:M Relationship
- db: https://raw.githubusercontent.com/launchschool/sql_course_data/master/sql-and-relational-databases/relational-data-and-joins/converting-a-1m-relationship-to-a-mm-relationship/films7.sql