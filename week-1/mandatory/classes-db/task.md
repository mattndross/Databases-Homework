# Class Database

## Submission

Below you will find a set of tasks for you to complete to set up a databases of students and mentors.

To submit this homework write the correct commands for each question here:

```sql
--Create a new database called cyf_classes (hint: use createdb in the terminal)
create database cyf_classes

--Create a new table mentors, for each mentor we want to save their name, how many years they lived in Glasgow,
-- their address and their favourite programming language.
create table mentors (
id SERIAL primary key,
name VARCHAR(30) not null,
years_in_glasgow int4,
address VARCHAR(120),
favourite_language VARCHAR(20) );

--Insert 5 mentors in the mentors table (you can make up the data, it doesn't need to be accurate ;-)).
insert into mentors (name, years_in_glasgow, address, favourite_language) values ('JORGE', 2, 'Carrer del sol, 24', 'python');
insert into mentors (name, years_in_glasgow, address, favourite_language) values ('GERMAN', 2, 'Carrer de Valencia, 240', 'javascript');
insert into mentors (name, years_in_glasgow, address, favourite_language) values ('JESSICA', 1, 'Carrer de La Lucía', 'c#');
insert into mentors (name, years_in_glasgow, address, favourite_language) values ('DANIEL', 4, 'Carrer de Aragó, 120', 'python');
insert into mentors (name, years_in_glasgow, address, favourite_language) values ('GERANIO', 3, 'Carrer de selva de mar, 98', 'javascript');

--Create a new table students, for each student we want to save their name, 
--address and if they have graduated from Code Your Future.
create table students (
id SERIAL primary key,
name VARCHAR(30) not null,
graduated boolean,
address VARCHAR(120) );

--Insert 10 students in the students table.
insert into students (name, address, graduated) values ('BERENICE', 'carrer de verdi, 54', true);
insert into students (name, address, graduated) values ('GUILLEM', 'carrer de lencarnació, 58', false);
insert into students (name, address, graduated) values ('PATRICIO', 'carrer de navas de tolosa, 112', false);
insert into students (name, address, graduated) values ('CARLOS', 'carrer de torrent de la olla, 200', true);
insert into students (name, address, graduated) values ('JESSICA', 'carrer de verdi, 40', true);
insert into students (name, address, graduated) values ('TAMARA', 'carrer de verdi, 90', FALSE);
insert into students (name, address, graduated) values ('ORIOL', 'carrer de verdi, 10', trUe);
insert into students (name, address, graduated) values ('ESTEBAN', 'carrer de verdi, 39', FALSE);
insert into students (name, address, graduated) values ('CAMILE', 'carrer de verdi, 23', true);

--Verify that the data you created for mentors and students are correctly stored in their respective tables 
--(hint: use a select SQL statement).
select * from mentors;
select * from students;

--Create a new classes table to record the following information:
--  A class has a leading mentor
--  A class has a topic (such as Javascript, NodeJS)
--  A class is taught at a specific date and at a specific location
create table classes (
id SERIAL primary key,
mentor int references mentors(id),
topic VARCHAR(20),
date DATE not null,
location VARCHAR(20)
);

--Insert a few classes in the classes table
insert into classes (mentor, topic, date, location) values (2, 'javascript', '2021-10-2', 'Barcelona');
insert into classes (mentor, topic, date, location) values (3, 'javascript', '2021-11-3', 'Barcelona');
insert into classes (mentor, topic, date, location) values (1, 'javascript', '2021-8-2', 'Barcelona');
insert into classes (mentor, topic, date, location) values (2, 'javascript', '2021-9-5', 'Barcelona');

--We now want to store who among the students attends a specific class. How would you store that?
-- Come up with a solution and insert some data if you model this as a new table.
alter table students add class_id int references classes(id);

--Answer the following questions using a select SQL statement:
--Retrieve all the mentors who lived more than 5 years in Glasgow
SELECT * FROM mentors where years_in_glasgow > 3;

--Retrieve all the mentors whose favourite language is Javascript
SELECT * FROM mentors where favourite_language = 'javascript';

--Retrieve all the students who are CYF graduates
SELECT * FROM students where graduated = true;

--Retrieve all the classes taught before June this year
select * from classes where "date" < '2021-06-01';

--Retrieve all the students (retrieving student ids only is fine)
-- who attended the Javascript class (or any other class that you have in the classes table).
select * from students s 
join classes c on s.class_id = c.id 
where c.topic = 'javascript';

```

When you have finished all of the questions - open a pull request with your answers to the `Databases-Homework` repository.

## Task

1. Create a new database called `cyf_classes` (hint: use `createdb` in the terminal)
2. Create a new table `mentors`, for each mentor we want to save their name, how many years they lived in Glasgow, their address and their favourite programming language.
3. Insert 5 mentors in the `mentors` table (you can make up the data, it doesn't need to be accurate ;-)).
4. Create a new table `students`, for each student we want to save their name, address and if they have graduated from Code Your Future.
5. Insert 10 students in the `students` table.
6. Verify that the data you created for mentors and students are correctly stored in their respective tables (hint: use a `select` SQL statement).
7. Create a new `classes` table to record the following information:

   - A class has a leading mentor
   - A class has a topic (such as Javascript, NodeJS)
   - A class is taught at a specific date and at a specific location

8. Insert a few classes in the `classes` table
9. We now want to store who among the students attends a specific class. How would you store that? Come up with a solution and insert some data if you model this as a new table.
10. Answer the following questions using a `select` SQL statement:
    - Retrieve all the mentors who lived more than 5 years in Glasgow
    - Retrieve all the mentors whose favourite language is Javascript
    - Retrieve all the students who are CYF graduates
    - Retrieve all the classes taught before June this year
    - Retrieve all the students (retrieving student ids only is fine) who attended the Javascript class (or any other class that you have in the `classes` table).
