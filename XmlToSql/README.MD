# XmlToSql

This script is inspired by a job I had in which we did all of our ETL on a legacy database using SQL queries, copy/paste and find/replace. One way to reduce this was to use dynamic SQL.

After doing dynamic SQL for several months, you start to realize a number of things:

1. It's very repetitive
2. It's hard to debug
3. Generated command strings never looks as good as if they were written by hand

One limitation with trying to introduce abstraction to your dynamic SQL, is the list as a parameter problem. There are a number of ways to do this, for example table types can be used as input parameters, but you must be connected to the proper database. You can also use delimited strings, but then you have to write a custom parser. You may use a previously agreed upon table, but this is not scalable.

So what I've come to use more often is XML strings as parameters. With XML I can define all of the pieces of the command in XML, then use TSQLs built in parser to load the pieces into table variables, and finally create the command strings.

The idea is to support the most common queries: SELECT, INSERT, DELETE, DROP
