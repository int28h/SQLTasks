# Type of Triangle  
  
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:  
  
Equilateral: It's a triangle with 3 sides of equal length.  
Isosceles: It's a triangle with 2 sides of equal length.  
Scalene: It's a triangle with 3 sides of differing lengths.  
Not A Triangle: The given values of A, B, and C don't form a triangle.  
  
***Input Format***  
  
The TRIANGLES table is described as follows:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png)  
  
	SELECT 
	CASE 
	WHEN (A + B <= C) OR (B + C <= A) OR(A + C <= B) THEN 'Not A Triangle'
	WHEN (A = B) AND (B = C) THEN 'Equilateral'
	WHEN (A =B) OR (C = A) OR (B = C) THEN 'Isosceles'
	ELSE 'Scalene'
	END 
	FROM TRIANGLES;
  
  	
  	
# The PADS  
  
Generate the following two result sets:  

1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).  
2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:  
	There are a total of [occupation_count] [occupation]s.  
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.  
  
***Note:*** There will be at least two entries in the table for each type of occupation.  
  
***Input Format***  
The OCCUPATIONS table is described as follows:   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)  
  
Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.  
  
***Sample Input***  
An OCCUPATIONS table that contains the following records:  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png)  
  
***Sample Output***  
	Ashely(P)  
	Christeen(P)  
	Jane(A)  
	Jenny(D)  
	Julia(A)  
	Ketty(P)  
	Maria(A)  
	Meera(S)  
	Priya(S)  
	Samantha(D)  
	There are a total of 2 doctors.  
	There are a total of 2 singers.  
	There are a total of 3 actors.  
	There are a total of 3 professors.   
  
	SELECT (name || '(' || SUBSTR(occupation,1,1) || ')') FROM occupations ORDER BY name;
	SELECT ('There are a total of ' || COUNT(occupation) || ' ' || LOWER(occupation) || 's' || '.') FROM occupations GROUP BY occupation ORDER BY COUNT(occupation), occupation ASC;
  
  
  
# Occupations  
  
Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.  
  
***Note:*** Print NULL when there are no more names corresponding to an occupation.  
  
***Input Format***  
The OCCUPATIONS table is described as follows:   
  
![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)  
  
Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.  
  
***Sample Input***  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12890/1443817648-1b2b8add45-2.png)  
  
***Sample Output***  
  
	Jenny    Ashley     Meera  Jane
	Samantha Christeen  Priya  Julia
	NULL     Ketty      NULL   Maria
  
***Explanation***  
  
The first column is an alphabetically ordered list of Doctor names.  
The second column is an alphabetically ordered list of Professor names.  
The third column is an alphabetically ordered list of Singer names.  
The fourth column is an alphabetically ordered list of Actor names.  
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.  
  
	SELECT Doctor, Professor, Singer, Actor FROM (
	SELECT ROW_NUMBER() OVER (PARTITION BY occupation ORDER BY name) as rn, name, occupation FROM       occupations) 
	PIVOT 
	(MAX(name) FOR occupation IN ('Doctor' as Doctor,'Professor' as Professor, 'Singer' as Singer, 'Actor' as Actor)) 
	ORDER BY rn;
  
  
  
# Binary Tree Nodes  
  
You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)  
  
Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

Root: If node is root node.  
Leaf: If node is leaf node.  
Inner: If node is neither root nor leaf node.  
  
***Sample Input***  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)  
  
***Sample Output***  
  
1 Leaf  
2 Inner  
3 Leaf  
5 Root  
6 Leaf  
8 Inner  
9 Leaf  
  
***Explanation***  
  
![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)  
  
	SELECT N,
	CASE
	WHEN P IS NULL THEN 'Root'
	WHEN N IN (SELECT P FROM BST) THEN 'Inner'
	ELSE 'Leaf'
	END
	FROM BST
	ORDER by N;
  
  
  
# New Companies  
  
Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)  
  
Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.   
  
***Note:***  
The tables may contain duplicate records.  
The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.  
  
***Input Format***  
The following tables contain company data:  
Company: The company_code is the code of the company and founder is the founder of the company.   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)  
  
Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)  
  
Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)  
  
Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.  
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)  
  
Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.   
  
![IMG](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)  
  
	SELECT c.company_code, c.founder, COUNT(DISTINCT e.lead_manager_code), COUNT(DISTINCT e.senior_manager_code), COUNT(DISTINCT e.manager_code), COUNT(DISTINCT e.employee_code) FROM company c
	JOIN employee e ON c.company_code = e.company_code GROUP BY c.company_code, c.founder ORDER BY c.company_code;
	