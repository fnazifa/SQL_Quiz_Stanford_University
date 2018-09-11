# seq-exercise-sql_movie_query_core
Stanford University_Databases: DB5 SQL

Q.1) Find the titles of all movies directed by Steven Spielberg.

Ans) select title
	 from Movie
	 where director = 'Steven Spielberg';

Q.2) Find all years that have a movie that received a rating of 4 or 5, and sort them in increasing order.

Ans) select distinct year
	 from Movie, Rating
	 where Movie.mID = Rating.mID and stars>=4;

Q.3) Find the titles of all movies that have no ratings.

Ans) select distinct title
	 from Movie, Rating
	 where Movie.mID not in (select mID from Rating);

Q.4) Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

Ans) select name
	 from Reviewer, Rating
	 where Reviewer.rID = Rating.rID and Rating.ratingDate is null;

Q.5) Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars.

Ans) select distinct name, title, stars, ratingDate
	 from Reviewer, Movie, Rating
	 where Movie.mID = Rating.mID and Reviewer.rID = Rating.rID;

Q.6) For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie. 

Ans) select name, title
	 from Movie
	 inner join Rating R1 using (mId)
	 inner join Rating R2 using (rId)
	 inner join Reviewer using (rId)
	 where R1.mId = R2.mId and R1.ratingDate < R2.ratingDate and R1.stars < R2.stars;

Q.7) For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title. 

Ans) select title, max(stars) from Movie, Rating
	 where Movie.mID = Rating.mID
	 group by Rating.mID
	 order by title asc;
	 
Q.8) Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

Ans) select name
	 from Reviewer, Rating
	 where Reviewer.rID = Rating.rID and Rating.ratingDate is null;

Q.9) Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

Ans) select name
	 from Reviewer, Rating
	 where Reviewer.rID = Rating.rID and Rating.ratingDate is null;
