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
  
	SELECT country.continent, FLOOR(AVG(city.population)) FROM country, city WHERE country.code = city.countrycode GROUP BY country.continent;  
  
  
  
# The Report  
  
You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818166-a5c852caa0-1.png)  
  
Grades contains the following data:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818137-69b76d805c-2.png)  
  
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.  
  
Write a query to help Eve.  
  
***Note***: Print "NULL"  as the name if the grade is less than 8.  
  
***Sample Input***  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818093-b79f376ec1-3.png)  
  
***Sample Output***  
  
Maria 10 99  
Jane 9 81  
Julia 9 88  
Scarlet 8 78  
NULL 7 63  
NULL 7 68  
  
	SELECT CASE 
		WHEN Grades.Grade < 8 THEN 'NULL' 
		ELSE Students.Name 
		END 
	, Grades.Grade, Students.Marks 
	FROM Students, Grades 
	WHERE Students.Marks >= Grades.Min_mark AND Students.Marks <= Grades.Max_mark 
	ORDER BY Grades.Grade DESC, Students.Name;
  
  
  
# Top Competitors  
  
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.  
  
***Input Format***  
  
The following tables contain contest data:  
  
Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png)  
  
Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png)  
  
Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png)  
  
Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.   
  
![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png)  
  
	SELECT Submissions.hacker_id, Hackers.name from Hackers, Submissions, Challenges, Difficulty
	WHERE Submissions.score = Difficulty.score
	AND Hackers.hacker_id = Submissions.hacker_id 
	AND Submissions.challenge_id = Challenges.challenge_id 
	AND Challenges.difficulty_level = Difficulty.difficulty_level
	GROUP BY Submissions.hacker_id, Hackers.name
	HAVING count(*) > 1 
	ORDER BY count(*) DESC, Submissions.hacker_id ASC;
  
  
  
# Ollivander's Inventory  
  
Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.  
  
Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.  
  
***Input Format***  
  
The following tables contain data on the wands in Ollivander's inventory:  
  
Wands: The id is the id of the wand, code is the code of the wand, coins_needed is the total number of gold galleons needed to buy the wand, and power denotes the quality of the wand (the higher the power, the better the wand is).  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png)  
  
Wands_Property: The code is the code of the wand, age is the age of the wand, and is_evil denotes whether the wand is good for the dark arts. If the value of is_evil is 0, it means that the wand is not evil. The mapping between code and age is one-one, meaning that if there are two pairs, (code1, age1) and (code2, age2), then code1 != code2 and age1 != age2.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png)  
  
***Sample Input***   
  
Wands Table:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538559-51bf29644e-ScreenShot2016-03-21at10.34.41AM.png)  
  
Wands_Property Table:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538583-fd514566f9-ScreenShot2016-03-21at10.34.28AM.png)  
  
***Sample Output***   
  
9 45 1647 10  
12 17 9897 10  
1 20 3688 8  
15 40 6018 7  
19 20 7651 6  
11 40 7587 5  
10 20 504 5  
18 40 3312 3  
20 17 5689 3  
5 45 6020 2  
14 40 5408 1  
  
	SELECT id, age, coins_needed, power FROM Wands JOIN Wands_Property ON Wands.code = Wands_Property.code
	WHERE (age, coins_needed, power) IN (
		SELECT age, MIN(coins_needed), power
		FROM Wands JOIN Wands_Property ON Wands.code = Wands_Property.code
		WHERE Wands_Property.is_evil = 0
		GROUP BY age, power)
	ORDER BY power DESC, age DESC;
  
  
  
# Challenges  
  
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.  
  
***Input Format***  
  
The following tables contain challenge data:  
  
Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png)  
  
Challenges: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png)  
  
***Sample Input 0***  
  
Hackers Table:   
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png)  
  
Challenges Table:  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png)  
  
***Sample Output 0***
  
21283 Angela 6   
88255 Patrick 5  
96196 Lisa 1  
  
***Sample Input 1***  
  
Hackers Table:  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png)  
  
Challenges Table:  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png)  
  
***Sample Output 1***
  
12299 Rose 6  
34856 Angela 6  
79345 Frank 4  
80491 Patrick 3  
81041 Lisa 1  
  
***Explanation***  
  
For Sample Case 0, we can get the following details:  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png)  
  
Students 5077 and 62743 both created 4 challenges, but the maximum number of challenges created is 6 so these students are excluded from the result.  
  
For Sample Case 1, we can get the following details:  
![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png)  
  
Students 12299 and 34856 both created 6 challenges. Because 6 is the maximum number of challenges created, these students are included in the result.  
  
	WITH a AS(
		SELECT h.hacker_id, name, count(c.challenge_id) AS nums 
		FROM hackers h join challenges c ON	h.hacker_id = c.hacker_id 
		GROUP BY h.hacker_id,h.name) 
	SELECT hacker_id, name, nums 
	FROM a 
	WHERE nums NOT IN (
		SELECT nums FROM a WHERE nums < (
			SELECT max(nums) FROM a
		) 
		GROUP BY nums 
		HAVING count(nums) > 1 ) 
	ORDER BY nums desc, hacker_id;
