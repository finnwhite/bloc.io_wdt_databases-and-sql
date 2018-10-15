### Exercises

> Answer the following questions and submit the responses.


> 1) Write out a generic `SELECT` statement.

```SQL
SELECT <columns> FROM <table> WHERE <conditions>;
```



> 2) Create a fun way to remember the order of operations in a `SELECT` statement, such as a _mnemonic_.

As a SQL developer, remembering (**`S`**)`ELECT` ... (**`F`**)`ROM` ... (**`W`**)`HERE` is definitely (**S**)afe (**F**)or (**W**)ork. However, confusing lexical order with [order of execution](https://www.periscopedata.com/blog/sql-query-order-of-operations) is probably NSFW!



> 3) Given this [`dogs`](https://www.db-fiddle.com/f/kvD6xZQ14vRbpPe5muA92L/0) table, write queries to select the following pieces of data:

> Intake teams typically guess the breed of shelter dogs, so the `breed` column may have multiple words (for example, "Labrador Collie mix").

> - Display the name, gender, and age of all dogs that are part Labrador.

```SQL
SELECT name, gender, age
FROM dogs
WHERE breed LIKE '%labrador%';
```

| name   | gender | age |
| ------ | ------ | --- |
| Boujee | F      | 3   |
| Marley | M      | 0   |


> - Display the ids of all dogs that are under 1 year old.

```SQL
SELECT id
FROM dogs
WHERE age < 1;
```

| id    |
| ----- |
| 10002 |
| 10004 |


> - Display the name and age of all dogs that are female and over 35lbs.

```SQL
SELECT name, age
FROM dogs
WHERE gender = 'F' AND weight > 35;
```

| name   | age |
| ------ | --- |
| Boujee | 3   |


> - Display all of the information about all dogs that are not Shepherd mixes.

```SQL
SELECT *
FROM dogs
WHERE breed NOT LIKE '%shepherd%';
```

| id    | name      | gender | age | weight | breed              | intake_date              | in_foster                |
| ----- | --------- | ------ | --- | ------ | ------------------ | ------------------------ | ------------------------ |
| 10001 | Boujee    | F      | 3   | 36     | labrador poodle    | 2017-06-22T00:00:00.000Z |                          |
| 10002 | Munchkin  | F      | 0   | 8      | dachsund chihuahua | 2017-01-13T00:00:00.000Z | 2017-01-31T00:00:00.000Z |
| 10004 | Marley    | M      | 0   | 10     | labrador           | 2017-05-04T00:00:00.000Z | 2016-06-20T00:00:00.000Z |
| 10006 | Marmaduke | M      | 7   | 150    | great dane         | 2016-03-22T00:00:00.000Z | 2016-05-15T00:00:00.000Z |
| 10007 | Rosco     | M      | 5   | 180    | rottweiler         | 2017-04-01T00:00:00.000Z |                          |


> - Display the id, age, weight, and breed of all dogs that are either over 60lbs or Great Danes.

```SQL
SELECT id, age, weight, breed
FROM dogs
WHERE weight > 60 OR breed LIKE '%great dane%';
```

| id    | age | weight | breed      |
| ----- | --- | ------ | ---------- |
| 10006 | 7   | 150    | great dane |
| 10007 | 5   | 180    | rottweiler |



> 4) Given this [`cats`](https://www.db-fiddle.com/f/55ePhx9NLn7PzdGnebFaG7/0) table, what records are returned from these queries?

> - `SELECT name, adoption_date FROM cats;`

| name     | adoption_date |
| -------- | ------------- |
| Mushi    | '2016-03-22'  |
| Seashell | NULL          |
| Azul     | '2016-04-17'  |
| Victoire | '2016-09-01'  |
| Nala     | NULL          |


> - `SELECT name, age FROM cats;`

| name     | age |
| -------- | --- |
| Mushi    | 1   |
| Seashell | 7   |
| Azul     | 3   |
| Victoire | 7   |
| Nala     | 1   |



> 5) From the `cats` table, write queries to select the following pieces of data.

> - Display all the information about all of the available cats.

```SQL
SELECT *
FROM cats
WHERE adoption_date IS NULL;
```

| id  | name     | gender | age | intake_date              | adoption_date |
| --- | -------- | ------ | --- | ------------------------ | ------------- |
| 2   | Seashell | F      | 7   | 2016-01-09T00:00:00.000Z |               |
| 5   | Nala     | F      | 1   | 2016-01-12T00:00:00.000Z |               |


> - Display the name and sex of all cats who are 7 years old.

```SQL
SELECT name, gender
FROM cats
WHERE age = 7;
```

| name     | gender |
| -------- | ------ |
| Seashell | F      |
| Victoire | M      |


> - Find all of the names of the cats, so you don’t choose duplicate names for new cats.

```SQL
SELECT name FROM cats;

-- over-engineering...
-- SELECT DISTINCT name FROM cats ORDER BY name;
```

| name     |
| -------- |
| Mushi    |
| Seashell |
| Azul     |
| Victoire |
| Nala     |



> 6) List each comparison operator and explain when you would use it. Include a real world example for each.

- `=` (equal to): use to select equal values; for example, purchases associated with my email address, `WHERE email = 'finnwhite@gmail.com'`
- `!=` (not equal to) -OR- `<>` (less than or greater than): use to exclude equal (or NULL) values, select unequal (non-NULL) values; for example, suitable morning coffees, `WHERE is_decaf != TRUE`
- `<` (less than): use to select values less than a value; for example, people eligible to stay on a parent's health insurance, `WHERE age < 26`
- `>` (greater than): use to select values greater than a value; for example, items currently in stock, `WHERE stock_count > 0`
- `<=` (less than or equal to): use to select values less than or equal to a value; for example, half-marathon finish times at or under 2 hours, `WHERE time_elapsed <= '02:00:00'`
- `>=` (greater than or equal to): use to select values greater than or equal to a value; for example, people tall enough to ride this roller coaster, `WHERE height >= 54`
- `LIKE` with `%` (match pattern, "contains"): use to select string values that contain a value, where `%` represents any zero or more leading or trailing characters; for example, apps built using the current major release of React, `WHERE version LIKE '16.%'`
- `IS [NOT] NULL` (nullity): use to select [exclude] NULL (empty) values.; for example, checkpoints I have submitted, `WHERE date_submitted IS NOT NULL`



> 7) From the `cats` table, what data is returned from these queries?

> - `SELECT name FROM cats WHERE gender = ‘F’;`

after fixing curly quotes...

| name     |
| -------- |
| Seashell |
| Nala     |


> - `SELECT name FROM cats WHERE age <> 3;`

| name     |
| -------- |
| Mushi    |
| Seashell |
| Victoire |
| Nala     |


> - `SELECT ID FROM cats WHERE name != ‘Mushi’ AND gender = ‘M’;`

after fixing curly quotes...

| id  |
| --- |
| 3   |
| 4   |
