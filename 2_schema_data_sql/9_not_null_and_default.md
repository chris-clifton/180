# NOT NULL and Default Values
- The design of rational databases comes from the work involved in defining a common set of attributes
- The more specific and exact the desgin of the schema, the "neater" and more consistent the data will be
- Relational databases allow a schema designer to build a variety of rules about the data into the system
- These rules allow users of system to make certain assumptions about the data that lead to simpler solutions

- You can't make a column NOT NULL if it already contains NULL values.  Fix by deleting problematic rows and adding them back.

- Result of using an operator on a NULL value = resulting value will also be NULL, which signifies an unknown value.
