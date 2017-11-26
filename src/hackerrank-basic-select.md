# Revising the Select Query I  
  
Query all columns for all American cities in CITY with populations larger than 100000. The CountryCode for America is USA.  
  
***Input Format***  
  
The CITY table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)  
  
	SELECT * FROM city WHERE population > 100000 AND countrycode = 'USA';  
  
  
  
# Revising the Select Query II  
  
Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA.  
  
	SELECT name FROM city WHERE countrycode = 'USA' AND population > 120000;  
  
  
  
# Select All  
  
Query all columns (attributes) for every row in the CITY table.  
  
	SELECT * FROM city;  
  
  
  
# Select By ID  
  
Query all columns for a city in CITY with the ID 1661.  
  
	SELECT * FROM city WHERE id = '1661';  
  
  
  
# Japanese Cities' Attributes  
  
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.  
  
	SELECT * FROM city WHERE countrycode = 'JPN';  
  
   
   
# Japanese Cities' Names  
  
Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.  
  
	SELECT name FROM city WHERE countrycode = 'JPN';  
  
  
  
# Weather Observation Station 1  
  
Query a list of CITY and STATE from the STATION table.  
  
***Input Format***  
  
The STATION table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)  
  
where LAT_N is the northern latitude and LONG_W is the western longitude.  
  
	SELECT city, state FROM station;  
  
  
  
# Weather Observation Station 3  
  
Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer.  
  
	SELECT DISTINCT city FROM station WHERE MOD(id, 2) = 0;  
  
  
  
# Weather Observation Station 4  
  
Let N be the number of CITY entries in STATION, and let N' be the number of distinct CITY names in STATION; query the value N-N' of from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.  
  
	SELECT COUNT(city) - COUNT(DISTINCT(city)) FROM station;   
  
  
  
# Weather Observation Station 5  
  
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.  
  
***Sample Input***  
  
Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY  
  
***Sample Output***   
  
ABC 3  
PQRS 4  
  
***Explanation***  
  
When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with the respective lengths 3, 3, 4 and 3. The longest-named city is obviously PQRS, but there are 3 options for shortest-named city; we choose ABC, because it comes first alphabetically.  
  
	SELECT * FROM (SELECT DISTINCT city, LENGTH(city) FROM station ORDER BY LENGTH(city) ASC, city ASC) WHERE ROWNUM = 1   
	UNION  
	SELECT * FROM (SELECT DISTINCT city, LENGTH(city) FROM station ORDER BY LENGTH(city) DESC, city ASC) WHERE ROWNUM = 1;  
  
  
  
# Weather Observation Station 6  
  
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.  
  
	SELECT DISTINCT city FROM station WHERE city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%';   
  
  
  
# Weather Observation Station 7  
  
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
  
	SELECT DISTINCT city FROM station WHERE city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u';  
  
  
  
# Weather Observation Station 8  
  
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.  
  
	SELECT DISTINCT city FROM 
	(SELECT DISTINCT city FROM station WHERE city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%') 
	WHERE city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u';
  
  
  
# Weather Observation Station 9  
  
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.  
  
	SELECT DISTINCT city FROM station WHERE NOT (city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%');   
  
  
  
# Weather Observation Station 10  
  
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.
  
	SELECT DISTINCT city FROM station WHERE NOT (city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u');  
  
  
  
# Weather Observation Station 11  
  
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.  
  
	SELECT DISTINCT city FROM station WHERE 
	(NOT (city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%') 
	OR NOT(city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u'));   
  
  
  
# Weather Observation Station 12  
  
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.  
  
	SELECT DISTINCT city FROM station WHERE NOT 
	((city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%')  
	OR (city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u'));
  
  
  
# Higher Than 75 Marks  
  
Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.  
  
***Input Format*** 
  
The STUDENTS table is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/12896/1443815243-94b941f556-1.png)  
  
The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.  
  
***Sample Input***  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12896/1443815209-cf4b260993-2.png)  
  
***Sample Output***  
  
Ashley  
Julia  
Belvet  
  
***Explanation***  
  
Only Ashley, Julia, and Belvet have Marks > 75. If you look at the last three characters of each of their names, there are no duplicates and 'ley' < 'lia' < 'vet'.   
  
	SELECT name FROM students WHERE marks > 75 ORDER BY SUBSTR(name, LENGTH(name)-2, 3), id;
  
  
  
# Employee Names  
  
Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.  
  
***Input Format***  
  
The Employee table containing employee data for a company is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)  
  
where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is their monthly salary.  
  
***Sample Input***  
   
![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)  
  
***Sample Output***  
  
Angela  
Bonnie  
Frank  
Joe  
Kimberly  
Lisa  
Michael  
Patrick  
Rose  
Todd  
  
	SELECT name FROM employee ORDER BY name;
  
  
  
# Employee Salaries  
  
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.  
  
	SELECT name FROM employee WHERE salary > 2000 AND months < 10 ORDER BY employee_id;