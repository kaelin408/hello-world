by kaelin morris
date 5/8/2020
Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below: 
i. Attribute table = 10,000 
ii. Business table = 10,000 
iii. Category table = 10,000 
iv. Checkin table = 10,000 
v. elite_years table = 10,000 
vi. friend table = 10,000 
vii. hours table = 10,000 
viii. photo table = 10,000 
ix. review table = 10,000 
x. tip table = 10,000 
xi. user table = 10,000 

SELECT COUNT(*)
FROM table   

2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

SELECT COUNT(DISTINCT(key))
FROM table
    
i. Business =10,000
ii. Hours =1562
iii. Category =2643
iv. Attribute =1115
v. Review =10,000
vi. Checkin = 493
vii. Photo =10,000
viii. Tip = 537
ix. User = 10,000
x. Friend = 11
xi. Elite_years =2780

Sample code:
select count(distinct name)  + count(distinct business_id) + count(distinct value)
as
total_records
from attribute;
+---------------+
| total_records |
+---------------+
|          1115 |
+---------------+

3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

Answer: no, there are zero null values 

SQL code used to arrive at answer:
SELECT COUNT(*)
FROM user
WHERE id IS NULL OR 
name IS NULL OR
review_count IS NULL OR 
yelping_since IS NULL OR
useful IS NULL OR
funny IS NULL OR 
cool IS NULL OR 
fans IS NULL OR 
average_stars IS NULL OR 
compliment_hot IS NULL OR 
compliment_more IS NULL OR
compliment_profile IS NULL OR 
compliment_cute IS NULL OR 
compliment_list IS NULL OR 
compliment_note IS NULL OR
compliment_plain IS NULL OR
compliment_cool IS NULL OR
compliment_funny IS NULL OR 
compliment_writer IS NULL OR 
compliment_photos IS NULL 

4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

SQL code used to arrive at answer:
select min(stars)
,max(stars)
,avg(stars)
from review;
+------------+------------+------------+
| min(stars) | max(stars) | avg(stars) |
+------------+------------+------------+
|          1 |          5 |     3.7082 |
    
i. Table: Review, Column: Stars
min:1	 
max:5	 
avg:3.7082
ii. Table: Business, Column: Stars
min:1	
max:5	
avg:3.6549
iii. Table: Tip, Column: Likes
min:0	
max:2	
avg:0.0144
iv. Table: Checkin, Column: Count
min:1	
max:53		
avg:1.9414
v. Table: User, Column: Review_count
min:0	
max:2000	
avg:24.2995

5. List the cities with the most reviews in descending order:
SQL code used to arrive at answer:
SELECT city,SUM(review_count) AS reviews
FROM business
GROUP BY city
ORDER BY NUM DESC
                +-----------------+---------+
		| city            | reviews |
		+-----------------+---------+
		| Las Vegas       |   82854 |
		| Phoenix         |   34503 |
		| Toronto         |   24113 |
		| Scottsdale      |   20614 |
		| Charlotte       |   12523 |
		| Henderson       |   10871 |
		| Tempe           |   10504 |
		| Pittsburgh      |    9798 |
		| Montréal        |    9448 |
		| Chandler        |    8112 |
		| Mesa            |    6875 |
		| Gilbert         |    6380 |
		| Cleveland       |    5593 |
		| Madison         |    5265 |
		| Glendale        |    4406 |
		| Mississauga     |    3814 |
		| Edinburgh       |    2792 |
		| Peoria          |    2624 |
		| North Las Vegas |    2438 |
		| Markham         |    2352 |
		| Champaign       |    2029 |
		| Stuttgart       |    1849 |
		| Surprise        |    1520 |
		| Lakewood        |    1465 |
		| Goodyear        |    1155 |
		+-----------------+---------+

6. Find the distribution of star ratings to the business in the following cities:
i. Avon
SQL code used to arrive at answer:
SELECT stars,SUM(review_count) AS count
FROM business
WHERE city == 'Avon'
GROUP BY stars
+-------+-------+
| stars | count |
+-------+-------+
|   1.5 |    10 |
|   2.5 |     6 |
|   3.5 |    88 |
|   4.0 |    21 |
|   4.5 |    31 |
|   5.0 |     3 |
+-------+-------+
ii. Beachwood
SQL code used to arrive at answer:
SELECT stars,SUM(review_count) AS count
FROM business
WHERE city == 'Beachwood'
GROUP BY stars
+-------+-------+
| stars | count |
+-------+-------+
|   2.0 |     8 |
|   2.5 |     3 |
|   3.0 |    11 |
|   3.5 |     6 |
|   4.0 |    69 |
|   4.5 |    17 |
|   5.0 |    23 |
+-------+-------+

7. Find the top 3 users based on their total number of reviews:
SQL code used to arrive at answer:
SELECT u.name, u.id, u.review_count
FROM user u
GROUP BY u.review_count
GROUP BY u.review_count
+-----------+------------------------+--------------+
| name      | id                     | review_count |
+-----------+------------------------+--------------+
| Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |         2000 |
| Sara      | -3s52C4zL_DHRK0ULG6qtg |         1629 |
| Yuri      | -8lbUNlXVSoXqaRRiHiSNg |         1339 |
| .Hon      | -K2Tcgh2EKX6e6HqqIrBIQ |         1246 |
| William   | -FZBTkAZEXoP7CYvRV2ZwQ |         1215 |
| Harald    | --2vR0DIsmQ6WfcSzKWigw |         1153 |
| eric      | -gokwePdbXjfS0iF7NsUGA |         1116 |
| Roanna    | -DFCC64NXgqrxlO8aLU5rg |         1039 |
| Mimi      | -8EnCioUmDygAbsYZmTeRQ |          968 |
| Christine | -0IiMAZI2SsQ7VmyzJjokQ |          930 |
| Ed        | -fUARDNuXAfrOn4WLSZLgA |          904 |
| Nicole    | -hKniZN2OdshWLHYuj21jQ |          864 |
| Fran      | -9da1xk7zgnnfO1uTVYGkA |          862 |
| Mark      | -B-QEUESGWHPE_889WJaeg |          861 |
| Christina | -kLVfaJytOJY2-QdQoCcNQ |          842 |
| Dominic   | -kO6984fXByyZm3_6z2JYg |          836 |
| Lissa     | -lh59ko3dxChBSZ9U7LfUw |          834 |
| Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |          813 |
| Alison    | -l9giG8TSDBG1jnUBUXp5w |          775 |
| Sui       | -dw8f7FLaUmWR7bfJ_Yf0w |          754 |
| Tim       | -AaBjWJYiQxXkCMDlXfPGw |          702 |
| L         | -jt1ACMiZljnBFvS6RRvnA |          696 |
| Angela    | -IgKkE8JvYNWeGu8ze4P8Q |          694 |
| Crissy    | -hxUwfo3cMnLTv-CAaP69A |          676 |
| Lyn       | -H6cTbVxeIRYR-atxdielQ |          675 |
+-----------+------------------------+--------------+
(Output limit exceeded, 25 of 367 total rows shown)	

8. Does posing more reviews correlate with more fans?
Please explain your findings and interpretation of the results:
SELECT id,
name,
review_count,
fans,
yelping_since
FROM user
ORDER BY fans DESC
                +------------------------+-----------+--------------+------+---------------------+
		| id                     | name      | review_count | fans | yelping_since       |
		+------------------------+-----------+--------------+------+---------------------+
		| -9I98YbNQnLdAmcYfb324Q | Amy       |          609 |  503 | 2007-07-19 00:00:00 |
		| -8EnCioUmDygAbsYZmTeRQ | Mimi      |          968 |  497 | 2011-03-30 00:00:00 |
		| --2vR0DIsmQ6WfcSzKWigw | Harald    |         1153 |  311 | 2012-11-27 00:00:00 |
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |         2000 |  253 | 2012-12-16 00:00:00 |
		| -0IiMAZI2SsQ7VmyzJjokQ | Christine |          930 |  173 | 2009-07-08 00:00:00 |
		| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |          813 |  159 | 2009-10-05 00:00:00 |
		| -9bbDysuiWeo2VShFJJtcw | Cat       |          377 |  133 | 2009-02-05 00:00:00 |
		| -FZBTkAZEXoP7CYvRV2ZwQ | William   |         1215 |  126 | 2015-02-19 00:00:00 |
		| -9da1xk7zgnnfO1uTVYGkA | Fran      |          862 |  124 | 2012-04-05 00:00:00 |
		| -lh59ko3dxChBSZ9U7LfUw | Lissa     |          834 |  120 | 2007-08-14 00:00:00 |
		| -B-QEUESGWHPE_889WJaeg | Mark      |          861 |  115 | 2009-05-31 00:00:00 |
		| -DmqnhW4Omr3YhmnigaqHg | Tiffany   |          408 |  111 | 2008-10-28 00:00:00 |
		| -cv9PPT7IHux7XUc9dOpkg | bernice   |          255 |  105 | 2007-08-29 00:00:00 |
		| -DFCC64NXgqrxlO8aLU5rg | Roanna    |         1039 |  104 | 2006-03-28 00:00:00 |
		| -IgKkE8JvYNWeGu8ze4P8Q | Angela    |          694 |  101 | 2010-10-01 00:00:00 |
		| -K2Tcgh2EKX6e6HqqIrBIQ | .Hon      |         1246 |  101 | 2006-07-19 00:00:00 |
		| -4viTt9UC44lWCFJwleMNQ | Ben       |          307 |   96 | 2007-03-10 00:00:00 |
		| -3i9bhfvrM3F1wsC9XIB8g | Linda     |          584 |   89 | 2005-08-07 00:00:00 |
		| -kLVfaJytOJY2-QdQoCcNQ | Christina |          842 |   85 | 2012-10-08 00:00:00 |
		| -ePh4Prox7ZXnEBNGKyUEA | Jessica   |          220 |   84 | 2009-01-12 00:00:00 |
		| -4BEUkLvHQntN6qPfKJP2w | Greg      |          408 |   81 | 2008-02-16 00:00:00 |
		| -C-l8EHSLXtZZVfUAUhsPA | Nieves    |          178 |   80 | 2013-07-08 00:00:00 |
		| -dw8f7FLaUmWR7bfJ_Yf0w | Sui       |          754 |   78 | 2009-09-07 00:00:00 |
		| -8lbUNlXVSoXqaRRiHiSNg | Yuri      |         1339 |   76 | 2008-01-03 00:00:00 |
		| -0zEEaDFIjABtPQni0XlHA | Nicole    |          161 |   73 | 2009-04-30 00:00:00 |
		+------------------------+-----------+--------------+------+---------------------+
the correlation between review count and number of fans can be positive were both values intercet at a key point. or negative
where both values are moving in opposed directions like the concept of supply and demand.
the resion for this inconsistency depends on a number of factors, such as the time they been yelping,and the general intereste the public is in there review.

9. Are there more reviews with the word "love" or with the word "hate" in them?
Answer: 
love=1780
hate=232
SQL code used to arrive at answer:
select
count (*)
from review
where text like '%love%';
+-----------+
| count (*) |
+-----------+
|      1780 |
+-----------+

select
count (*)
from review
where text like '%hate%';
+-----------+
| count (*) |
+-----------+
|       232 |
+-----------+

10. Find the top 10 users with the most fans:
SQL code used to arrive at answer:
select
name
, id
, fans
from user
order by fans desc;
+-----------+------------------------+------+
| name      | id                     | fans |
+-----------+------------------------+------+
| Amy       | -9I98YbNQnLdAmcYfb324Q |  503 |
| Mimi      | -8EnCioUmDygAbsYZmTeRQ |  497 |
| Harald    | --2vR0DIsmQ6WfcSzKWigw |  311 |
| Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |  253 |
| Christine | -0IiMAZI2SsQ7VmyzJjokQ |  173 |
| Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |  159 |
| Cat       | -9bbDysuiWeo2VShFJJtcw |  133 |
| William   | -FZBTkAZEXoP7CYvRV2ZwQ |  126 |
| Fran      | -9da1xk7zgnnfO1uTVYGkA |  124 |
| Lissa     | -lh59ko3dxChBSZ9U7LfUw |  120 |

11.Is there a strong relationship (or correlation) between having a high number of fans and being listed as "useful" or"funny?" Out of the top 10 users with the highest number offans, what percent are also listed as “useful” or “funny”?
SQL code used to arrive at answer
select
select
, id
, fans
, useful
, funny
from user
order by fans desc;
+-----------+------------------------+------+--------+--------+
| name      | id                     | fans | useful |  funny |
+-----------+------------------------+------+--------+--------+
| Amy       | -9I98YbNQnLdAmcYfb324Q |  503 |   3226 |   2554 |
| Mimi      | -8EnCioUmDygAbsYZmTeRQ |  497 |    257 |    138 |
| Harald    | --2vR0DIsmQ6WfcSzKWigw |  311 | 122921 | 122419 |
| Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |  253 |  17524 |   2324 |
| Christine | -0IiMAZI2SsQ7VmyzJjokQ |  173 |   4834 |   6646 |
| Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |  159 |     48 |     13 |
| Cat       | -9bbDysuiWeo2VShFJJtcw |  133 |   1062 |    672 |
| William   | -FZBTkAZEXoP7CYvRV2ZwQ |  126 |   9363 |   9361 |
| Fran      | -9da1xk7zgnnfO1uTVYGkA |  124 |   9851 |   7606 |
| Lissa     | -lh59ko3dxChBSZ9U7LfUw |  120 |    455 |    150 |
| Mark      | -B-QEUESGWHPE_889WJaeg |  115 |   4008 |    570 |
| Tiffany   | -DmqnhW4Omr3YhmnigaqHg |  111 |   1366 |    984 |
| bernice   | -cv9PPT7IHux7XUc9dOpkg |  105 |    120 |    112 |
| Roanna    | -DFCC64NXgqrxlO8aLU5rg |  104 |   2995 |   1188 |
| Angela    | -IgKkE8JvYNWeGu8ze4P8Q |  101 |    158 |    164 |
| .Hon      | -K2Tcgh2EKX6e6HqqIrBIQ |  101 |   7850 |   5851 |
| Ben       | -4viTt9UC44lWCFJwleMNQ |   96 |   1180 |   1155 |
| Linda     | -3i9bhfvrM3F1wsC9XIB8g |   89 |   3177 |   2736 |
| Christina | -kLVfaJytOJY2-QdQoCcNQ |   85 |    158 |     34 |
| Jessica   | -ePh4Prox7ZXnEBNGKyUEA |   84 |   2161 |   2091 |
| Greg      | -4BEUkLvHQntN6qPfKJP2w |   81 |    820 |    753 |
| Nieves    | -C-l8EHSLXtZZVfUAUhsPA |   80 |   1091 |    774 |
| Sui       | -dw8f7FLaUmWR7bfJ_Yf0w |   78 |      9 |     18 |
| Yuri      | -8lbUNlXVSoXqaRRiHiSNg |   76 |   1166 |    220 |
| Nicole    | -0zEEaDFIjABtPQni0XlHA |   73 |     13 |     10 |
+-----------+------------------------+------+--------+--------+
(Output limit exceeded, 25 of 10000 total rows shown)
based on the results of the data there is a correlation between the number of fans to the number of  “useful” or “funny” but thats for some of the data. if you countinue down the chart you start to see negative correlation, wehere one variable increases and the other variable decrease. thus in total there in no true correlation 

Part 2: Inferences and Analysis
1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

i. Do the two groups you chose to analyze have a different distribution of hours?

ii. Do the two groups you chose to analyze have a different number of reviews?
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
SQL code used for analysis:
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
i. Difference 1:
ii. Difference 2:
SQL code used for analysis:
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.
Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
i. Indicate the type of analysis you chose to do:
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
iii. Output of your finished dataset:
iv. Provide the SQL code you used to create your final dataset:
