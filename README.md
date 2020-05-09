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
min:1	 max:5		avg:3.7082
ii. Table: Business, Column: Stars
min:1		max:5		avg:3.6549
iii. Table: Tip, Column: Likes
min:0		max:2		avg:0.0144
iv. Table: Checkin, Column: Count
min:1		max:53		avg:1.9414
v. Table: User, Column: Review_count
min:0		max:2000		avg:24.2995

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
Copy and Paste the Result Below:
8. Does posing more reviews correlate with more fans?
Please explain your findings and interpretation of the results:
9. Are there more reviews with the word "love" or with the word "hate" in them?
Answer:
SQL code used to arrive at answer:
10. Find the top 10 users with the most fans:
SQL code used to arrive at answer:
Copy and Paste the Result Below:
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
