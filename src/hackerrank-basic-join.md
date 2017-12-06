# Asian Population  
  
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.  
***Note:*** CITY.CountryCode and COUNTRY.Code are matching key columns.  
  
***Input Format***  
  
The CITY and COUNTRY tables are described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)  
  
![img](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)  
  
	SELECT SUM(city.population) FROM country INNER JOIN city ON country.code = city.countrycode WHERE country.continent = 'Asia';
  
  
  
# African Cities  
  
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.   
  
	SELECT city.name FROM country INNER JOIN city ON country.code = city.countrycode WHERE country.continent = 'Africa';
  
  
  
# Average Population of Each Continent  
  
Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.  
  
	SELECT country.continent, FLOOR(AVG(city.population)) FROM country, city WHERE country.code = city.countrycode GROUP BY country.continent ;