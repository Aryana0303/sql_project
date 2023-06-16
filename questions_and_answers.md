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

#### Ques 7. What are the movies with a rating higher than the average rating of their genre?

````sql
SELECT
Title,
Genre,
Rating
FROM (
SELECT
Title,
Genre,
Rating,
AVG(Rating) OVER (PARTITION BY Genre) AS average_rating
FROM movies.movie_ratings
) subquery
WHERE rating > average_rating;
````

**Results:**

| Title                                                      | Genre                      | Rating |
|------------------------------------------------------------|----------------------------|--------|
| Män som hatar kvinnor                                      | Drama,Mystery,Thriller     |    7.8 |
| We Need to Talk About Kevin                                | Drama,Mystery,Thriller     |    7.5 |
| Tinker Tailor Soldier Spy                                  | Drama,Mystery,Thriller     |    7.1 |
| Sunshine                                                   | Adventure,Sci-Fi,Thriller  |    7.3 |
| The Hunger Games                                           | Adventure,Sci-Fi,Thriller  |    7.2 |
| The Love Witch                                             | Comedy,Horror              |    6.2 |
| Underworld Awakening                                       | Action,Fantasy,Horror      |    6.4 |
| The Mortal Instruments: City of Bones                      | Action,Fantasy,Horror      |    5.9 |
| Interstellar                                               | Adventure,Drama,Sci-Fi     |    8.6 |
| The Host                                                   | Comedy,Drama,Horror        |      7 |
| 28 Weeks Later                                             | Drama,Horror,Sci-Fi        |      7 |
| I Am Legend                                                | Drama,Horror,Sci-Fi        |    7.2 |
| The Fighter                                                | Action,Biography,Drama     |    7.8 |
| Lone Survivor                                              | Action,Biography,Drama     |    7.5 |
| Rush                                                       | Action,Biography,Drama     |    8.1 |
| American Sniper                                            | Action,Biography,Drama     |    7.3 |
| Creed                                                      | Drama,Sport                |    7.6 |
| Apocalypto                                                 | Action,Adventure,Drama     |    7.8 |
| Terminator Salvation                                       | Action,Adventure,Drama     |    6.6 |
| The Book of Eli                                            | Action,Adventure,Drama     |    6.9 |
| Robin Hood                                                 | Action,Adventure,Drama     |    6.7 |
| Dawn of the Planet of the Apes                             | Action,Adventure,Drama     |    7.6 |
| Everest                                                    | Action,Adventure,Drama     |    7.1 |
| Shin Gojira                                                | Action,Adventure,Drama     |    6.9 |
| The Illusionist                                            | Drama,Mystery,Romance      |    7.6 |
| El secreto de sus ojos                                     | Drama,Mystery,Romance      |    8.2 |
| Ah-ga-ssi                                                  | Drama,Mystery,Romance      |    8.1 |
| Ted 2                                                      | Adventure,Comedy,Romance   |    6.3 |
| Hanna                                                      | Action,Drama,Thriller      |    6.8 |
| Deepwater Horizon                                          | Action,Drama,Thriller      |    7.2 |
| The Age of Shadows                                         | Action,Drama,Thriller      |    7.2 |
| The Avengers                                               | Action,Sci-Fi              |    8.1 |
| What We Do in the Shadows                                  | Comedy,Fantasy,Horror      |    7.6 |
| Tropic Thunder                                             | Action,Comedy              |      7 |
| Kick-Ass                                                   | Action,Comedy              |    7.7 |
| Kung Fu Panda                                              | Animation,Action,Adventure |    7.6 |
| How to Train Your Dragon                                   | Animation,Action,Adventure |    8.1 |
| The Lego Movie                                             | Animation,Action,Adventure |    7.8 |
| Big Hero 6                                                 | Animation,Action,Adventure |    7.8 |
| How to Train Your Dragon 2                                 | Animation,Action,Adventure |    7.9 |
| Superbad                                                   | Comedy                     |    7.6 |
| Step Brothers                                              | Comedy                     |    6.9 |
| The Hangover                                               | Comedy                     |    7.8 |
| The Dictator                                               | Comedy                     |    6.4 |
| American Reunion                                           | Comedy                     |    6.7 |
| Project X                                                  | Comedy                     |    6.7 |
| The Internship                                             | Comedy                     |    6.3 |
| Let's Be Cops                                              | Comedy                     |    6.5 |
| The Interview                                              | Comedy                     |    6.6 |
| Neighbors                                                  | Comedy                     |    6.4 |
| The DUFF                                                   | Comedy                     |    6.5 |
| Entourage                                                  | Comedy                     |    6.6 |
| Everybody Wants Some!!                                     | Comedy                     |      7 |
| Why Him?                                                   | Comedy                     |    6.3 |
| Bad Moms                                                   | Comedy                     |    6.2 |
| Green Room                                                 | Crime,Horror,Thriller      |      7 |
| Don't Breathe                                              | Crime,Horror,Thriller      |    7.2 |
| Ratatouille                                                | Animation,Comedy,Family    |      8 |
| Sing                                                       | Animation,Comedy,Family    |    7.2 |
| The Theory of Everything                                   | Biography,Drama,Romance    |    7.7 |
| The Shallows                                               | Drama,Horror,Thriller      |    6.4 |
| The Lost City of Z                                         | Action,Adventure,Biography |    7.1 |
| Pirates of the Caribbean: Dead Man's Chest                 | Action,Adventure,Fantasy   |    7.3 |
| X-Men: The Last Stand                                      | Action,Adventure,Fantasy   |    6.7 |
| Pirates of the Caribbean: At World's End                   | Action,Adventure,Fantasy   |    7.1 |
| Hellboy II: The Golden Army                                | Action,Adventure,Fantasy   |      7 |
| Avatar                                                     | Action,Adventure,Fantasy   |    7.8 |
| Underworld: Rise of the Lycans                             | Action,Adventure,Fantasy   |    6.6 |
| Prince of Persia: The Sands of Time                        | Action,Adventure,Fantasy   |    6.6 |
| Thor                                                       | Action,Adventure,Fantasy   |      7 |
| Pirates of the Caribbean: On Stranger Tides                | Action,Adventure,Fantasy   |    6.7 |
| Thor: The Dark World                                       | Action,Adventure,Fantasy   |      7 |
| Man of Steel                                               | Action,Adventure,Fantasy   |    7.1 |
| Star Wars: Episode VII - The Force Awakens                 | Action,Adventure,Fantasy   |    8.1 |
| Warcraft                                                   | Action,Adventure,Fantasy   |      7 |
| Doctor Strange                                             | Action,Adventure,Fantasy   |    7.6 |
| Harry Potter and the Order of the Phoenix                  | Adventure,Family,Fantasy   |    7.5 |
| Stardust                                                   | Adventure,Family,Fantasy   |    7.7 |
| Harry Potter and the Half-Blood Prince                     | Adventure,Family,Fantasy   |    7.5 |
| Harry Potter and the Deathly Hallows: Part 1               | Adventure,Family,Fantasy   |    7.7 |
| Fantastic Beasts and Where to Find Them                    | Adventure,Family,Fantasy   |    7.5 |
| Pete's Dragon                                              | Adventure,Family,Fantasy   |    6.8 |
| The Host                                                   | Action,Adventure,Romance   |    5.9 |
| RocknRolla                                                 | Action,Crime,Thriller      |    7.3 |
| Fast Five                                                  | Action,Crime,Thriller      |    7.3 |
| Furious 6                                                  | Action,Crime,Thriller      |    7.1 |
| John Wick                                                  | Action,Crime,Thriller      |    7.2 |
| The Equalizer                                              | Action,Crime,Thriller      |    7.2 |
| Furious Seven                                              | Action,Crime,Thriller      |    7.2 |
| Prometheus                                                 | Adventure,Mystery,Sci-Fi   |      7 |
| The Maze Runner                                            | Action,Mystery,Sci-Fi      |    6.8 |
| Shooter                                                    | Action,Crime,Drama         |    7.2 |
| The Dark Knight                                            | Action,Crime,Drama         |      9 |
| Looper                                                     | Action,Crime,Drama         |    7.4 |
| Sicario                                                    | Action,Crime,Drama         |    7.6 |
| Chappie                                                    | Action,Crime,Drama         |    6.9 |
| The Accountant                                             | Action,Crime,Drama         |    7.4 |
| The Finest Hours                                           | Action,Drama,History       |    6.8 |
| 13 Hours                                                   | Action,Drama,History       |    7.3 |
| Rise of the Planet of the Apes                             | Action,Drama,Sci-Fi        |    7.6 |
| Snowpiercer                                                | Action,Drama,Sci-Fi        |      7 |
| Maleficent                                                 | Action,Adventure,Family    |      7 |
| Tomorrowland                                               | Action,Adventure,Family    |    6.5 |
| The Visit                                                  | Comedy,Horror,Thriller     |    6.2 |
| Transformers                                               | Action,Adventure,Sci-Fi    |    7.1 |
| The Incredible Hulk                                        | Action,Adventure,Sci-Fi    |    6.8 |
| Iron Man                                                   | Action,Adventure,Sci-Fi    |    7.9 |
| Star Trek                                                  | Action,Adventure,Sci-Fi    |      8 |
| Iron Man 2                                                 | Action,Adventure,Sci-Fi    |      7 |
| Tron                                                       | Action,Adventure,Sci-Fi    |    6.8 |
| Inception                                                  | Action,Adventure,Sci-Fi    |    8.8 |
| X: First Class                                             | Action,Adventure,Sci-Fi    |    7.8 |
| Captain America: The First Avenger                         | Action,Adventure,Sci-Fi    |    6.9 |
| Pacific Rim                                                | Action,Adventure,Sci-Fi    |      7 |
| Star Trek Into Darkness                                    | Action,Adventure,Sci-Fi    |    7.8 |
| Iron Man Three                                             | Action,Adventure,Sci-Fi    |    7.2 |
| X-Men: Days of Future Past                                 | Action,Adventure,Sci-Fi    |      8 |
| Captain America: The Winter Soldier                        | Action,Adventure,Sci-Fi    |    7.8 |
| Guardians of the Galaxy                                    | Action,Adventure,Sci-Fi    |    8.1 |
| Edge of Tomorrow                                           | Action,Adventure,Sci-Fi    |    7.9 |
| Jurassic World                                             | Action,Adventure,Sci-Fi    |      7 |
| Mad Max: Fury Road                                         | Action,Adventure,Sci-Fi    |    8.1 |
| Avengers: Age of Ultron                                    | Action,Adventure,Sci-Fi    |    7.4 |
| X-Men: Apocalypse                                          | Action,Adventure,Sci-Fi    |    7.1 |
| Star Trek Beyond                                           | Action,Adventure,Sci-Fi    |    7.1 |
| Rogue One                                                  | Action,Adventure,Sci-Fi    |    7.9 |
| Captain America: Civil War                                 | Action,Adventure,Sci-Fi    |    7.9 |
| A Good Year                                                | Comedy,Drama,Romance       |    6.9 |
| Forgetting Sarah Marshall                                  | Comedy,Drama,Romance       |    7.2 |
| (500) Days of Summer                                       | Comedy,Drama,Romance       |    7.7 |
| Easy A                                                     | Comedy,Drama,Romance       |    7.1 |
| Crazy, Stupid, Love.                                       | Comedy,Drama,Romance       |    7.4 |
| 50/50                                                      | Comedy,Drama,Romance       |    7.7 |
| Silver Linings Playbook                                    | Comedy,Drama,Romance       |    7.8 |
| The First Time                                             | Comedy,Drama,Romance       |    6.9 |
| The Spectacular Now                                        | Comedy,Drama,Romance       |    7.1 |
| Birdman or (The Unexpected Virtue of Ignorance)            | Comedy,Drama,Romance       |    7.8 |
| PK                                                         | Comedy,Drama,Romance       |    8.2 |
| Before We Go                                               | Comedy,Drama,Romance       |    6.9 |
| The Lobster                                                | Comedy,Drama,Romance       |    7.1 |
| Their Finest                                               | Comedy,Drama,Romance       |      7 |
| Paterson                                                   | Comedy,Drama,Romance       |    7.5 |
| Sherlock Holmes                                            | Action,Adventure,Crime     |    7.6 |
| Sherlock Holmes: A Game of Shadows                         | Action,Adventure,Crime     |    7.5 |
| World War Z                                                | Action,Adventure,Horror    |      7 |
| Little Miss Sunshine                                       | Comedy,Drama               |    7.8 |
| Juno                                                       | Comedy,Drama               |    7.5 |
| 3 Idiots                                                   | Comedy,Drama               |    8.4 |
| The Descendants                                            | Comedy,Drama               |    7.3 |
| Chef                                                       | Comedy,Drama               |    7.3 |
| Me and Earl and the Dying Girl                             | Comedy,Drama               |    7.8 |
| The Dressmaker                                             | Comedy,Drama               |    7.1 |
| The Intern                                                 | Comedy,Drama               |    7.1 |
| En man som heter Ove                                       | Comedy,Drama               |    7.7 |
| Toni Erdmann                                               | Comedy,Drama               |    7.6 |
| The Edge of Seventeen                                      | Comedy,Drama               |    7.4 |
| 20th Century Women                                         | Comedy,Drama               |    7.4 |
| Captain Fantastic                                          | Comedy,Drama               |    7.9 |
| Mr. Church                                                 | Comedy,Drama               |    7.7 |
| The Intouchables                                           | Biography,Comedy,Drama     |    8.6 |
| The Big Short                                              | Biography,Comedy,Drama     |    7.8 |
| The Assassination of Jesse James by the Coward Robert Ford | Biography,Crime,Drama      |    7.5 |
| Freedom Writers                                            | Biography,Crime,Drama      |    7.5 |
| American Gangster                                          | Biography,Crime,Drama      |    7.8 |
| Taken                                                      | Action,Thriller            |    7.8 |
| The Dark Knight Rises                                      | Action,Thriller            |    8.5 |
| Whiplash                                                   | Drama,Music                |    8.5 |
| The Amazing Spider-Man                                     | Action,Adventure           |      7 |
| Lincoln                                                    | Biography,Drama,History    |    7.4 |
| Argo                                                       | Biography,Drama,History    |    7.7 |
| 12 Years a Slave                                           | Biography,Drama,History    |    8.1 |
| Straight Outta Compton                                     | Biography,Drama,History    |    7.9 |
| Hidden Figures                                             | Biography,Drama,History    |    7.8 |
| Hacksaw Ridge                                              | Biography,Drama,History    |    8.2 |
| Goosebumps                                                 | Adventure,Comedy,Family    |    6.3 |
| The Hurt Locker                                            | Drama,History,Thriller     |    7.6 |
| Bridge of Spies                                            | Drama,History,Thriller     |    7.6 |
| The Prestige                                               | Drama,Mystery,Sci-Fi       |    8.5 |
| Moon                                                       | Drama,Mystery,Sci-Fi       |    7.9 |
| Arrival                                                    | Drama,Mystery,Sci-Fi       |      8 |
| Scott Pilgrim vs. the World                                | Action,Comedy,Fantasy      |    7.5 |
| Dracula Untold                                             | Action,Drama,Fantasy       |    6.3 |
| 300: Rise of an Empire                                     | Action,Drama,Fantasy       |    6.2 |
| Harry Potter and the Deathly Hallows: Part 2               | Adventure,Drama,Fantasy    |    8.1 |
| Life of Pi                                                 | Adventure,Drama,Fantasy    |    7.9 |
| Cloverfield                                                | Action,Horror,Sci-Fi       |      7 |
| The Babadook                                               | Drama,Horror               |    6.8 |
| Raw (II)                                                   | Drama,Horror               |    7.5 |
| The Curious Case of Benjamin Button                        | Drama,Fantasy,Romance      |    7.8 |
| The Age of Adaline                                         | Drama,Fantasy,Romance      |    7.2 |
| Blood Diamond                                              | Adventure,Drama,Thriller   |      8 |
| The Revenant                                               | Adventure,Drama,Thriller   |      8 |
| Drive                                                      | Crime,Drama                |    7.8 |
| Lawless                                                    | Crime,Drama                |    7.3 |
| American Hustle                                            | Crime,Drama                |    7.3 |
| The Judge                                                  | Crime,Drama                |    7.4 |
| Bacalaureat                                                | Crime,Drama                |    7.5 |
| Babel                                                      | Drama                      |    7.5 |
| Slumdog Millionaire                                        | Drama                      |      8 |
| Precious                                                   | Drama                      |    7.3 |
| The Help                                                   | Drama                      |    8.1 |
| Melancholia                                                | Drama                      |    7.1 |
| Shame                                                      | Drama                      |    7.2 |
| Jagten                                                     | Drama                      |    8.3 |
| Blue Jasmine                                               | Drama                      |    7.3 |
| Locke                                                      | Drama                      |    7.1 |
| Mommy                                                      | Drama                      |    8.1 |
| Boyhood                                                    | Drama                      |    7.9 |
| Room                                                       | Drama                      |    8.2 |
| Moonlight                                                  | Drama                      |    7.5 |
| Wakefield                                                  | Drama                      |    7.5 |
| Fences                                                     | Drama                      |    7.3 |
| L'avenir                                                   | Drama                      |    7.1 |
| Manchester by the Sea                                      | Drama                      |    7.9 |
| Diary of a Wimpy Kid: Rodrick Rules                        | Comedy,Family              |    6.6 |
| Diary of a Wimpy Kid: Dog Days                             | Comedy,Family              |    6.4 |
| Revolutionary Road                                         | Drama,Romance              |    7.3 |
| Vicky Cristina Barcelona                                   | Drama,Romance              |    7.1 |
| Seven Pounds                                               | Drama,Romance              |    7.7 |
| Blue Valentine                                             | Drama,Romance              |    7.4 |
| Remember Me                                                | Drama,Romance              |    7.2 |
| Jane Eyre                                                  | Drama,Romance              |    7.4 |
| The Perks of Being a Wallflower                            | Drama,Romance              |      8 |
| The Great Gatsby                                           | Drama,Romance              |    7.3 |
| La vie d'Adèle                                             | Drama,Romance              |    7.8 |
| The Fault in Our Stars                                     | Drama,Romance              |    7.8 |
| Brooklyn                                                   | Drama,Romance              |    7.5 |
| The Longest Ride                                           | Drama,Romance              |    7.1 |
| Carol                                                      | Drama,Romance              |    7.2 |
| Dear Zindagi                                               | Drama,Romance              |    7.8 |
| Me Before You                                              | Drama,Romance              |    7.4 |
| The Light Between Oceans                                   | Drama,Romance              |    7.2 |
| Her                                                        | Drama,Romance,Sci-Fi       |      8 |
| I Origins                                                  | Drama,Romance,Sci-Fi       |    7.3 |
|                                                       1408 | Fantasy,Horror             |    6.8 |
| The Bourne Legacy                                          | Action,Adventure,Mystery   |    6.7 |
| Oblivion                                                   | Action,Adventure,Mystery   |      7 |
| The Hunger Games: Catching Fire                            | Action,Adventure,Mystery   |    7.6 |
| Knocked Up                                                 | Comedy,Romance             |      7 |
| Zack and Miri Make a Porno                                 | Comedy,Romance             |    6.6 |
| The Ugly Truth                                             | Comedy,Romance             |    6.5 |
| She's Out of My League                                     | Comedy,Romance             |    6.4 |
| Bridesmaids                                                | Comedy,Romance             |    6.8 |
| Friends with Benefits                                      | Comedy,Romance             |    6.6 |
| Just Go with It                                            | Comedy,Romance             |    6.4 |
| To Rome with Love                                          | Comedy,Romance             |    6.3 |
| What If                                                    | Comedy,Romance             |    6.8 |
| Blended                                                    | Comedy,Romance             |    6.5 |
| Love, Rosie                                                | Comedy,Romance             |    7.2 |
| Bridget Jones's Baby                                       | Comedy,Romance             |    6.7 |
| Warrior                                                    | Action,Drama,Sport         |    8.2 |
| A Monster Calls                                            | Drama,Fantasy              |    7.5 |
| Morgan                                                     | Horror,Sci-Fi,Thriller     |    5.8 |
| District 9                                                 | Action,Sci-Fi,Thriller     |      8 |
| Shutter Island                                             | Mystery,Thriller           |    8.1 |
| The Ghost Writer                                           | Mystery,Thriller           |    7.2 |
| Enemy                                                      | Mystery,Thriller           |    6.9 |
| The Gift                                                   | Mystery,Thriller           |    7.1 |
| The Pursuit of Happyness                                   | Biography,Drama            |      8 |
| Hunger                                                     | Biography,Drama            |    7.6 |
| The King's Speech                                          | Biography,Drama            |      8 |
| The Social Network                                         | Biography,Drama            |    7.7 |
| Dallas Buyers Club                                         | Biography,Drama            |      8 |
| Lion                                                       | Biography,Drama            |    8.1 |
| Horrible Bosses                                            | Comedy,Crime               |    6.9 |
| Seven Psychopaths                                          | Comedy,Crime               |    7.2 |
| We're the Millers                                          | Comedy,Crime               |      7 |
| Orphan                                                     | Horror,Mystery,Thriller    |      7 |
| Insidious                                                  | Horror,Mystery,Thriller    |    6.8 |
| The Conjuring                                              | Horror,Mystery,Thriller    |    7.5 |
| The Conjuring 2                                            | Horror,Mystery,Thriller    |    7.4 |
| Pineapple Express                                          | Action,Comedy,Crime        |      7 |
| RED                                                        | Action,Comedy,Crime        |    7.1 |
| 21 Jump Street                                             | Action,Comedy,Crime        |    7.2 |
| 22 Jump Street                                             | Action,Comedy,Crime        |    7.1 |
| Spy                                                        | Action,Comedy,Crime        |    7.1 |
| Free Fire                                                  | Action,Comedy,Crime        |      7 |
| The Nice Guys                                              | Action,Comedy,Crime        |    7.4 |
| Real Steel                                                 | Action,Drama,Family        |    7.1 |
| Popstar: Never Stop Never Stopping                         | Comedy,Music               |    6.7 |
| Spotlight                                                  | Crime,Drama,History        |    8.1 |
| Let Me In                                                  | Drama,Horror,Mystery       |    7.2 |
| 10 Cloverfield Lane                                        | Drama,Horror,Mystery       |    7.2 |
| The Boy in the Striped Pyjamas                             | Drama,War                  |    7.8 |
| Limitless                                                  | Mystery,Sci-Fi,Thriller    |    7.4 |
| Into the Wild                                              | Adventure,Biography,Drama  |    8.1 |
| 127 Hours                                                  | Adventure,Biography,Drama  |    7.6 |
| The Fall                                                   | Adventure,Comedy,Drama     |    7.9 |
| Moonrise Kingdom                                           | Adventure,Comedy,Drama     |    7.8 |
| The Grand Budapest Hotel                                   | Adventure,Comedy,Drama     |    8.1 |
| Hunt for the Wilderpeople                                  | Adventure,Comedy,Drama     |    7.9 |
| Hairspray                                                  | Comedy,Drama,Family        |    6.7 |
| 17 Again                                                   | Comedy,Drama,Family        |    6.4 |
| The Departed                                               | Crime,Drama,Thriller       |    8.5 |
| Mr. Brooks                                                 | Crime,Drama,Thriller       |    7.3 |
| No Country for Old Men                                     | Crime,Drama,Thriller       |    8.1 |
| Law Abiding Citizen                                        | Crime,Drama,Thriller       |    7.4 |
| The Town                                                   | Crime,Drama,Thriller       |    7.6 |
| The Place Beyond the Pines                                 | Crime,Drama,Thriller       |    7.3 |
| End of Watch                                               | Crime,Drama,Thriller       |    7.7 |
| Nightcrawler                                               | Crime,Drama,Thriller       |    7.9 |
| Hell or High Water                                         | Crime,Drama,Thriller       |    7.7 |
| The Hobbit: An Unexpected Journey                          | Adventure,Fantasy          |    7.9 |
| The Hobbit: The Desolation of Smaug                        | Adventure,Fantasy          |    7.9 |
| Captain Phillips                                           | Biography,Drama,Thriller   |    7.8 |
| The Imitation Game                                         | Biography,Drama,Thriller   |    8.1 |
| The A-Team                                                 | Action,Adventure,Comedy    |    6.8 |
| Men in Black 3                                             | Action,Adventure,Comedy    |    6.8 |
| Kingsman: The Secret Service                               | Action,Adventure,Comedy    |    7.7 |
| The Man from U.N.C.L.E.                                    | Action,Adventure,Comedy    |    7.3 |
| Ant-Man                                                    | Action,Adventure,Comedy    |    7.3 |
| Turbo Kid                                                  | Action,Adventure,Comedy    |    6.7 |
| Deadpool                                                   | Action,Adventure,Comedy    |      8 |
| Safe Haven                                                 | Drama,Romance,Thriller     |    6.7 |
| Paul                                                       | Adventure,Comedy,Sci-Fi    |      7 |
| Goksung                                                    | Drama,Fantasy,Horror       |    7.5 |
| Passengers                                                 | Adventure,Drama,Romance    |      7 |
| Lucky Number Slevin                                        | Crime,Drama,Mystery        |    7.8 |
| Inside Man                                                 | Crime,Drama,Mystery        |    7.6 |
| Fracture                                                   | Crime,Drama,Mystery        |    7.2 |
| Eastern Promises                                           | Crime,Drama,Mystery        |    7.7 |
| Gone Baby Gone                                             | Crime,Drama,Mystery        |    7.7 |
| The Girl with the Dragon Tattoo                            | Crime,Drama,Mystery        |    7.8 |
| La migliore offerta                                        | Crime,Drama,Mystery        |    7.8 |
| Prisoners                                                  | Crime,Drama,Mystery        |    8.1 |
| Gone Girl                                                  | Crime,Drama,Mystery        |    8.1 |
| The Hateful Eight                                          | Crime,Drama,Mystery        |    7.8 |
| Casino Royale                                              | Action,Adventure,Thriller  |      8 |
| Live Free or Die Hard                                      | Action,Adventure,Thriller  |    7.2 |
| Mission: Impossible - Ghost Protocol                       | Action,Adventure,Thriller  |    7.4 |
| Skyfall                                                    | Action,Adventure,Thriller  |    7.8 |
| Mission: Impossible - Rogue Nation                         | Action,Adventure,Thriller  |    7.4 |
| In Bruges                                                  | Comedy,Crime,Drama         |    7.9 |
| Dope                                                       | Comedy,Crime,Drama         |    7.3 |
| War Dogs                                                   | Comedy,Crime,Drama         |    7.1 |
| Children of Men                                            | Drama,Sci-Fi,Thriller      |    7.9 |
| Gravity                                                    | Drama,Sci-Fi,Thriller      |    7.8 |
| Sing Street                                                | Comedy,Drama,Music         |      8 |
| La La Land                                                 | Comedy,Drama,Music         |    8.3 |
| Hugo                                                       | Adventure,Drama,Family     |    7.5 |
| The Jungle Book                                            | Adventure,Drama,Family     |    7.5 |
| The Bourne Ultimatum                                       | Action,Mystery,Thriller    |    8.1 |
| Ted                                                        | Comedy,Fantasy             |      7 |
| Sinister                                                   | Horror,Mystery             |    6.8 |
| It Follows                                                 | Horror,Mystery             |    6.9 |
| The VVitch: A New-England Folktale                         | Horror,Mystery             |    6.8 |
| Cloud Atlas                                                | Drama,Sci-Fi               |    7.5 |
| Fantastic Mr. Fox                                          | Animation,Adventure,Comedy |    7.8 |
| Up                                                         | Animation,Adventure,Comedy |    8.3 |
| Tangled                                                    | Animation,Adventure,Comedy |    7.8 |
| Toy Story 3                                                | Animation,Adventure,Comedy |    8.3 |
| Despicable Me                                              | Animation,Adventure,Comedy |    7.7 |
| Wreck-It Ralph                                             | Animation,Adventure,Comedy |    7.8 |
| Frozen                                                     | Animation,Adventure,Comedy |    7.5 |
| Monsters University                                        | Animation,Adventure,Comedy |    7.3 |
| Despicable Me 2                                            | Animation,Adventure,Comedy |    7.4 |
| The Book of Life                                           | Animation,Adventure,Comedy |    7.3 |
| Inside Out                                                 | Animation,Adventure,Comedy |    8.2 |
| Zootopia                                                   | Animation,Adventure,Comedy |    8.1 |
| Finding Dory                                               | Animation,Adventure,Comedy |    7.4 |
| Moana                                                      | Animation,Adventure,Comedy |    7.7 |
| Jack Reacher                                               | Action,Crime,Mystery       |      7 |
| The Lives of Others                                        | Drama,Thriller             |    8.5 |
| Black Swan                                                 | Drama,Thriller             |      8 |
| The Skin I Live In                                         | Drama,Thriller             |    7.6 |
| The imposible                                              | Drama,Thriller             |    7.6 |
| Nocturnal Animals                                          | Drama,Thriller             |    7.5 |
| Forushande                                                 | Drama,Thriller             |      8 |
| The Blind Side                                             | Biography,Drama,Sport      |    7.7 |
| Moneyball                                                  | Biography,Drama,Sport      |    7.6 |
|                                                         42 | Biography,Drama,Sport      |    7.5 |
| Queen of Katwe                                             | Biography,Drama,Sport      |    7.4 |
| The Hills Have Eyes                                        | Horror                     |    6.4 |
| The Mist                                                   | Horror                     |    7.2 |
| The Cabin in the Woods                                     | Horror                     |      7 |
| Lights Out                                                 | Horror                     |    6.4 |
| Final Destination 5                                        | Horror,Thriller            |    5.9 |
| Mama                                                       | Horror,Thriller            |    6.2 |
| Split                                                      | Horror,Thriller            |    7.3 |
| Ouija: Origin of Evil                                      | Horror,Thriller            |    6.1 |
| The Neon Demon                                             | Horror,Thriller            |    6.2 |
|                                                            |                            |        |

