### Exercises

> Answer the following questions and submit the responses.


> 1) Write out a generic `SELECT` statement.




> 2) Create a fun way to remember the order of operations in a `SELECT` statement, such as a _mnemonic_.




> 3) Given this [`dogs`](https://www.db-fiddle.com/f/kvD6xZQ14vRbpPe5muA92L/0) table, write queries to select the following pieces of data:

> Intake teams typically guess the breed of shelter dogs, so the `breed` column may have multiple words (for example, "Labrador Collie mix").

> - Display the name, gender, and age of all dogs that are part Labrador.



> - Display the ids of all dogs that are under 1 year old.



> - Display the name and age of all dogs that are female and over 35lbs.



> - Display all of the information about all dogs that are not Shepherd mixes.



> - Display the id, age, weight, and breed of all dogs that are either over 60lbs or Great Danes.




> 4) Given this [`cats`](https://www.db-fiddle.com/f/55ePhx9NLn7PzdGnebFaG7/0) table, what records are returned from these queries?

> - `SELECT name, adoption_date FROM cats;`



> - `SELECT name, age FROM cats;`




> 5) From the `cats` table, write queries to select the following pieces of data.

> - Display all the information about all of the available cats.



> - Display the name and sex of all cats who are 7 years old.



> - Find all of the names of the cats, so you don’t choose duplicate names for new cats.




> 6) List each comparison operator and explain when you would use it. Include a real world example for each.

> If you can’t list these from memory, do these flashcards until you can!




> 7) From the `cats` table, what data is returned from these queries?

> - `SELECT name FROM cats WHERE gender = ‘F’;`



> - `SELECT name FROM cats WHERE age <> 3;`



> - `SELECT ID FROM cats WHERE name != ‘Mushi’ AND gender = ‘M’;`
