### Exercises

> Create a new repository on GitHub to hold your assignments for the Databases module. Create a new branch for Checkpoint 1. Submit your answers.



> 1) What data types do each of these values represent?

1. "A Clockwork Orange"
1. 42
1. 09/02/1945
1. 98.7
1. $15.99



> 2) Explain when a database would be used. Explain when a text file would be used.



> 3) Describe one difference between SQL and other programming languages.



> 4) In your own words, explain how the pieces of a database system fit together at a high level.



> 5) Explain the meaning of `table`, `row`, `column`, and `value`.




> 6) List three data types that can be used in a table.



> 7) Given this [`payments`](https://www.db-fiddle.com/f/5gVGFmB8Aq66SejCFEbfdd/0) table, provide an English description of the following queries and include their results:

```SQL
     SELECT date, amount
     FROM payments;
```

```SQL
     SELECT amount
     FROM payments
     WHERE amount > 500;
```

```SQL
     SELECT *
     FROM payments
     WHERE payee = 'Mega Foods';
```



> 8) Given this [`users`](https://www.db-fiddle.com/f/iQAEYktwysXqcLQHv2dwbc/0) table, write SQL queries using the following criteria and include the output:

- The email and sign-up date for the user named DeAndre Data.
- The user ID for the user with email 'aleesia.algorithm@uw.edu'.
- All the columns for the user ID equal to 4.



#### Additional practice:
- [SQLCourse](http://www.sqlcourse.com/intro.html)
- [HackerRank](https://www.hackerrank.com/domains/sql/select)
