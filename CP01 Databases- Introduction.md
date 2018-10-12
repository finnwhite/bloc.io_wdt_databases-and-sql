### Exercises

> Create a new repository on GitHub to hold your assignments for the Databases module. Create a new branch for Checkpoint 1. Submit your answers.



> 1) What data types do each of these values represent?

1. `"A Clockwork Orange"` - string
1. `42` - number, integer
1. `09/02/1945` - number, date
1. `98.7` - number, float/decimal
1. `$15.99` - number, float/decimal, currency



> 2) Explain when a database would be used. Explain when a text file would be used.

A database is useful when an application works with data that changes frequently and must persist beyond a single session with that application. Databases are built to handle data sets that are large and constantly changing, that need to be efficiently searched and analyzed in multiple ways, that need to be accessed and modified by multiple concurrent users. A good example might be all the data needed to run an online store.

A text file might still be a useful option for taking certain dynamic data outside of the application itself. For limited sets of data that need to live outside the application proper, that dynamically impact the application in some way but are unlikely to change frequently, a text file might be an appropriate solution. A possible use case might be a configuration file that customizes a specific installation of an application.



> 3) Describe one difference between SQL and other programming languages.

**SQL** is a _declarative language_, whereas many other programming languages are _imperative_ or _procedural_. SQL expresses the desired outcome, what the program aims to produce, rather than the specific steps for how the problem should be solved. Imperative or procedural languages enumerate the actual series of steps or function calls that must be executed to accomplish a given task.



> 4) In your own words, explain how the pieces of a database system fit together at a high level.

A database is a piece of software that stores structured data and provides a means to access that data. A database saves information in a machine-readable format that allows it to efficiently store, search, and analyze data of various data types. It also provides or exposes a means to add, modify, and delete data; perhaps via a command line interface, a graphical user interface, or remotely via an API.



> 5) Explain the meaning of `table`, `row`, `column`, and `value`.

These terms describe the conceptual organization of data in a database. A **TABLE** represents a particular list of items or records of a common type, somewhat analogous to a JavaScript array of objects. Each table **ROW** represents a single distinct record, which is a collection of related information, of potentially various data types, about a single parent item, analogous to a JavaScript object or class instance. Each table **COLUMN** represents a field name, which gives meaning to the values stored in that column, similar to a (well-named) JavaScript property or variable name. Each table **VALUE** (or cell, the intersection of a row and column) is the actual piece of data related to its parent record, like a JavaScript variable value.


> 6) List three data types that can be used in a table.

Database tables can store (1) strings, sequences of text characters; (2) numbers, such as integers or whole numbers, and floating point numbers or decimals; and (3) objects.


> 7) Given this [`payments`](https://www.db-fiddle.com/f/5gVGFmB8Aq66SejCFEbfdd/0) table, provide an English description of the following queries and include their results:

```SQL
     SELECT date, amount
     FROM payments;
```

Show me the `date` and `amount` for all `payments`.

date | amount
---- | ------
'2016-05-01' | 1500.00
'2016-05-10' | 37.00
'2016-05-15' | 124.93
'2016-05-23' | 54.72


```SQL
     SELECT amount
     FROM payments
     WHERE amount > 500;
```

Show me the `amount` for all `payments` over $`500`.

amount |
------ |
1500.00 |


```SQL
     SELECT *
     FROM payments
     WHERE payee = 'Mega Foods';
```

Tell me `everything` about all `payments` made by `Mega Foods`.

date | payee | amount | memo
---- | ----- | ------ | ----
'2016-05-15' | 'Mega Foods' | 124.93 | 'Groceries'



> 8) Given this [`users`](https://www.db-fiddle.com/f/iQAEYktwysXqcLQHv2dwbc/0) table, write SQL queries using the following criteria and include the output:

- The email and sign-up date for the user named DeAndre Data.

```SQL
SELECT email, signup
FROM users
WHERE name = 'DeAndre Data';
```

email | signup
---- | ------
'datad@comcast.net' | '2008-01-20'


- The user ID for the user with email 'aleesia.algorithm@uw.edu'.

```SQL
SELECT userid
FROM users
WHERE email = 'aleesia.algorithm@uw.edu';
```

userid |
------ |
1 |


- All the columns for the user ID equal to 4.

```SQL
SELECT *
FROM users
WHERE userid = 4;
```

userid | name | email | signup
---- | ----- | ------ | ----
4 | 'Brandy Boolean' | 'bboolean@nasa.gov' | '1999-10-15'



#### Additional practice:
- [SQLCourse](http://www.sqlcourse.com/intro.html)
- [HackerRank](https://www.hackerrank.com/domains/sql/select)
