# What is Relational Data?
- Relational databases are called relational because they persist data in a set of relations.
- Relations are a table- a set of columns and rows of data
- Relationship is a connection between two entities (rows of data)

## Three Levels of Schema
- Conceptual
- Logical
- Physical

### Conceptual Schema
- High level design focused on identifying entities and their relationships
- Entity Relationship Diagram (ERD) represent them well

### Logical Schema
- Somewhere in between big idea of conceptual schema and nitty gritty of physical
- Concerned with physical schema but not the particulars of a specific database type

### Physical Schema
- Low level database-specific design focused on implementation

## One to Many Relationships
- On the ONE side, there is a Primary Key
- On the MANY side, there is a Foreign Key

## Many to Many Relationship
- Always going to be an extra table between two entities to represent the relationship
- This table will hold two foreign keys
- Called JOIN tables

# Database Diagrams: Cardinality and Modality
- **Cardinality**: The number of obejcts on each side of the relationship (1:1, 1:M, M:M)
- **Modality**: Represents if the relationship is required(1) or optional(0)
  - If required, that means there must be at least one instance of that entity
  - Can be thougth of as the lower bound of what is necessary for relationship to exist

## One to One Relationship
- Are actually pretty rare in a real database- most often, if a one-to-one relationship does exist at a conceptual level, the two entities will be joined together at the physical level and included in the same table

# JOIN Video
- FULL OUTER JOIN is a sort of a combination of the LEFT OUTER JOIN and RIGHT OUTER JOIN.  First an inner join is done.  Next, a LEFT OUTER JOIN without an additional INNER JOIN.  Finally, a RIGHT OUTER JOIN is added without an additional INNER JOIN

# As percent percentage join
``` SELECT COUNT(DISTINCT tickets.customer_id) / COUNT(DISTINCT customers.id)::float * 100 AS percent FROM customers LEFT OUTER JOIN tickets on tickets.customer_id = customers.id; ```