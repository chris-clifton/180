## How to connect to DB server
- To connect via `psql` console:  
  `psql -d sql_book`
- If database name is first argument, `-d` flag may be left out  
  `psql sql_book`

## Useful `psql` Meta Commands
- Since console metacommands are not SQL statements, they don't need a semicolon

| Meta Command | Description | Example |
|:-------------|:------------|:--------|
| `\l` | Lists all db's available in server youre connected to| `\l`|
|`\c $dbname` | Connect to database `$dbname` | `\c blog_development` |
| `\d` | Describe available relations (all tables, views, and sequences) | |
| `\dt` | Show just the tables | `\dt` |
| `\s` | Show just the seuences | `\s` |
| `\d $name` | Show schema/Describe relation of table `$name` | `\d users` | 
| `\?` | List of console commands and options | |
| `\h` | List of available SQL syntax Help topics | |
| `\h $topic` | SQL syntax help on syntax for `$topic`| `\h INSERT` |
| `\q` | Quit | |

