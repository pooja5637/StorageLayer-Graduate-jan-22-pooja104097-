1.SELECT the American directors ordered FROM oldest to youngest.
>>SELECT * 
FROM directors 
WHERE nationality='American' 
ORDER BY date_of_birth DESC;

2.Return the Distinct nationalities FROM the directors table.
>>SELECT DISTINCT(nationality) 
FROM directors;

3.Return the first names, last names and date of births of the 10 youngest female actors.
>>SELECT first_name,last_name,date_of_birth 
FROM actors
 ORDER BY date_of_birth ASC 
 LIMIT 10;

4.Return the top 3 movies with the highest international takings.
>>SELECT movie_name,international_takings
FROM movies 
JOIN movie_revenue ON movie_revenue.movie_id=movies.movie_id 
WHERE international_takings IS NOT NULL 
ORDER BY international_takings DESC 
LIMIT 3;

5.Concatenate the first and last names of the directors spearated by a space, and call this new column full_name.
>>SELECT first_name|| ' ' || last_name AS full_name
 FROM directors;

6.Return the actors with missing first_names or data_of_births.
>>SELECT *
 FROM actors
 WHERE first_name IS NULL OR date_of_birth IS NULL;

7.Count the number of actors born after the 1st January 1970.
>>SELECT count(*)
 FROM actors
  WHERE date_of_birth>'1970-01-01';

8.What was the highest and lowest domestic takings for a movie.
>>SELECT min(domestic_takings) as lowest_domestic_takings,
max(domestic_takings) as highest_domestic_takings 
FROM movie_revenue;

9.What is the sum total movie length for movies rated 15.
>>SELECT sum (movie_length) as Total
FROM movies
WHERE age_certificate = '15';

10.How many Japanese directors are in the directors table.
>> SELECT count(*)
 FROM directors
  WHERE nationality='Japanese';

11.What is the average movie length for chinese movies.
>>SELECT avg(movie_length) 
FROM movies 
WHERE movie_lang='Chinese';

12.How many directors are there per nationality?
>>SELECT nationality,count(*) 
FROM directors GROUP BY nationality;

13.What is the sum total movie_length for each age certificate and movie language combination?
>>SELECT movie_lang, age_certificate, SUM(movie_length)
FROM movies
GROUP BY movie_lang, age_certificate
ORDER BY movie_lang, age_certificate;

14.Return the movie languages which have a sum total movie length of over 500 minutes.
>>SELECT movie_lang
FROM movies
GROUP BY movie_lang
HAVING SUM(movie_length) > 500;

15.SELECT the directors first and last names, the movie names, and release dates for all Chinese, Korean, and Japanese movies.
>>SELECT first_name,last_name,movie_name,release_date
FROM movies
JOIN directors on movies.director_id = directors.director_id
WHERE movie_lang in ('Japanese','Chinese','Korean');

16.SELECT the movie names, release dates & international takings of all English language movies.
>>moviedb-# SELECT movie_name,release_date,international_takings
moviedb-# FROM movies
moviedb-# JOIN movie_revenue On movies.movie_id=movie_revenue.movie_id WHERE movie_lang='English';

17.SELECT the movie names, domestic takings and international takings for all movies with either missing domestic takings or missing international takings and order the results by movie name.
>>SELECT movie_name, domestic_takings, international_takings
FROM movies
NATURAL JOIN movie_revenues
WHERE domestic_takings IS NULL OR international_takings IS NULL
ORDER BY movie_name;

18.Use LEFT JOIN to SELECT the first and last names of all British directors and the names and age certificates of the movies that they directed.
>>SELECT first_name, last_name, movie_name, age_certificate
FROM directors
LEFT JOIN movies USING (director_id)
WHERE nationality = 'British';


19.Count the number of movies that each director has directed.
>>SELECT first_name || ' ' || last_name AS full_name, COUNT(movie_id)
FROM directors
NATURAL JOIN movies
GROUP BY director_id;

20.SELECT the first names, last names and dates of birth FROM directors & actors table. Order the result by the date of birth.
>>
SELECT first_name, last_name, date_of_birth
FROM directors
UNION
SELECT first_name, last_name, date_of_birth
FROM actors;


21.SELECT the first and last names of all directprs and actors born in the 1960s. Order the result by last name.
>>
SELECT first_name, last_name 
FROM directors 
WHERE date_of_birth between '1960-01-01' and '1969-12-31'
union 
SELECT first_name, last_name 
FROM actors
WHERE date_of_birth between '1960-01-01' and '1969-12-31' 
ORDER BY last_name;
