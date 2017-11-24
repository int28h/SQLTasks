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
  
Note: There will be at least two entries in the table for each type of occupation.  
  
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