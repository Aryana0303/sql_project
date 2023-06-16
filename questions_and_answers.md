# Movie_Database_Analysis
## Questions and Answers

**Collaborators**: Aryana Sharma, Arshiya Mahajan

#### Ques 1. What were the top 5 highest-rated movies from 2006-2016?

````sql
SELECT Title, Rating FROM movies.movie_ratings
ORDER BY Rating DESC
LIMIT 5;
````

**Results:**

| Title            | Rating | 
|------------------|--------|
| The Dark Knight  |      9 |   
| Inception        |    8.8 |   
| Kimi no na wa    |    8.6 |   
| Interstellar     |    8.6 |   
| The Intouchables |    8.6 |


#### Ques 2. Do the Directors and the Cast have an impact on movie ratings?
````sql
SELECT Director, Actors, AVG(Rating) AS average_rating
FROM movies.movie_ratings
GROUP BY Director, Actors
HAVING AVG(Rating) > (SELECT AVG(Rating) FROM movies.movie_ratings)
limit 20;
````
**Results:**

| Director                         | Actors                                                                        | average_rating |   |   |
|----------------------------------|-------------------------------------------------------------------------------|----------------|---|---|
| Christopher Nolan                | Christian Bale, Heath Ledger, Aaron Eckhart,Michael Caine                     |              9 |   |   |
| Christopher Nolan                | Leonardo DiCaprio, Joseph Gordon-Levitt, Ellen Page, Ken Watanabe             |            8.8 |   |   |
| Olivier Nakache                  | François Cluzet, Omar Sy, Anne Le Ny, Audrey Fleurot                          |            8.6 |   |   |
| Christopher Nolan                | Matthew McConaughey, Anne Hathaway, Jessica Chastain, Mackenzie Foy           |            8.6 |   |   |
| Makoto Shinkai                   | Ryûnosuke Kamiki, Mone Kamishiraishi, Ryô Narita, Aoi Yuki                    |            8.6 |   |   |
| Christopher Nolan                | Christian Bale, Hugh Jackman, Scarlett Johansson, Michael Caine               |            8.5 |   |   |
| Martin Scorsese                  | Leonardo DiCaprio, Matt Damon, Jack Nicholson, Mark Wahlberg                  |            8.5 |   |   |
| Florian Henckel von Donnersmarck | Ulrich Mühe, Martina Gedeck,Sebastian Koch, Ulrich Tukur                      |            8.5 |   |   |
| Aamir Khan                       | Darsheel Safary, Aamir Khan, Tanay Chheda, Sachet Engineer                    |            8.5 |   |   |
| Christopher Nolan                | Christian Bale, Tom Hardy, Anne Hathaway,Gary Oldman                          |            8.5 |   |   |
| Damien Chazelle                  | Miles Teller, J.K. Simmons, Melissa Benoist, Paul Reiser                      |            8.5 |   |   |
| Rajkumar Hirani                  | Aamir Khan, Madhavan, Mona Singh, Sharman Joshi                               |            8.4 |   |   |
| Quentin Tarantino                | Jamie Foxx, Christoph Waltz, Leonardo DiCaprio,Kerry Washington               |            8.4 |   |   |
| Quentin Tarantino                | Brad Pitt, Diane Kruger, Eli Roth,Mélanie Laurent                             |            8.3 |   |   |
| Pete Docter                      | Edward Asner, Jordan Nagai, John Ratzenberger, Christopher Plummer            |            8.3 |   |   |
| Lee Unkrich                      | Tom Hanks, Tim Allen, Joan Cusack, Ned Beatty                                 |            8.3 |   |   |
| Thomas Vinterberg                | Mads Mikkelsen, Thomas Bo Larsen, Annika Wedderkopp, Lasse Fogelstrøm         |            8.3 |   |   |
| Damien Chazelle                  | Ryan Gosling, Emma Stone, Rosemarie DeWitt, J.K. Simmons                      |            8.3 |   |   |
| Guillermo del Toro               | Ivana Baquero, Ariadna Gil, Sergi López,Maribel Verdú                         |            8.2 |   |   |
| Juan José Campanella             | Ricardo Darín, Soledad Villamil, Pablo Rago,Carla Quevedo                     |            8.2 |   |   |

Conclusion: In this query, we retrieve the director, cast, and average ratings for movies grouped by the director and cast. The `HAVING` clause filters the results to only include combinations (director and cast) that have an average rating higher than the overall average rating of all movies.

By comparing the average rating of movies associated with a specific director and cast to the overall average rating, this query helps identify instances where a director and cast combination tends to yield higher-rated movies, suggesting an impact on the movie rating.

#### Ques 3. Do votes and ratings have a correlation?

````sql
SELECT
CORR(votes, rating) AS correlation_coefficient
FROM
movies.movie_ratings;
````

**Results:**

| correlation_coefficient |   |   |   |   |
|-------------------------|---|---|---|---|
|            0.5174521336 |   |   |   |   |
|                         |   |   |   |   |
|                         |   |   |   |   |

Conclusion: A value close to 1 indicates a strong positive correlation, a value close to -1 indicates a strong negative correlation and a value close to 0 indicates no or weak correlation.

Hence, it can be seen that there exists minimal positive correlation between votes and ratings.

#### Ques 4. Retrieve the directors whose movies have consistently high ratings (all movies have a rating above 8).

````sql
SELECT Director
FROM movies.movie_ratings
GROUP BY Director
HAVING MIN(Rating) > 8;

````

**Results:**

| Director                         |   |   |
|----------------------------------|---|---|
| Christopher Nolan                |   |   |
| Florian Henckel von Donnersmarck |   |   |
| Aamir Khan                       |   |   |
| Sean Penn                        |   |   |
| Juan José Campanella             |   |   |
| Pete Docter                      |   |   |
| Rajkumar Hirani                  |   |   |
| Lee Unkrich                      |   |   |
| Olivier Nakache                  |   |   |
| Thomas Vinterberg                |   |   |
| Damien Chazelle                  |   |   |
| Xavier Dolan                     |   |   |
| Damián Szifron                   |   |   |
| Tom McCarthy                     |   |   |
| Lenny Abrahamson                 |   |   |
| Garth Davis                      |   |   |
| Byron Howard                     |   |   |
| Chan-wook Park                   |   |   |
| Makoto Shinkai                   |   |   |

Conclusion: We can see that Christopher Nolan, Florian Henckel von Donnersmarck, Aamir Khan, Sean Penn, Juan José Campanella are among the directors who directed the highest rating movies of all times.

#### Ques 5. Retrieve the movies that have a rating higher than the average rating of all movies in the same genre and year.

````sql
SELECT Title, Genre, Year, Rating
FROM movies.movie_ratings
WHERE Rating > (
  SELECT AVG(Rating)
  FROM movies.movie_ratings
  WHERE genre = Genre AND year = Year
)
limit 30;
````

**Results:**

| Title                                                         | Genre                      | Year | Rating |   |
|---------------------------------------------------------------|----------------------------|------|--------|---|
| The Host                                                      | Comedy,Drama,Horror        | 2006 |      7 |   |
| Babel                                                         | Drama                      | 2006 |    7.5 |   |
| Perfume: The Story of a Murderer                              | Crime,Drama,Fantasy        | 2006 |    7.5 |   |
| Casino Royale                                                 | Action,Adventure,Thriller  | 2006 |      8 |   |
| The Pursuit of Happyness                                      | Biography,Drama            | 2006 |      8 |   |
| Blood Diamond                                                 | Adventure,Drama,Thriller   | 2006 |      8 |   |
| The Prestige                                                  | Drama,Mystery,Sci-Fi       | 2006 |    8.5 |   |
| The Departed                                                  | Crime,Drama,Thriller       | 2006 |    8.5 |   |
| The Lives of Others                                           | Drama,Thriller             | 2006 |    8.5 |   |
| Pirates of the Caribbean: Dead Man's Chest                    | Action,Adventure,Fantasy   | 2006 |    7.3 |   |
| The Fountain                                                  | Drama,Sci-Fi               | 2006 |    7.3 |   |
| Rescue Dawn                                                   | Adventure,Biography,Drama  | 2006 |    7.3 |   |
| Apocalypto                                                    | Action,Adventure,Drama     | 2006 |    7.8 |   |
| Little Miss Sunshine                                          | Comedy,Drama               | 2006 |    7.8 |   |
| Lucky Number Slevin                                           | Crime,Drama,Mystery        | 2006 |    7.8 |   |
| Cars                                                          | Animation,Adventure,Comedy | 2006 |    7.1 |   |
| The Illusionist                                               | Drama,Mystery,Romance      | 2006 |    7.6 |   |
| Inside Man                                                    | Crime,Drama,Mystery        | 2006 |    7.6 |   |
| Pan's Labyrinth                                               | Drama,Fantasy,War          | 2006 |    8.2 |   |
| A Good Year                                                   | Comedy,Drama,Romance       | 2006 |    6.9 |   |
| Mission: Impossible III                                       | Action,Adventure,Thriller  | 2006 |    6.9 |   |
| Children of Men                                               | Drama,Sci-Fi,Thriller      | 2006 |    7.9 |   |
| The Fall                                                      | Adventure,Comedy,Drama     | 2006 |    7.9 |   |
| Rocky Balboa                                                  | Drama,Sport                | 2006 |    7.2 |   |
|                                                           300 | Action,Fantasy,War         | 2006 |    7.7 |   |
| Knocked Up                                                    | Comedy,Romance             | 2007 |      7 |   |
| 28 Weeks Later                                                | Drama,Horror,Sci-Fi        | 2007 |      7 |   |
| Harry Potter and the Order of the Phoenix                     | Adventure,Family,Fantasy   | 2007 |    7.5 |   |
| Juno                                                          | Comedy,Drama               | 2007 |    7.5 |   |
| The Assassination of Jesse James by the Coward Robert Ford    | Biography,Crime,Drama      | 2007 |    7.5 |   |
                                             

#### Ques 6. What is the most common genre combinations in movies?

````sql
SELECT
Genre,
COUNT(*) AS frequency
FROM (
SELECT
ARRAY_TO_STRING(ARRAY_AGG(DISTINCT Genre ORDER BY Genre), ',') AS Genre
FROM movies.movie_ratings
GROUP BY Title
) subquery
GROUP BY Genre
ORDER BY frequency DESC
limit 30;

````

**Results:**

| Genre                                        | frequency |   |   |   |
|----------------------------------------------|-----------|---|---|---|
| Action,Adventure,Sci-Fi                      |        50 |   |   |   |
| Comedy,Drama,Romance                         |        30 |   |   |   |
| Drama                                        |        29 |   |   |   |
| Drama,Romance                                |        27 |   |   |   |
| Animation,Adventure,Comedy                   |        26 |   |   |   |
| Comedy                                       |        26 |   |   |   |
| Action,Adventure,Fantasy                     |        25 |   |   |   |
| Comedy,Drama                                 |        24 |   |   |   |
| Comedy,Romance                               |        22 |   |   |   |
| Crime,Drama,Thriller                         |        18 |   |   |   |
| Crime,Drama,Mystery                          |        18 |   |   |   |
| Action,Adventure,Drama                       |        17 |   |   |   |
| Action,Crime,Drama                           |        16 |   |   |   |
| Adventure,Family,Fantasy                     |        14 |   |   |   |
| Action,Adventure,Comedy                      |        14 |   |   |   |
| Drama,Thriller                               |        12 |   |   |   |
| Biography,Drama,History                      |        12 |   |   |   |
| Action,Comedy,Crime                          |        12 |   |   |   |
| Action,Crime,Thriller                        |        11 |   |   |   |
| Action,Adventure,Thriller                    |        11 |   |   |   |
| Biography,Drama                              |        11 |   |   |   |
| Horror,Thriller                              |        11 |   |   |   |
| Adventure,Comedy,Drama                       |         8 |   |   |   |
| Biography,Crime,Drama                        |         8 |   |   |   |
| Animation,Action,Adventure                   |         8 |   |   |   |
| Action,Thriller                              |         8 |   |   |   |
| Crime,Drama                                  |         8 |   |   |   |
| Horror                                       |         7 |   |   |   |
| Horror,Mystery,Thriller                      |         7 |   |   |   |
| Biography,Drama,Sport                        |         7 |   |   |   |

Conclusion: Action,Adventure,Sci-Fi is the most famous combination of genres throughput 2006-2016.

