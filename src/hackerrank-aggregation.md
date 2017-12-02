# Revising Aggregations - The Count Function  
  
Query a count of the number of cities in CITY having a Population larger than 100 000. 
  
***Input Format***  
The CITY table is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)  
  
	SELECT COUNT(*) FROM city WHERE population > 100000;  
  
  
  
# Revising Aggregations - The Sum Function  
  
Query the total population of all cities in CITY where District is California.   
  
	SELECT SUM(population) FROM city WHERE district = 'California';
  
  
  
# Revising Aggregations - Averages  
  
Query the average population of all cities in CITY where District is California.   
  
	SELECT AVG(population) FROM city WHERE district = 'California';
  
  
  
# Average Population  
  
Query the average population for all cities in CITY, rounded down to the nearest integer.  
  
	SELECT ROUND(AVG(population)) FROM city;
  
  
  
# Japan Population  
  
Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.  
  
	SELECT SUM(population) FROM city WHERE countrycode = 'JPN';
  
  
  
# Population Density Difference  
  
Query the difference between the maximum and minimum populations in CITY.  
  
	SELECT (MAX(population) - MIN(population)) FROM city;
  
  
  
# The Blunder  
  
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.  
Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries), and round it up to the next integer.  
  
***Input Format***  
The EMPLOYEES table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12893/1443817108-adc2235c81-1.png)  
  
***Note:*** Salary is measured in dollars per month and its value is < 10^5.  
  
	SELECT CEIL(AVG(salary) - AVG(REPLACE(salary, '0', ''))) FROM employees;
  
  
  
# Top Earners  
  
We define an employee's total earnings to be their monthly salary*months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2-space-separated integers.  
  
***Input Format***  
The Employee table containing employee data for a company is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)  
  
where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.  
  
	SELECT * FROM (SELECT  months*salary, COUNT(*) FROM employee GROUP BY months*salary ORDER BY months*salary DESC) WHERE ROWNUM = 1;
  
  
  
# Weather Observation Station 2  
  
Query the following two values from the STATION table:  
The sum of all values in LAT_N rounded to a scale of 2 decimal places.  
The sum of all values in LONG_W rounded to a scale of 2 decimal places.  
  
***Input Format***  
The STATION table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)  
  
where LAT_N is the northern latitude and LONG_W is the western longitude.  
  
	SELECT (ROUND(SUM(lat_n), 2) || ' ' || ROUND(SUM(long_w), 2)) FROM station;
  
  
  
# Weather Observation Station 13
  
Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.  
  
	SELECT ROUND(SUM(lat_n), 4) FROM station WHERE lat_n > 38.7880 AND lat_n < 137.2345;