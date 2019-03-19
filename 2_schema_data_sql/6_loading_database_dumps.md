# Loading Database Dumps
- First option is to pipe the SQL file into the `psql` program using redirection on command line to stream SQL file into `psql`'s standard input
  ` $ psql -d my_database < file_to_import.sql`
- This will execute the SQL statements within the `file_to_import.sql` within the `my_database` database.

- If you already have a running `psql` session though, you can import an SQL file using the `\i` meta command
  ` my_database=# \i ~/some/files/file_to_import.sql`

- Does the same thing but doesn't require you to exit a running `psql` session
