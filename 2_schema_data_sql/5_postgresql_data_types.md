# PostgreSQL Data Types
- Integer values limited at +/- 2 billion
- **NULL**: Most important thing is it behaves different than the nothing value in other languages
  - When `NULL` appears on either side of any ordinary comparison operator (=, <, >), the operator will return NULL instead of true or false.
  - psql displays empty output for NULL values so always use `IS NULL` AND `IS NOT NULL` constructs
  