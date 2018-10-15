### Exercises

> Submit your answers to the following questions.

> NOTE: Real-world examples must be your own and not based on the text or previous assignments.


> 1) How do you find related data held in two separate data tables?




> 2) Explain, in your own words, the difference between an `INNER JOIN`, `LEFT OUTER JOIN`, and `RIGHT OUTER JOIN`. Give a real-world example for each.




> 3) Define primary key and foreign key. Give a real-world example for each.




> 4) Define aliasing.




> 5) Change this query so that you are using aliasing:
```SQL
SELECT professor.name, compensation.salary,
compensation.vacation_days FROM professor JOIN
compensation ON professor.id =
compensation.professor_id;
```



> 6) Why would you use a `NATURAL JOIN`? Give a real-world example.




> 7) Using [this Employee schema and data](https://www.db-fiddle.com/f/sG1TKgR15GhH8cjbAwzjAm/0), write queries to find the following information:

> - List all employees and all shifts.




> 8) Using [this Adoption schema and data](https://www.db-fiddle.com/f/tpodLv3A43VL4gHqohqx2o/0), please write queries to retrieve the following information and include the results:

> - Create a list of all volunteers. If the volunteer is fostering a dog, include each dog as well.



> - The cat's name, adopter's name, and adopted date for each cat adopted within the past month to be displayed as part of the "Happy Tail" social media promotion which posts recent successful adoptions.



> - Create a list of adopters who have not yet chosen a dog to adopt.



> - Lists of all cats and all dogs who have not been adopted.



> - The name of the person who adopted Rosco.




> 9) Using [this Library schema and data](https://www.db-fiddle.com/f/j4EGoWzHWDBVtiYzB9ygC4/0), write queries applying the following scenarios and include the results:

> - To determine if the library should buy more copies of a given book, please provide the names and position, in order, of all of the patrons with a hold (request for a book with all copies checked out) on "Advanced Potion-Making".



> - List all of the library patrons. If they have one or more books checked out, list the books with the patrons.
