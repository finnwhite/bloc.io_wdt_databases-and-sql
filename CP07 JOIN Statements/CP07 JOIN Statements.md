### Exercises

> Submit your answers to the following questions.

> NOTE: Real-world examples must be your own and not based on the text or previous assignments.


> 1) How do you find related data held in two separate data tables?

Data from two (or more) separate tables can be assembled using a `JOIN` clause. The resulting data set is combined based on the "relationship" between the tables, by specifying the "related" columns from each table that form the join condition, or rules for matching rows from one table to rows in the other.



> 2) Explain, in your own words, the difference between an `INNER JOIN`, `LEFT OUTER JOIN`, and `RIGHT OUTER JOIN`. Give a real-world example for each.

The different join types can be thought of in terms of which tables contain _mandatory_ join condition data in order for a combined row to be included in the resulting data set.

In an `INNER JOIN`, _both tables are required;_ only rows where join condition data exists in _both tables_ will appear in the resulting set. An example use case might be retrieving emails from a particular person in your contacts (`FROM messages INNER JOIN contacts ON email_address`).

In a `LEFT OUTER JOIN`, _the first table (**left** of `ON`) is required,_ and the second table is optional. _All rows from the left table_ will appear in the resulting set, and data from the right table will be filled in wherever such data exists (and some rows from the right table might not appear at all). An example use case might be retrieving track info for a playlist (`FROM songs LEFT OUTER JOIN genres ON genre_id`).

In a `RIGHT OUTER JOIN`, _the second table (**right** of `ON`) is required,_ and the first table is optional. _All rows from the right table_ will appear in the resulting set, and data from the left table will be filled in wherever such data exists (and some rows from the left table might not appear at all). An example use case might be retrieving sales figures for specific products (`FROM sales RIGHT OUTER JOIN products ON product_id`).



> 3) Define primary key and foreign key. Give a real-world example for each.

A **primary key** is the column (or set of columns) that uniquely identifies each row in an individual table. Each table can define only _one_ primary key. An example of a primary key might be the `serial_number` in an `inventory` table.

A **foreign key** is any column that contains values that identify rows in external tables, primarily used to facilitate table joins. An example of a foriegn key might be a `merchant_id` in a credit card `expenses` table, referring to the `merchant_id` in a `merchants` table.



> 4) Define aliasing.

**Aliasing** is a useful feature for creating temporary short names (usually a single character) for tables in a SQL query, in the format `<table_name> AS <alias>`, that can be used to make the code more concise and readable.



> 5) Change this query so that you are using aliasing:
```SQL
SELECT professor.name, compensation.salary,
compensation.vacation_days FROM professor JOIN
compensation ON professor.id =
compensation.professor_id;
```

```SQL
SELECT p.name, c.salary, c.vacation_days
  FROM professor AS p
  JOIN compensation AS c
    ON p.id = c.professor_id;
```



> 6) Why would you use a `NATURAL JOIN`? Give a real-world example.

A `NATURAL JOIN` is a shorthand syntax to equi-join two tables `USING` _all columns_ having common names in both tables. This can make the code for joining tables much more concise when there are a number of columns that form the basis for the table "relationship," acting as a sort of multi-column foreign key where there may be no formal id stored in both tables.

This approach is generally considered risky, as adding new columns later can impact the results of the join in unintended ways. Also, not all RDBMSs support natural joins. Therefore, a `NATURAL JOIN` might best be reserved for tables with highly unique column names, highly stable schemas, highly likely to remain on a system known to support natural joins.

A good use case for a `NATURAL JOIN` might be combining two tables that weren't initially designed to be joined, and as such probably have no common formal key columns, but store overlapping data likely to be sufficiently unique in combination, using highly conventional column names. An example might be combining your contacts with a table storing invitations to a baby shower (`FROM shower_guests NATURAL JOIN contacts`), which would probably join on fields like `first_name`, `last_name`, and `address`.



> 7) Using [this Employee schema and data](https://www.db-fiddle.com/f/sG1TKgR15GhH8cjbAwzjAm/0), write queries to find the following information:

> - List all employees and all shifts.

```SQL
SELECT e.name, s.date, s.start_time, s.end_time -- or SELECT *
  FROM employees AS e
  FULL JOIN scheduled_shifts AS ss -- include employees w/o shifts
    ON e.id = ss.employee_id
  FULL JOIN shifts AS s -- include uncovered shifts
    ON ss.shift_id = s.id;
```

| name               | date       | start_time | end_time |
| ------------------ | ---------- | ---------- | -------- |
| Hermione Granger   | 1998-03-09 | 08:00:00   | 16:00:00 |
| Hermione Granger   | 1998-03-10 | 08:00:00   | 16:00:00 |
| Hermione Granger   | 1998-03-11 | 08:00:00   | 16:00:00 |
| Hermione Granger   | 1998-03-12 | 08:00:00   | 16:00:00 |
| Hermione Granger   | 1998-03-13 | 08:00:00   | 16:00:00 |
| Ronald Weasley     | 1998-03-10 | 12:00:00   | 16:00:00 |
| Ronald Weasley     | 1998-03-12 | 12:00:00   | 16:00:00 |
| Luna Lovegood      | 1998-03-09 | 12:00:00   | 16:00:00 |
| Luna Lovegood      | 1998-03-11 | 12:00:00   | 16:00:00 |
| Luna Lovegood      | 1998-03-13 | 12:00:00   | 16:00:00 |
| Draco Malfoy       | 1998-03-11 | 16:00:00   | 20:00:00 |
| Draco Malfoy       | 1998-03-12 | 16:00:00   | 20:00:00 |
| Draco Malfoy       | 1998-03-13 | 16:00:00   | 20:00:00 |
| Padma Patil        | 1998-03-09 | 12:00:00   | 20:00:00 |
| Padma Patil        | 1998-03-10 | 12:00:00   | 20:00:00 |
| Padma Patil        | 1998-03-11 | 12:00:00   | 20:00:00 |
| Padma Patil        | 1998-03-09 | 08:00:00   | 12:00:00 |
| Padma Patil        | 1998-03-10 | 08:00:00   | 12:00:00 |
| Padma Patil        | 1998-03-11 | 08:00:00   | 12:00:00 |
| Cho Chang          | 1998-03-12 | 12:00:00   | 20:00:00 |
| Cho Chang          | 1998-03-13 | 12:00:00   | 20:00:00 |
| Dean Thomas        | 1998-03-09 | 16:00:00   | 20:00:00 |
| Dean Thomas        | 1998-03-10 | 16:00:00   | 20:00:00 |
| Neville Longbottom |            |            |          |
| Cedric Diggory     |            |            |          |
|                    | 1998-03-13 | 08:00:00   | 12:00:00 |
|                    | 1998-03-12 | 08:00:00   | 12:00:00 |



> 8) Using [this Adoption schema and data](https://www.db-fiddle.com/f/tpodLv3A43VL4gHqohqx2o/0), please write queries to retrieve the following information and include the results:

> - Create a list of all volunteers. If the volunteer is fostering a dog, include each dog as well.

```SQL
SELECT v.first_name, v.last_name, d.name AS dog_name -- or SELECT *
  FROM volunteers AS v
  LEFT JOIN dogs AS d -- include volunteers w/o dogs
    ON v.foster_dog_id = d.id;
```

| first_name | last_name  | dog_name  |
| ---------- | ---------- | --------- |
| Rubeus     | Hagrid     | Munchkin  |
| Marjorie   | Dursley    | Marmaduke |
| Sirius     | Black      |           |
| Remus      | Lupin      |           |
| Albus      | Dumbledore |           |


> - The cat's name, adopter's name, and adopted date for each cat adopted within the past month to be displayed as part of the "Happy Tail" social media promotion which posts recent successful adoptions.

```SQL
SELECT c.name AS cat_name,
       a.first_name AS adopter_first, a.last_name AS adopter_last,
       ca.date
  FROM cats AS c
  JOIN cat_adoptions AS ca
    ON c.id = ca.cat_id
  LEFT JOIN adopters AS a -- include anonymously adopted cats?
    ON ca.adopter_id = a.id
  WHERE ca.date >= ( CURRENT_DATE - INTERVAL '30 DAYS' ) -- or use EXTRACT to precisely calculate "1 month ago"
;
```

| cat_name | adopter_first | adopter_last | date                     |
| -------- | ------------- | ------------ | ------------------------ |
| Mushi    | Arabella      | Figg         | 2018-09-27T00:00:00.000Z |
| Victoire | Argus         | Filch        | 2018-10-02T00:00:00.000Z |


> - Create a list of adopters who have not yet chosen a dog to adopt.

```SQL
SELECT *
  FROM adopters AS a
  LEFT JOIN dog_adoptions AS da -- include all adopters
    ON a.id = da.adopter_id
  WHERE da.dog_id IS NULL;
```

| id  | first_name | last_name | address             | phone_number | adopter_id | dog_id | date | fee |
| --- | ---------- | --------- | ------------------- | ------------ | ---------- | ------ | ---- | --- |
| 2   | Arabella   | Figg      | 4 Wisteria Walk     | 843-228-5239 |            |        |      |     |
| 1   | Hermione   | Granger   | 32 Granger's Street | 676-464-7837 |            |        |      |     |


> - Lists of all cats and all dogs who have not been adopted.

```SQL
SELECT 'cat' AS pet_type,
       c.name, c.gender, c.age, ca.date
  FROM cats AS c
  LEFT JOIN cat_adoptions AS ca -- include all cats
    ON c.id = ca.cat_id
  WHERE ca.date IS NULL
UNION
SELECT 'dog' AS pet_type,
       d.name, d.gender, d.age, da.date
  FROM dogs AS d
  LEFT JOIN dog_adoptions AS da -- include all dogs
    ON d.id = da.dog_id
  WHERE da.date IS NULL;
```

| pet_type | name      | gender | age | date |
| -------- | --------- | ------ | --- | ---- |
| dog      | Boujee    | F      | 3   |      |
| dog      | Marley    | M      | 0   |      |
| dog      | Marmaduke | M      | 7   |      |
| cat      | Seashell  | F      | 7   |      |
| dog      | Munchkin  | F      | 0   |      |
| cat      | Nala      | F      | 1   |      |
| dog      | Lassie    | F      | 7   |      |


> - The name of the person who adopted Rosco.

```SQL
SELECT a.first_name AS adopter_first, a.last_name AS adopter_last
       --, d.name AS dog_name, da.date
  FROM adopters AS a
  RIGHT JOIN dog_adoptions AS da -- include all adoptions
    ON a.id = da.adopter_id
  RIGHT JOIN dogs AS d -- include all dogs
    ON da.dog_id = d.id
  WHERE d.name = 'Rosco';

-- or UNION query dogs and cats, if I didn't know Rosco was a dog
```

| adopter_first | adopter_last |
| ------------- | ------------ |
| Argus         | Filch        |



> 9) Using [this Library schema and data](https://www.db-fiddle.com/f/j4EGoWzHWDBVtiYzB9ygC4/0), write queries applying the following scenarios and include the results:

> - To determine if the library should buy more copies of a given book, please provide the names and position, in order, of all of the patrons with a hold (request for a book with all copies checked out) on "Advanced Potion-Making".

```SQL
SELECT p.name, h.rank AS position
       --, b.title
  FROM patrons AS p
  RIGHT JOIN holds AS h -- include all holds
    ON p.id = h.patron_id
  RIGHT JOIN books AS b -- include all books
    ON h.isbn = b.isbn
  WHERE b.title = 'Advanced Potion-Making'
ORDER BY h.rank ASC;
```

| name           | position |
| -------------- | -------- |
| Terry Boot     | 1        |
| Cedric Diggory | 2        |


> - List all of the library patrons. If they have one or more books checked out, list the books with the patrons.

```SQL
SELECT p.name, tb.title AS book_title, tb.checked_out_date -- or SELECT *
  FROM patrons AS p
  LEFT JOIN ( -- include all patrons
    SELECT *
      FROM transactions AS t
      JOIN books AS b
        ON t.isbn = b.isbn
      WHERE t.checked_in_date IS NULL -- exclude books checked back in, disable for full checkout history
    ) AS tb
    ON p.id = tb.patron_id
ORDER BY p.id -- keep multiple records for each patron together
;
```

| name             | book_title                              | checked_out_date         |
| ---------------- | --------------------------------------- | ------------------------ |
| Hermione Granger |                                         |                          |
| Terry Boot       | Advanced Potion-Making                  | 2018-10-14T00:00:00.000Z |
| Padma Patil      |                                         |                          |
| Cho Chang        |                                         |                          |
| Cedric Diggory   | Fantastic Beasts and Where to Find Them | 2018-10-16T00:00:00.000Z |
