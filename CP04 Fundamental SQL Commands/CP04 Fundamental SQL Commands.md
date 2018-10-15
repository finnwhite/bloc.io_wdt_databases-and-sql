### Exercises

> Use the commands above to complete the following tasks, and submit the SQL statements. Real-world examples must be distinct from those used in the text.


> 1) List the commands for adding, updating, and deleting data.

- **adding:** use the `INSERT INTO` statement
- **updating:** use the `UPDATE` statement
- **deleting:** use the `DELETE FROM` statement


> 2) Explain the structure for each type of command.

- **adding:** An `INSERT` statement specifies the table where the new data should be added, followed by a list of columns where the individual values should be stored. The `VALUES` clause enumerates one or more rows to be added, as a list of values in sequence corresponding to the list of columns.

```SQL
INSERT INTO <table> (<column1>, <column2>, ... <columnN>)
  VALUES
  (<row1_value1>, <row1_value2>, ... <row1_valueN>),
  ...
  (<rowN_value1>, <rowN_value2>, ... <rowN_valueN>);
```

- **updating:** An `UPDATE` statement specifies the table where the data to be modified is stored. The `SET` clause lists one or more column-value pairs containing the new data values, and the `WHERE` clause specifies the criteria for matching the row(s) that should be updated.

```SQL
UPDATE <table>
  SET <column1> = <value1>, ... <columnN> = <valueN>
  WHERE <predicates>;
```

- **deleting:** A `DELETE` statement specifies the table where the data to be removed is located. The `WHERE` clause specifies the criteria for matching the row(s) that should be deleted.

```SQL
DELETE FROM <table>
  WHERE <predicates>;
```


> 3) What are some of the data types that can be used in tables? Give a real-world example of each type.

Some common data types include:
- `character` or `char`: specifies a fixed-length character string. Examples include 2-letter abbreviations for US states, or product serial numbers.
- `timestamp`: represents a specific date _and_ time. Examples include a user's last login attempt, or date and time of birth (for hospital records or an astrology application?).
- `integer` or `int`: specifies a signed 4-byte (32-bit) integer, whole numbers between -2,147,483,648 to 2,147,483,647. Use cases include the population of a city or country, or vehicle or iPhone units sold.
- `smallint`: specifies a signed 2-byte (16-bit) integer, whole numbers between -32,768 to 32,767. Use cases include the number of pages in a book, or the square footage of a home.



> 4) Decide how to create a new table to hold a list of people invited to a wedding dinner. The table needs to have first and last names, whether they sent in their RSVP, the number of guests they are bringing, and the number of meals (1 for adults and 1/2 for children).

> - Which data type would you use to store each of the following pieces of information?

  - First and last name. - `text` (or `character varying` or `varchar` if space was a concern, and as long as [these persons](http://www.historyrundown.com/top-5-people-with-the-longest-names/) aren't invited... :wink:)
  - Whether they sent in their RSVP. - `boolean`
  - Number of guests. - `smallint`
  - Number of meals. - `numeric(3,1)` or `decimal(3,1)` (enough space for 10.5 meals for a very large family?)


> - Write a command that creates the table to track the wedding dinner.

```SQL
CREATE TABLE wedding_guests (
  name_first CHARACTER VARYING(72),
  name_last CHARACTER VARYING(72),
  has_rsvpd BOOLEAN,
  guest_count SMALLINT,
  meal_count NUMERIC(3,1)
);
```


> - Write a command that adds a column to track whether the guest sent a thank you card.

```SQL
ALTER TABLE wedding_guests
  ADD COLUMN sent_thankyou BOOLEAN;
```


> - You have decided to move the data about the meals to another table, so write a command to remove the column storing the number meals from the wedding table.

```SQL
ALTER TABLE wedding_guests
  DROP COLUMN meal_count;
```


> - The guests will need a place to sit at the reception, so write a command that adds a column for table number.

```SQL
ALTER TABLE wedding_guests
  ADD COLUMN table_number SMALLINT;
```


> - The wedding is over and we do not need to keep this information, so write a command that deletes the table numbers from the database.

```SQL
ALTER TABLE wedding_guests
  DROP COLUMN table_number;
```

...or delete the entire table?

```SQL
DROP TABLE wedding_guests;
```


TESTING LOG: [assignment-e04-log.txt](https://github.com/finnwhite/bloc.io_wdt_databases-and-sql/blob/cp04-sql-commands/CP04%20Fundamental%20SQL%20Commands/assignment-e04-log.txt)



> 5) Write a command to create a new table to hold the books in a library with the columns ISBN, title, author, genre, publishing date, number of copies, and available copies.

```SQL
CREATE TABLE books (
  isbn CHARACTER(17), --ISBN-10 or ISBN-13
  title TEXT,
  author TEXT,
  genre TEXT,
  date_published DATE,
  copies_total SMALLINT,
  copies_available SMALLINT
);
```


> - Find three books and add their information to the table.

```SQL
INSERT INTO books
    (isbn, title, author, genre, date_published, copies_total, copies_available)
  VALUES
    ('978-1-4019-5309-6', 'Becoming supernatural : how common people are doing the uncommon', 'Dispenza, Joe', 'LCSH: Energy medicine. | Mind and body. Self-care, Health.', '2017-10-31', 3, 2),
    ('978-1-59184-644-4', 'Start with why : how great leaders inspire everyone to take action', 'Sinek, Simon', 'Leadership', '2011-12-27', 7, 4),
    ('978-0-06-240780-1', 'Never split the difference : negotiating as if your life depended on it', 'Voss, Chris', 'Business Management & Leadership', '2016-05-17', 1, 1);
```


> - Someone has just checked out one of the books. Change the number of available copies to 1 fewer.

```SQL
UPDATE books
  SET copies_available = 0
  WHERE isbn = '978-0-06-240780-1'; --Never split the difference
```


> - Now one of the books has been added to the banned books list. Remove it from the table.

```SQL
DELETE FROM books
  WHERE isbn = '978-1-4019-5309-6'; --Becoming supernatural
```


TESTING LOG: [assignment-e05-log.txt](https://github.com/finnwhite/bloc.io_wdt_databases-and-sql/blob/cp04-sql-commands/CP04%20Fundamental%20SQL%20Commands/assignment-e05-log.txt)



> 6) Write a command to make a new table to hold spacecrafts. Information should include id, name, year launched, country of origin, a brief description of the mission, orbiting body, if it is currently operating, and its approximate miles from Earth.

```SQL
CREATE TABLE spacecrafts (
  id CHARACTER VARYING(11), --COSPAR designation
  name TEXT,
  launch_year SMALLINT,
  origin CHARACTER(3), --ISO 3166-1 alpha-3
  mission TEXT,
  orbiting TEXT,
  is_operating BOOLEAN,
  distance INTEGER
);
```


> In addition to the table creation, provide commands that perform the following operations:

> - Add three non-Earth-orbiting satellites to the table.

```SQL
INSERT INTO spacecrafts
    (id, name, launch_year, origin,
      mission,
      orbiting, is_operating, distance)
  VALUES
    ('2010-020D', 'Akatsuki', 2010, 'JPN',
      'Planned observations include cloud and surface imaging from an orbit around the planet with cameras operating in the infrared, visible and UV wavelengths to investigate the complex Venusian meteorology.',
      'Venus', TRUE, 25749622),
    ('2013-060A', 'Mangalyaan', 2013, 'IND',
      'The primary objective of the mission is to develop the technologies required for designing, planning, management and operations of an interplanetary mission.',
      'Mars', TRUE, 48709288),
    ('2011-040A', 'Juno', 2011, 'USA',
      'Juno''s mission is to measure Jupiter''s composition, gravity field, magnetic field, and polar magnetosphere.',
      'Jupiter', TRUE, 390693351);
```


> - Remove one of the satellites from the table since it has just crashed into the planet.

```SQL
DELETE FROM spacecrafts
  WHERE id = '2010-020D'; --Akatsuki
```


> - Edit another satellite because it is no longer operating and change the value to reflect that.

```SQL
UPDATE spacecrafts
  SET is_operating = FALSE
  WHERE id = '2013-060A'; --Mangalyaan
```


TESTING LOG: [assignment-e06-log.txt](https://github.com/finnwhite/bloc.io_wdt_databases-and-sql/blob/cp04-sql-commands/CP04%20Fundamental%20SQL%20Commands/assignment-e06-log.txt)



> 7) Write a command to create a new table to hold the emails in your inbox. This table should include an id, the subject line, the sender, any additional recipients, the body of the email, the timestamp, whether or not you have read the email, and the id of the email chain it's in.

```SQL
CREATE TABLE inbox (
  id INTEGER,
  sender TEXT,
  recipients TEXT,
  subject TEXT,
  body TEXT,
  sent_at TIMESTAMP,
  is_read BOOLEAN,
  chain_id INTEGER
);
```


> Also provide commands that perform the following operations:

> - Add three new emails to the inbox.

```SQL
INSERT INTO inbox
    (id, sender, recipients,
      subject,
      body,
      sent_at, is_read, chain_id)
  VALUES
    (101, 'buddy@supergym.net', 'finn@supergym.net; wifey@supergym.net; coach@supergym.net',
      'Baby & Me fitness class',
      'Are we on for class tomorrow?',
      '2018-10-13 09:42:00 -7:00', TRUE, 11),
    (102, 'coach@supergym.net', 'finn@supergym.net; wifey@supergym.net; buddy@supergym.net',
      'Baby & Me fitness class',
      'Absolutely!',
      '2018-10-13 09:44:00 -7:00', FALSE, 11),
    (576, 'success@bloc.io', 'finnwhite@gmail.com',
      'New mentor',
      'Hi Finn, thanks for writing in!\n\nI have just gone in and reset your mentor pairing so that the next time you log in you will be prompted to choose a new mentor.',
      '2018-09-05 10:39:00 -7:00', TRUE, 42);
```


> - You deleted one of the emails, so write a command to remove the row from the inbox table.

```SQL
DELETE FROM inbox
  WHERE id = 102;
```


> - You started reading an email but just heard a crash in another room. Mark the email as unread before investigating the crash, so you can come back and read it later.

```SQL
UPDATE inbox
  SET is_read = FALSE
  WHERE id = 576;
```


TESTING LOG: [assignment-e07-log.txt](https://github.com/finnwhite/bloc.io_wdt_databases-and-sql/blob/cp04-sql-commands/CP04%20Fundamental%20SQL%20Commands/assignment-e07-log.txt)
