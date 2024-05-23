# SQL
Have a look on my SQL Queries.


CREATE DATABASE SQL1 ;


-- Create the course table

CREATE TABLE course(
course_id INT PRIMARY KEY,
course_name VARCHAR(20) NOT NULL,
instructor_name VARCHAR(20) NOT NULL,
duration_weeks INT NOT NULL,
credits INT NOT NULL) ;

INSERT INTO course()
VALUES
(1, "Mathematics", "Dr. Smith", 12, 4),
(2, "Physics", "Dr. Johnson", 10, 3),
(3, "Chemistry", "Dr. Lee", 8, 4),
(4, "Biology", "Dr. Kim", 10, 3),
(5, "English Literature", "Dr. Brown", 14, 4),
(6, "History", "Dr. Green", 12, 3),
(7, "Computer Science", "Dr. White", 16, 5),
(8, "Art", "Dr. Black", 8, 2),
(9, "Music", "Dr. Grey", 10, 2),
(10, "Philosophy", "Dr. Rose", 12, 4),
(11, "Psychology", "Dr. Blue", 10, 3),
(12, "Economics", "Dr. Orange", 12, 4),
(13, "Political Science", "Dr. Purple", 14, 4),
(14, "Sociology", "Dr. Pink", 10, 3),
(15, "Anthropology", "Dr. Yellow", 12, 4) ;


-- Create the student table

CREATE TABLE student (
student_id INT PRIMARY KEY,
student_name VARCHAR(20) NOT NULL,
age INT NOT NULL,
course VARCHAR(20) NOT NULL,
course_id INT NOT NULL,
FOREIGN KEY (course_id) REFERENCES course(course_id)) ;

INSERT INTO student() 
VALUES
(1, "Alice", 20, "Computer Science", 7),
(2, "Bob", 21, "Mathematics", 1),
(3, "Charlie", 19, "Physics", 2),
(4, "David", 22, "Chemistry", 3),
(5, "Eva", 20, "Biology", 4),
(6, "Frank", 21, "English Literature", 5),
(7, "Grace", 19, "History", 6),
(8, "Hannah", 20, "Art", 8),
(9, "Ivy", 21, "Music", 9),
(10, "Jack", 22, "Philosophy", 10),
(11, "Karen", 20, "Psychology", 11),
(12, "Leo", 21, "Economics", 12),
(13, "Mia", 19, "Political Science", 13),
(14, "Noah", 20, "Sociology", 14),
(15, "Olivia", 21, "Anthropology", 15) ;


SELECT * FROM courses ;
SELECT * FROM student ; -- to see the values/records of the table.


DESC student ; -- to see the structure of the table. (Values orRecords will not be seen.)

RENAME TABLE course TO courses ; -- to rename the table.

ALTER TABLE student
CHANGE course courses VARCHAR(20) ; -- to change the name of the column.

ALTER TABLE student 
MODIFY student_id VARCHAR(40) ; -- to change the data type.

ALTER TABLE student 
ADD percentage FLOAT ; -- to add the column.

ALTER TABLE student 
ADD percentage FLOAT FIRST ; -- to add the column at 1st position.

ALTER TABLE student 
DROP percentage ; -- to delete the column.

UPDATE courses
SET duration_weeks = 8
WHERE course_id = 9 ; -- to change the values in column.

SELECT * FROM courses
WHERE duration_weeks > 10 ;

SELECT DISTINCT(credits) FROM courses ; -- Distinct is use to display unique values.

SELECT * FROM courses
WHERE duration_weeks = 8 OR duration_weeks = 14 OR duration_weeks = 10 ;




CREATE TABLE t1(product VARCHAR(20), cp INT, sp INT, CONSTRAINT prod CHECK(cp > 100 AND sp < 500));

ALTER TABLE t1
ADD CONSTRAINT prod1 CHECK(cp > 40 AND sp < 100);


-- Foreign Key..........................................................................................................


--  used to create relationship between tables
--  Foreign Key refers to Primary key of base table



/*  Base Table (Referenced table)                                                  Referencing Table

    id        name1         address                                               id         c_name          c_id
    (PK)                                                                          (FK)
    
    1          a              x                                                    1          SQL             c1
    2          b              y                                                    2          Python          c2
    3          c              z                        
    
    
    
    INSERT -  Possible.                                                     INSERT- Possible for values which are present in Base Table(PK).
    
    UPDATE -  Not possible for PK.                                          UPDATE - Not possible for FK,  Possible for other columns.
    
    DELETE - Not possible for values which are prsent                       DELETE - Possible.
	          in Referencing Table.           

*/




CREATE TABLE adm(id INT PRIMARY KEY, NAME1 VARCHAR(20), address VARCHAR(40));

CREATE TABLE course1(id INT, c_name VARCHAR(20), c_id VARCHAR(20), FOREIGN KEY(id) REFERENCES adm(id));


INSERT INTO adm()
VALUES(1, "a", "x"), (2, "b", "y"), (3, "c", "z"), (4, "c", "m");

INSERT INTO course1()
VALUES(1, "SQL", "c1"), (2, "Python", "c2");


SELECT * FROM adm;

SELECT * FROM course1;


-- Operations on Base Table......................................................

-- 1)  INSERT.............................


INSERT INTO adm()
VALUES(5, "e", "n"); -- Possible.



-- 2)  UPDATE..............................


UPDATE adm
SET id = 10
WHERE NAME1 = "a"; -- Not Possible.


UPDATE adm
SET NAME1 = "w"
WHERE id = 3;  -- Possible.




-- 3)  DELETE....................


DELETE FROM adm
WHERE id = 1;  -- Not Possible.


DELETE FROM adm
WHERE id = 5;  -- Possible.




-- Operations on Referencing Table......................................



-- 1)  INSERT...................


INSERT INTO course1()
VALUES(3 , "ML", "c3"); -- Possible.


INSERT INTO course1()
VALUES()




-- 2)  UPDATE.......................

UPDATE course1
SET id = 20
WHERE c_name = "Python"; -- Not Possible.


UPDATE course1
SET c_name = "DL"
WHERE id = 3; -- Possible.



-- 3)  DELETE.......................


DELETE FROM course1
WHERE c_id = "c2";


TRUNCATE TABLE adm; -- to delete the records of the table, table structure will not get deleted.



SELECT * FROM courses WHERE duration_weeks IN (8, 10); 

SELECT * FROM courses WHERE duration_weeks NOT IN (10, 12);

SELECT * FROM courses WHERE course_name LIKE 'p%' ; 

SELECT * FROM courses WHERE course_name LIKE '%y' ;

SELECT * FROM courses WHERE course_name LIKE '__t%' ;


SELECT * FROM courses 
ORDER BY course_id ;

SELECT * FROM courses 
ORDER BY credits DESC  LIMIT 2 ;

SELECT * FROM courses 
ORDER BY credits DESC LIMIT 1,1 ; -- to see 2nd highest credit.



-- Length..........................................................................................................

SELECT LENGTH("Database MS"); -- length of the string.

SELECT CHAR_LENGTH("DATABASE MS");

SELECT UPPER("database"); -- chage case of the string.



-- Replace............................................................................................................


SELECT REPLACE ("R Database Management System", "R", "Relational");



-- Concat...............................................................................................................


SELECT CONCAT ("Good", "Morning");

SELECT CONCAT ("Good", " ", "Morning");




SELECT DAYNAME('15-08-1947') AS Independence ; -- Output is NULL.

SELECT DAYNAME('1947-08-15') AS Independence ; -- Accepted.... date should be mentioned in International format.


SELECT SUBSTRING("MYSQL", 3, 2); -- SUBSTRING function extracts a substring from a string.

SELECT MONTHNAME('1997-12-24') AS MY_Birth_mnt ; -- MONTHNAME  function display the name of month from given date.




-- CASE..........................................................................................................................


SELECT DISTINCT(credits),
case
when credits = 5 then 'A'
when credits = 4 then 'B'
when credits = 3 then 'C'
ELSE 'D'
END AS C_Grades
FROM courses
ORDER BY credits DESC ;



-- String Functions......................................................................................................



SELECT LENGTH("Admin"); -- display length of string

SELECT UPPER("tejas") AS U_NAME ; -- UPPER  function display the string in capital letter.

SELECT LOWER("TEJAS") AS L_NAME ; -- LOWER  function display the string in Small letter.

SELECT LEFT("Admin", 3); -- display 3 letters from left.

SELECT RIGHT("Admin", 3); -- display 3 letters from right.

SELECT MID("Admin", 3, 2); -- display 2 middle letters, starting from 3rd letter.

SELECT LTRIM(" Admin"); -- removes left unwanted space.

SELECT RTRIM("Admin  "); -- removes right unwanted space.

SELECT TRIM(" Admin   "); -- removes unwanted space.

SELECT SUBSTRING("Hello Everyone", 3, 4);

SELECT SUBSTRING_INDEX("abc.xyz@gmail.com", ".", 1); -- display all the strings before 1st "." 

SELECT SUBSTRING_INDEX("abc.xyz@gmail.com", ".", 2); -- display all the strings before 2nd "." 

SELECT SUBSTRING_INDEX("abc.xyz@gmail.com", "@", 1);

SELECT SUBSTRING_INDEX("abc.xyz@gmail.com", ".", -2); -- display all the strings after 2nd "." 



-- Date Function...............................................................................................................


SELECT ADDDATE('2014-01-02', INTERVAL 10 DAY); -- Display date of after 10 days.

SELECT ADDDATE('2014-01-02', INTERVAL -2 WEEK); -- Display date of before 2 weeks.

SELECT ADDDATE('2014-01-02 10:30:45', INTERVAL 15 MINUTE); -- Display time of after 15 Minute.


SELECT ADDDATE('2015-01-03 12:05:10', INTERVAL -2 MONTH);

SELECT ADDDATE('2015-01-03 12:05:10', INTERVAL -3 YEAR);

SELECT ADDDATE('2015-01-03 12:05:10', INTERVAL 2 HOUR);

SELECT ADDDATE('2015-01-03 12:05:10', INTERVAL -3 MONTH);

SELECT NOW() ;

SELECT CURRENT_DATE() ;

SELECT CURRENT_TIME() ;

SELECT DATE_FORMAT('2000-01-04', '%Y') ; -- Display year of the date.

SELECT DATE_FORMAT('2000-01-04', '%y') ; -- Display last 2 digits of year.

SELECT DATE_FORMAT('2000-01-04', '%M') ; -- Display month name of the date.

SELECT DATE_FORMAT('2000-01-04', '%m') ; -- Display month number of the date.




-- SubQueries............................................................................................................


SELECT * FROM courses
WHERE credits = (SELECT MAX(credits) FROM courses) ;

SELECT DISTINCT(credits) FROM courses
WHERE credits = (SELECT DISTINCT(credits) FROM courses ORDER BY credits DESC LIMIT 1,1) ; -- 2nd highest credit.


SELECT MIN(credits) FROM courses
WHERE credits > (SELECT MIN(credits) FROM courses) ; -- 2nd lowest credit.





-- Joins....................................................................................................................



SELECT * FROM courses
UNION
SELECT * FROM student ;

SELECT * FROM courses
UNION ALL 
SELECT * FROM student ;


SELECT * FROM courses
CROSS JOIN student ;


SELECT * FROM courses
INNER JOIN student ;


SELECT * FROM courses
LEFT JOIN student
ON courses.course_id = student.course_id ;

SELECT * FROM courses
RIGHT JOIN student
ON courses.course_id = student.course_id ;


SELECT * FROM courses
LEFT JOIN student
ON courses.course_id = student.course_id
UNION
SELECT * FROM courses
RIGHT JOIN student
ON courses.course_id = student.course_id ; -- Outer Join.
