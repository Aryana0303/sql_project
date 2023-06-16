# Movie_Database_Analysis
## Questions and Answers

**Collaborators**: Aryana Sharma, Arshiya Mahajan

#### What were the top 5 highest-rated movies from 2006-16?

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


#### Do the Directors and the Cast have an impact on movie ratings?
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

#### Do votes and ratings have a correlation?

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

#### Retrieve the directors whose movies have consistently high ratings (all movies have a rating above 8).

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

Conclusion: We can see that Christopher Nolan, Florian Henckel von Donnersmarck, Aamir Khan, Sean Penn, Juan José Campanella are among the highest rating movies of all times.

#### Retrieve the movies that have a rating higher than the average rating of all movies in the same genre and year.

````sql
SELECT Title, Genre, Year, Rating
FROM movies.movie_ratings
WHERE Rating > (
  SELECT AVG(Rating)
  FROM movies.movie_ratings
  WHERE genre = Genre AND year = Year
);
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
| August Rush                                                   | Drama,Music                | 2007 |    7.5 |   |
| Freedom Writers                                               | Biography,Crime,Drama      | 2007 |    7.5 |   |
| Ratatouille                                                   | Animation,Comedy,Family    | 2007 |      8 |   |
| Taare Zameen Par                                              | Drama,Family,Music         | 2007 |    8.5 |   |
| Sunshine                                                      | Adventure,Sci-Fi,Thriller  | 2007 |    7.3 |   |
| Mr. Brooks                                                    | Crime,Drama,Thriller       | 2007 |    7.3 |   |
| American Gangster                                             | Biography,Crime,Drama      | 2007 |    7.8 |   |
| No Country for Old Men                                        | Crime,Drama,Thriller       | 2007 |    8.1 |   |
| Into the Wild                                                 | Adventure,Biography,Drama  | 2007 |    8.1 |   |
| There Will Be Blood                                           | Drama,History              | 2007 |    8.1 |   |
| The Bourne Ultimatum                                          | Action,Mystery,Thriller    | 2007 |    8.1 |   |
| Pirates of the Caribbean: At World's End                      | Action,Adventure,Fantasy   | 2007 |    7.1 |   |
| Transformers                                                  | Action,Adventure,Sci-Fi    | 2007 |    7.1 |   |
| Enchanted                                                     | Animation,Comedy,Family    | 2007 |    7.1 |   |
| Superbad                                                      | Comedy                     | 2007 |    7.6 |   |
| Ocean's Thirteen                                              | Crime,Thriller             | 2007 |    6.9 |   |
| Sweeney Todd: The Demon Barber of Fleet Street                | Drama,Horror,Musical       | 2007 |    7.4 |   |
| Across the Universe                                           | Drama,Fantasy,Musical      | 2007 |    7.4 |   |
| Hot Fuzz                                                      | Action,Comedy,Mystery      | 2007 |    7.9 |   |
| I Am Legend                                                   | Drama,Horror,Sci-Fi        | 2007 |    7.2 |   |
| Shooter                                                       | Action,Crime,Drama         | 2007 |    7.2 |   |
| The Mist                                                      | Horror                     | 2007 |    7.2 |   |
| Live Free or Die Hard                                         | Action,Adventure,Thriller  | 2007 |    7.2 |   |
| Fracture                                                      | Crime,Drama,Mystery        | 2007 |    7.2 |   |
| Bridge to Terabithia                                          | Adventure,Drama,Family     | 2007 |    7.2 |   |
| Zodiac                                                        | Crime,Drama,History        | 2007 |    7.7 |   |
| Stardust                                                      | Adventure,Family,Fantasy   | 2007 |    7.7 |   |
| Eastern Promises                                              | Crime,Drama,Mystery        | 2007 |    7.7 |   |
| Gone Baby Gone                                                | Crime,Drama,Mystery        | 2007 |    7.7 |   |
| Tropic Thunder                                                | Action,Comedy              | 2008 |      7 |   |
| Cloverfield                                                   | Action,Horror,Sci-Fi       | 2008 |      7 |   |
| Hellboy II: The Golden Army                                   | Action,Adventure,Fantasy   | 2008 |      7 |   |
| Pineapple Express                                             | Action,Comedy,Crime        | 2008 |      7 |   |
| Slumdog Millionaire                                           | Drama                      | 2008 |      8 |   |
| The Dark Knight                                               | Action,Crime,Drama         | 2008 |      9 |   |
| RocknRolla                                                    | Action,Crime,Thriller      | 2008 |    7.3 |   |
| Revolutionary Road                                            | Drama,Romance              | 2008 |    7.3 |   |
| Taken                                                         | Action,Thriller            | 2008 |    7.8 |   |
| The Curious Case of Benjamin Button                           | Drama,Fantasy,Romance      | 2008 |    7.8 |   |
| The Boy in the Striped Pyjamas                                | Drama,War                  | 2008 |    7.8 |   |
| Changeling                                                    | Biography,Drama,Mystery    | 2008 |    7.8 |   |
| Body of Lies                                                  | Action,Drama,Romance       | 2008 |    7.1 |   |
| Vicky Cristina Barcelona                                      | Drama,Romance              | 2008 |    7.1 |   |
| Rambo                                                         | Action,Thriller,War        | 2008 |    7.1 |   |
| The Hurt Locker                                               | Drama,History,Thriller     | 2008 |    7.6 |   |
| Hunger                                                        | Biography,Drama            | 2008 |    7.6 |   |
| Kung Fu Panda                                                 | Animation,Action,Adventure | 2008 |    7.6 |   |
| Step Brothers                                                 | Comedy                     | 2008 |    6.9 |   |
| Iron Man                                                      | Action,Adventure,Sci-Fi    | 2008 |    7.9 |   |
| In Bruges                                                     | Comedy,Crime,Drama         | 2008 |    7.9 |   |
| Forgetting Sarah Marshall                                     | Comedy,Drama,Romance       | 2008 |    7.2 |   |
| Seven Pounds                                                  | Drama,Romance              | 2008 |    7.7 |   |
| Public Enemies                                                | Biography,Crime,Drama      | 2009 |      7 |   |
| Orphan                                                        | Horror,Mystery,Thriller    | 2009 |      7 |   |
| Harry Potter and the Half-Blood Prince                        | Adventure,Family,Fantasy   | 2009 |    7.5 |   |
| Star Trek                                                     | Action,Adventure,Sci-Fi    | 2009 |      8 |   |
| District 9                                                    | Action,Sci-Fi,Thriller     | 2009 |      8 |   |
| Kynodontas                                                    | Drama,Thriller             | 2009 |    7.3 |   |
| Precious                                                      | Drama                      | 2009 |    7.3 |   |
| Avatar                                                        | Action,Adventure,Fantasy   | 2009 |    7.8 |   |
| The Hangover                                                  | Comedy                     | 2009 |    7.8 |   |
| Män som hatar kvinnor                                         | Drama,Mystery,Thriller     | 2009 |    7.8 |   |
| Fantastic Mr. Fox                                             | Animation,Adventure,Comedy | 2009 |    7.8 |   |
| The Princess and the Frog                                     | Animation,Adventure,Comedy | 2009 |    7.1 |   |
| Watchmen                                                      | Action,Drama,Mystery       | 2009 |    7.6 |   |
| Sherlock Holmes                                               | Action,Adventure,Crime     | 2009 |    7.6 |   |
| El secreto de sus ojos                                        | Drama,Mystery,Romance      | 2009 |    8.2 |   |
| Law Abiding Citizen                                           | Crime,Drama,Thriller       | 2009 |    7.4 |   |
| Moon                                                          | Drama,Mystery,Sci-Fi       | 2009 |    7.9 |   |
| Inglourious Basterds                                          | Adventure,Drama,War        | 2009 |    8.3 |   |
| Up                                                            | Animation,Adventure,Comedy | 2009 |    8.3 |   |
| The Blind Side                                                | Biography,Drama,Sport      | 2009 |    7.7 |   |
| Zombieland                                                    | Adventure,Comedy,Horror    | 2009 |    7.7 |   |
| Coraline                                                      | Animation,Family,Fantasy   | 2009 |    7.7 |   |
| (500) Days of Summer                                          | Comedy,Drama,Romance       | 2009 |    7.7 |   |
| 3 Idiots                                                      | Comedy,Drama               | 2009 |    8.4 |   |
| Iron Man 2                                                    | Action,Adventure,Sci-Fi    | 2010 |      7 |   |
| Trust                                                         | Crime,Drama,Thriller       | 2010 |      7 |   |
| Scott Pilgrim vs. the World                                   | Action,Comedy,Fantasy      | 2010 |    7.5 |   |
| Black Swan                                                    | Drama,Thriller             | 2010 |      8 |   |
| The King's Speech                                             | Biography,Drama            | 2010 |      8 |   |
| Megamind                                                      | Animation,Action,Comedy    | 2010 |    7.3 |   |
| Tangled                                                       | Animation,Adventure,Comedy | 2010 |    7.8 |   |
| The Fighter                                                   | Action,Biography,Drama     | 2010 |    7.8 |   |
| Shutter Island                                                | Mystery,Thriller           | 2010 |    8.1 |   |
| How to Train Your Dragon                                      | Animation,Action,Adventure | 2010 |    8.1 |   |
| Easy A                                                        | Comedy,Drama,Romance       | 2010 |    7.1 |   |
| RED                                                           | Action,Comedy,Crime        | 2010 |    7.1 |   |
| The Town                                                      | Crime,Drama,Thriller       | 2010 |    7.6 |   |
| True Grit                                                     | Adventure,Drama,Western    | 2010 |    7.6 |   |
| 127 Hours                                                     | Adventure,Biography,Drama  | 2010 |    7.6 |   |
| Incendies                                                     | Drama,Mystery,War          | 2010 |    8.2 |   |
| The Book of Eli                                               | Action,Adventure,Drama     | 2010 |    6.9 |   |
| Blue Valentine                                                | Drama,Romance              | 2010 |    7.4 |   |
| Toy Story 3                                                   | Animation,Adventure,Comedy | 2010 |    8.3 |   |
| Inception                                                     | Action,Adventure,Sci-Fi    | 2010 |    8.8 |   |
| The Ghost Writer                                              | Mystery,Thriller           | 2010 |    7.2 |   |
| Let Me In                                                     | Drama,Horror,Mystery       | 2010 |    7.2 |   |
| Remember Me                                                   | Drama,Romance              | 2010 |    7.2 |   |
| Kick-Ass                                                      | Action,Comedy              | 2010 |    7.7 |   |
| The Social Network                                            | Biography,Drama            | 2010 |    7.7 |   |
| Despicable Me                                                 | Animation,Adventure,Comedy | 2010 |    7.7 |   |
| Harry Potter and the Deathly Hallows: Part 1                  | Adventure,Family,Fantasy   | 2010 |    7.7 |   |
| Thor                                                          | Action,Adventure,Fantasy   | 2011 |      7 |   |
| Paul                                                          | Adventure,Comedy,Sci-Fi    | 2011 |      7 |   |
| One Day                                                       | Drama,Romance              | 2011 |      7 |   |
| Sherlock Holmes: A Game of Shadows                            | Action,Adventure,Crime     | 2011 |    7.5 |   |
| Source Code                                                   | Mystery,Romance,Sci-Fi     | 2011 |    7.5 |   |
| We Need to Talk About Kevin                                   | Drama,Mystery,Thriller     | 2011 |    7.5 |   |
| Hugo                                                          | Adventure,Drama,Family     | 2011 |    7.5 |   |
| Fast Five                                                     | Action,Crime,Thriller      | 2011 |    7.3 |   |
| The Descendants                                               | Comedy,Drama               | 2011 |    7.3 |   |
| Drive                                                         | Crime,Drama                | 2011 |    7.8 |   |
| X: First Class                                                | Action,Adventure,Sci-Fi    | 2011 |    7.8 |   |
| The Girl with the Dragon Tattoo                               | Crime,Drama,Mystery        | 2011 |    7.8 |   |
| The Help                                                      | Drama                      | 2011 |    8.1 |   |
| Harry Potter and the Deathly Hallows: Part 2                  | Adventure,Drama,Fantasy    | 2011 |    8.1 |   |
| The Intouchables                                              | Biography,Comedy,Drama     | 2011 |    8.6 |   |
| Super 8                                                       | Mystery,Sci-Fi,Thriller    | 2011 |    7.1 |   |
| Tinker Tailor Soldier Spy                                     | Drama,Mystery,Thriller     | 2011 |    7.1 |   |
| Melancholia                                                   | Drama                      | 2011 |    7.1 |   |
| Real Steel                                                    | Action,Drama,Family        | 2011 |    7.1 |   |
| Rise of the Planet of the Apes                                | Action,Drama,Sci-Fi        | 2011 |    7.6 |   |
| Moneyball                                                     | Biography,Drama,Sport      | 2011 |    7.6 |   |
| The Skin I Live In                                            | Drama,Thriller             | 2011 |    7.6 |   |
| Warrior                                                       | Action,Drama,Sport         | 2011 |    8.2 |   |
| Captain America: The First Avenger                            | Action,Adventure,Sci-Fi    | 2011 |    6.9 |   |
| Horrible Bosses                                               | Comedy,Crime               | 2011 |    6.9 |   |
| Unknown                                                       | Action,Mystery,Thriller    | 2011 |    6.9 |   |
| Rio                                                           | Animation,Adventure,Comedy | 2011 |    6.9 |   |
| Crazy, Stupid, Love.                                          | Comedy,Drama,Romance       | 2011 |    7.4 |   |
| Mission: Impossible - Ghost Protocol                          | Action,Adventure,Thriller  | 2011 |    7.4 |   |
| Limitless                                                     | Mystery,Sci-Fi,Thriller    | 2011 |    7.4 |   |
| Jane Eyre                                                     | Drama,Romance              | 2011 |    7.4 |   |
| Shame                                                         | Drama                      | 2011 |    7.2 |   |
| Midnight in Paris                                             | Comedy,Fantasy,Romance     | 2011 |    7.7 |   |
| 50/50                                                         | Comedy,Drama,Romance       | 2011 |    7.7 |   |
| Prometheus                                                    | Adventure,Mystery,Sci-Fi   | 2012 |      7 |   |
| The Cabin in the Woods                                        | Horror                     | 2012 |      7 |   |
| The Amazing Spider-Man                                        | Action,Adventure           | 2012 |      7 |   |
| Jack Reacher                                                  | Action,Crime,Mystery       | 2012 |      7 |   |
| Ted                                                           | Comedy,Fantasy             | 2012 |      7 |   |
| Cloud Atlas                                                   | Drama,Sci-Fi               | 2012 |    7.5 |   |
| The Perks of Being a Wallflower                               | Drama,Romance              | 2012 |      8 |   |
| The Dark Knight Rises                                         | Action,Thriller            | 2012 |    8.5 |   |
| The Place Beyond the Pines                                    | Crime,Drama,Thriller       | 2012 |    7.3 |   |
| Lawless                                                       | Crime,Drama                | 2012 |    7.3 |   |
| Flight                                                        | Drama,Thriller             | 2012 |    7.3 |   |
| Skyfall                                                       | Action,Adventure,Thriller  | 2012 |    7.8 |   |
| Silver Linings Playbook                                       | Comedy,Drama,Romance       | 2012 |    7.8 |   |
| Moonrise Kingdom                                              | Adventure,Comedy,Drama     | 2012 |    7.8 |   |
| Wreck-It Ralph                                                | Animation,Adventure,Comedy | 2012 |    7.8 |   |
| The Avengers                                                  | Action,Sci-Fi              | 2012 |    8.1 |   |
| Dredd                                                         | Action,Sci-Fi              | 2012 |    7.1 |   |
| Les Misérables                                                | Drama,Musical,Romance      | 2012 |    7.6 |   |
| The imposible                                                 | Drama,Thriller             | 2012 |    7.6 |   |
| The First Time                                                | Comedy,Drama,Romance       | 2012 |    6.9 |   |
| Lincoln                                                       | Biography,Drama,History    | 2012 |    7.4 |   |
| Looper                                                        | Action,Crime,Drama         | 2012 |    7.4 |   |
| Zero Dark Thirty                                              | Drama,History,Thriller     | 2012 |    7.4 |   |
| The Hobbit: An Unexpected Journey                             | Adventure,Fantasy          | 2012 |    7.9 |   |
| Life of Pi                                                    | Adventure,Drama,Fantasy    | 2012 |    7.9 |   |
| Jagten                                                        | Drama                      | 2012 |    8.3 |   |
| The Hunger Games                                              | Adventure,Sci-Fi,Thriller  | 2012 |    7.2 |   |
| 21 Jump Street                                                | Action,Comedy,Crime        | 2012 |    7.2 |   |
| Pitch Perfect                                                 | Comedy,Music,Romance       | 2012 |    7.2 |   |
| Brave                                                         | Animation,Adventure,Comedy | 2012 |    7.2 |   |
| Seven Psychopaths                                             | Comedy,Crime               | 2012 |    7.2 |   |
| Argo                                                          | Biography,Drama,History    | 2012 |    7.7 |   |
| End of Watch                                                  | Crime,Drama,Thriller       | 2012 |    7.7 |   |
| Django Unchained                                              | Drama,Western              | 2012 |    8.4 |   |
| Pacific Rim                                                   | Action,Adventure,Sci-Fi    | 2013 |      7 |   |
| Thor: The Dark World                                          | Action,Adventure,Fantasy   | 2013 |      7 |   |
| We're the Millers                                             | Comedy,Crime               | 2013 |      7 |   |
| Nymphomaniac: Vol. I                                          | Drama                      | 2013 |      7 |   |
| Oblivion                                                      | Action,Adventure,Mystery   | 2013 |      7 |   |
| Snowpiercer                                                   | Action,Drama,Sci-Fi        | 2013 |      7 |   |
| World War Z                                                   | Action,Adventure,Horror    | 2013 |      7 |   |
| The World's End                                               | Action,Comedy,Sci-Fi       | 2013 |      7 |   |
| Trance                                                        | Crime,Drama,Mystery        | 2013 |      7 |   |
| Frozen                                                        | Animation,Adventure,Comedy | 2013 |    7.5 |   |
| The Conjuring                                                 | Horror,Mystery,Thriller    | 2013 |    7.5 |   |
| Lone Survivor                                                 | Action,Biography,Drama     | 2013 |    7.5 |   |
|                                                            42 | Biography,Drama,Sport      | 2013 |    7.5 |   |
| Saving Mr. Banks                                              | Biography,Comedy,Drama     | 2013 |    7.5 |   |
| Her                                                           | Drama,Romance,Sci-Fi       | 2013 |      8 |   |
| Dallas Buyers Club                                            | Biography,Drama            | 2013 |      8 |   |
| The Great Gatsby                                              | Drama,Romance              | 2013 |    7.3 |   |
| Now You See Me                                                | Crime,Mystery,Thriller     | 2013 |    7.3 |   |
| American Hustle                                               | Crime,Drama                | 2013 |    7.3 |   |
| Monsters University                                           | Animation,Adventure,Comedy | 2013 |    7.3 |   |
| The Secret Life of Walter Mitty                               | Adventure,Comedy,Drama     | 2013 |    7.3 |   |
| Blue Jasmine                                                  | Drama                      | 2013 |    7.3 |   |
| La vie d'Adèle                                                | Drama,Romance              | 2013 |    7.8 |   |
| About Time                                                    | Comedy,Drama,Fantasy       | 2013 |    7.8 |   |
| Star Trek Into Darkness                                       | Action,Adventure,Sci-Fi    | 2013 |    7.8 |   |
| Gravity                                                       | Drama,Sci-Fi,Thriller      | 2013 |    7.8 |   |
| Captain Phillips                                              | Biography,Drama,Thriller   | 2013 |    7.8 |   |
| La migliore offerta                                           | Crime,Drama,Mystery        | 2013 |    7.8 |   |
| Prisoners                                                     | Crime,Drama,Mystery        | 2013 |    8.1 |   |
| 12 Years a Slave                                              | Biography,Drama,History    | 2013 |    8.1 |   |
| Rush                                                          | Action,Biography,Drama     | 2013 |    8.1 |   |
| Furious 6                                                     | Action,Crime,Thriller      | 2013 |    7.1 |   |
| Man of Steel                                                  | Action,Adventure,Fantasy   | 2013 |    7.1 |   |
| The Spectacular Now                                           | Comedy,Drama,Romance       | 2013 |    7.1 |   |
| Locke                                                         | Drama                      | 2013 |    7.1 |   |
| The Hunger Games: Catching Fire                               | Action,Adventure,Mystery   | 2013 |    7.6 |   |
| The Wolf of Wall Street                                       | Biography,Comedy,Crime     | 2013 |    8.2 |   |
| Enemy                                                         | Mystery,Thriller           | 2013 |    6.9 |   |
| Warm Bodies                                                   | Comedy,Horror,Romance      | 2013 |    6.9 |   |
| Despicable Me 2                                               | Animation,Adventure,Comedy | 2013 |    7.4 |   |
| Begin Again                                                   | Drama,Music                | 2013 |    7.4 |   |
| The Hobbit: The Desolation of Smaug                           | Adventure,Fantasy          | 2013 |    7.9 |   |
| Iron Man Three                                                | Action,Adventure,Sci-Fi    | 2013 |    7.2 |   |
| Coherence                                                     | Mystery,Sci-Fi,Thriller    | 2013 |    7.2 |   |
| The Kings of Summer                                           | Adventure,Comedy,Drama     | 2013 |    7.2 |   |
| Maleficent                                                    | Action,Adventure,Family    | 2014 |      7 |   |
| X-Men: Days of Future Past                                    | Action,Adventure,Sci-Fi    | 2014 |      8 |   |
| Whiplash                                                      | Drama,Music                | 2014 |    8.5 |   |
| American Sniper                                               | Action,Biography,Drama     | 2014 |    7.3 |   |
| I Origins                                                     | Drama,Romance,Sci-Fi       | 2014 |    7.3 |   |
| The Book of Life                                              | Animation,Adventure,Comedy | 2014 |    7.3 |   |
| Chef                                                          | Comedy,Drama               | 2014 |    7.3 |   |
| Captain America: The Winter Soldier                           | Action,Adventure,Sci-Fi    | 2014 |    7.8 |   |
| Birdman or (The Unexpected Virtue of Ignorance)               | Comedy,Drama,Romance       | 2014 |    7.8 |   |
| The Fault in Our Stars                                        | Drama,Romance              | 2014 |    7.8 |   |
| The Lego Movie                                                | Animation,Action,Adventure | 2014 |    7.8 |   |
| Big Hero 6                                                    | Animation,Action,Adventure | 2014 |    7.8 |   |
| Guardians of the Galaxy                                       | Action,Adventure,Sci-Fi    | 2014 |    8.1 |   |
| Gone Girl                                                     | Crime,Drama,Mystery        | 2014 |    8.1 |   |
| The Imitation Game                                            | Biography,Drama,Thriller   | 2014 |    8.1 |   |
| The Grand Budapest Hotel                                      | Adventure,Comedy,Drama     | 2014 |    8.1 |   |
| Mommy                                                         | Drama                      | 2014 |    8.1 |   |
| Relatos salvajes                                              | Comedy,Drama,Thriller      | 2014 |    8.1 |   |
| Interstellar                                                  | Adventure,Drama,Sci-Fi     | 2014 |    8.6 |   |
| 22 Jump Street                                                | Action,Comedy,Crime        | 2014 |    7.1 |   |
| The Drop                                                      | Crime,Drama,Mystery        | 2014 |    7.1 |   |
| Wild                                                          | Adventure,Biography,Drama  | 2014 |    7.1 |   |
| Dawn of the Planet of the Apes                                | Action,Adventure,Drama     | 2014 |    7.6 |   |
| Fury                                                          | Action,Drama,War           | 2014 |    7.6 |   |
| What We Do in the Shadows                                     | Comedy,Fantasy,Horror      | 2014 |    7.6 |   |
| PK                                                            | Comedy,Drama,Romance       | 2014 |    8.2 |   |
| It Follows                                                    | Horror,Mystery             | 2014 |    6.9 |   |
| Before We Go                                                  | Comedy,Drama,Romance       | 2014 |    6.9 |   |
| The Hobbit: The Battle of the Five Armies                     | Adventure,Fantasy          | 2014 |    7.4 |   |
| The Judge                                                     | Crime,Drama                | 2014 |    7.4 |   |
| Nightcrawler                                                  | Crime,Drama,Thriller       | 2014 |    7.9 |   |
| Edge of Tomorrow                                              | Action,Adventure,Sci-Fi    | 2014 |    7.9 |   |
| Boyhood                                                       | Drama                      | 2014 |    7.9 |   |
| How to Train Your Dragon 2                                    | Animation,Action,Adventure | 2014 |    7.9 |   |
| John Wick                                                     | Action,Crime,Thriller      | 2014 |    7.2 |   |
| The Equalizer                                                 | Action,Crime,Thriller      | 2014 |    7.2 |   |
| Unbroken                                                      | Biography,Drama,Sport      | 2014 |    7.2 |   |
| Love, Rosie                                                   | Comedy,Romance             | 2014 |    7.2 |   |
| Kingsman: The Secret Service                                  | Action,Adventure,Comedy    | 2014 |    7.7 |   |
| Ex Machina                                                    | Drama,Mystery,Sci-Fi       | 2014 |    7.7 |   |
| The Theory of Everything                                      | Biography,Drama,Romance    | 2014 |    7.7 |   |
| Jurassic World                                                | Action,Adventure,Sci-Fi    | 2015 |      7 |   |
| Legend                                                        | Biography,Crime,Drama      | 2015 |      7 |   |
| Cinderella                                                    | Drama,Family,Fantasy       | 2015 |      7 |   |
| The Danish Girl                                               | Biography,Drama,Romance    | 2015 |      7 |   |
| Green Room                                                    | Crime,Horror,Thriller      | 2015 |      7 |   |
| Demolition                                                    | Comedy,Drama               | 2015 |      7 |   |
| Brooklyn                                                      | Drama,Romance              | 2015 |    7.5 |   |
| The Martian                                                   | Adventure,Drama,Sci-Fi     | 2015 |      8 |   |
| The Revenant                                                  | Adventure,Drama,Thriller   | 2015 |      8 |   |
| The Man from U.N.C.L.E.                                       | Action,Adventure,Comedy    | 2015 |    7.3 |   |
| Woman in Gold                                                 | Biography,Drama,History    | 2015 |    7.3 |   |
| Ant-Man                                                       | Action,Adventure,Comedy    | 2015 |    7.3 |   |
| Youth                                                         | Comedy,Drama,Music         | 2015 |    7.3 |   |
| Dope                                                          | Comedy,Crime,Drama         | 2015 |    7.3 |   |
| Eye in the Sky                                                | Drama,Thriller,War         | 2015 |    7.3 |   |
| The Hateful Eight                                             | Crime,Drama,Mystery        | 2015 |    7.8 |   |
| The Big Short                                                 | Biography,Comedy,Drama     | 2015 |    7.8 |   |
| Me and Earl and the Dying Girl                                | Comedy,Drama               | 2015 |    7.8 |   |
| Star Wars: Episode VII - The Force Awakens                    | Action,Adventure,Fantasy   | 2015 |    8.1 |   |
| Mad Max: Fury Road                                            | Action,Adventure,Sci-Fi    | 2015 |    8.1 |   |
| Spotlight                                                     | Crime,Drama,History        | 2015 |    8.1 |   |
| The Lobster                                                   | Comedy,Drama,Romance       | 2015 |    7.1 |   |
| Spy                                                           | Action,Comedy,Crime        | 2015 |    7.1 |   |
| The Dressmaker                                                | Comedy,Drama               | 2015 |    7.1 |   |
| Everest                                                       | Action,Adventure,Drama     | 2015 |    7.1 |   |
| The Longest Ride                                              | Drama,Romance              | 2015 |    7.1 |   |
| Bone Tomahawk                                                 | Adventure,Drama,Horror     | 2015 |    7.1 |   |
| The Gift                                                      | Mystery,Thriller           | 2015 |    7.1 |   |
| The Intern                                                    | Comedy,Drama               | 2015 |    7.1 |   |
| Sicario                                                       | Action,Crime,Drama         | 2015 |    7.6 |   |
| Creed                                                         | Drama,Sport                | 2015 |    7.6 |   |
| Bridge of Spies                                               | Drama,History,Thriller     | 2015 |    7.6 |   |
| Room                                                          | Drama                      | 2015 |    8.2 |   |
| Inside Out                                                    | Animation,Adventure,Comedy | 2015 |    8.2 |   |
| Black Mass                                                    | Biography,Crime,Drama      | 2015 |    6.9 |   |
| Chappie                                                       | Action,Crime,Drama         | 2015 |    6.9 |   |
| In the Heart of the Sea                                       | Action,Adventure,Biography | 2015 |    6.9 |   |
| The Stanford Prison Experiment                                | Biography,Drama,History    | 2015 |    6.9 |   |
| Avengers: Age of Ultron                                       | Action,Adventure,Sci-Fi    | 2015 |    7.4 |   |
| Mission: Impossible - Rogue Nation                            | Action,Adventure,Thriller  | 2015 |    7.4 |   |
| Southpaw                                                      | Drama,Sport                | 2015 |    7.4 |   |
| Straight Outta Compton                                        | Biography,Drama,History    | 2015 |    7.9 |   |
| Furious Seven                                                 | Action,Crime,Thriller      | 2015 |    7.2 |   |
| Steve Jobs                                                    | Biography,Drama            | 2015 |    7.2 |   |
| The Age of Adaline                                            | Drama,Fantasy,Romance      | 2015 |    7.2 |   |
| Carol                                                         | Drama,Romance              | 2015 |    7.2 |   |
| En man som heter Ove                                          | Comedy,Drama               | 2015 |    7.7 |   |
| Passengers                                                    | Adventure,Drama,Romance    | 2016 |      7 |   |
| Their Finest                                                  | Comedy,Drama,Romance       | 2016 |      7 |   |
| Warcraft                                                      | Action,Adventure,Fantasy   | 2016 |      7 |   |
| Free Fire                                                     | Action,Comedy,Crime        | 2016 |      7 |   |
| American Honey                                                | Drama                      | 2016 |      7 |   |
| Everybody Wants Some!!                                        | Comedy                     | 2016 |      7 |   |
| Christine                                                     | Biography,Drama            | 2016 |      7 |   |
| Miracles from Heaven                                          | Biography,Drama,Family     | 2016 |      7 |   |
| Fantastic Beasts and Where to Find Them                       | Adventure,Family,Fantasy   | 2016 |    7.5 |   |
| Nocturnal Animals                                             | Drama,Thriller             | 2016 |    7.5 |   |
| Moonlight                                                     | Drama                      | 2016 |    7.5 |   |
| Sully                                                         | Biography,Drama            | 2016 |    7.5 |   |
| Wakefield                                                     | Drama                      | 2016 |    7.5 |   |
| A Monster Calls                                               | Drama,Fantasy              | 2016 |    7.5 |   |
| The Jungle Book                                               | Adventure,Drama,Family     | 2016 |    7.5 |   |
| Raw (II)                                                      | Drama,Horror               | 2016 |    7.5 |   |
| Paterson                                                      | Comedy,Drama,Romance       | 2016 |    7.5 |   |
| Busanhaeng                                                    | Action,Drama,Horror        | 2016 |    7.5 |   |
| Frantz                                                        | Drama,History,War          | 2016 |    7.5 |   |
| Bacalaureat                                                   | Crime,Drama                | 2016 |    7.5 |   |
| Goksung                                                       | Drama,Fantasy,Horror       | 2016 |    7.5 |   |
| Arrival                                                       | Drama,Mystery,Sci-Fi       | 2016 |      8 |   |
| Deadpool                                                      | Action,Adventure,Comedy    | 2016 |      8 |   |
| Forushande                                                    | Drama,Thriller             | 2016 |      8 |   |
| Sing Street                                                   | Comedy,Drama,Music         | 2016 |      8 |   |
| Split                                                         | Horror,Thriller            | 2016 |    7.3 |   |
| Miss Sloane                                                   | Drama,Thriller             | 2016 |    7.3 |   |
| Silence                                                       | Adventure,Drama,History    | 2016 |    7.3 |   |
| Fences                                                        | Drama                      | 2016 |    7.3 |   |
| 13 Hours                                                      | Action,Drama,History       | 2016 |    7.3 |   |
| Snowden                                                       | Biography,Drama,Thriller   | 2016 |    7.3 |   |
| Hidden Figures                                                | Biography,Drama,History    | 2016 |    7.8 |   |
| Dear Zindagi                                                  | Drama,Romance              | 2016 |    7.8 |   |
| Ma vie de Courgette                                           | Animation,Comedy,Drama     | 2016 |    7.8 |   |
| Lion                                                          | Biography,Drama            | 2016 |    8.1 |   |
| Zootopia                                                      | Animation,Adventure,Comedy | 2016 |    8.1 |   |
| Ah-ga-ssi                                                     | Drama,Mystery,Romance      | 2016 |    8.1 |   |
| Kimi no na wa                                                 | Animation,Drama,Fantasy    | 2016 |    8.6 |   |
| The Lost City of Z                                            | Action,Adventure,Biography | 2016 |    7.1 |   |
| X-Men: Apocalypse                                             | Action,Adventure,Sci-Fi    | 2016 |    7.1 |   |
| Star Trek Beyond                                              | Action,Adventure,Sci-Fi    | 2016 |    7.1 |   |
| Allied                                                        | Action,Drama,Romance       | 2016 |    7.1 |   |
| War Dogs                                                      | Comedy,Crime,Drama         | 2016 |    7.1 |   |
| Norman: The Moderate Rise and Tragic Fall of a New York Fixer | Drama,Thriller             | 2016 |    7.1 |   |
| The Infiltrator                                               | Biography,Crime,Drama      | 2016 |    7.1 |   |
| Swiss Army Man                                                | Adventure,Comedy,Drama     | 2016 |    7.1 |   |
| Loving                                                        | Biography,Drama,Romance    | 2016 |    7.1 |   |
| L'avenir                                                      | Drama                      | 2016 |    7.1 |   |
| Doctor Strange                                                | Action,Adventure,Fantasy   | 2016 |    7.6 |   |
| Toni Erdmann                                                  | Comedy,Drama               | 2016 |    7.6 |   |
| La tortue rouge                                               | Animation,Fantasy          | 2016 |    7.6 |   |
| Hacksaw Ridge                                                 | Biography,Drama,History    | 2016 |    8.2 |   |
| The Magnificent Seven                                         | Action,Adventure,Western   | 2016 |    6.9 |   |
| Storks                                                        | Animation,Adventure,Comedy | 2016 |    6.9 |   |
| Florence Foster Jenkins                                       | Biography,Comedy,Drama     | 2016 |    6.9 |   |
| Indignation                                                   | Drama,Romance              | 2016 |    6.9 |   |
| Shin Gojira                                                   | Action,Adventure,Drama     | 2016 |    6.9 |   |
| Me Before You                                                 | Drama,Romance              | 2016 |    7.4 |   |
| Patriots Day                                                  | Drama,History,Thriller     | 2016 |    7.4 |   |
| The Accountant                                                | Action,Crime,Drama         | 2016 |    7.4 |   |
| The Nice Guys                                                 | Action,Comedy,Crime        | 2016 |    7.4 |   |
| Finding Dory                                                  | Animation,Adventure,Comedy | 2016 |    7.4 |   |
| The Edge of Seventeen                                         | Comedy,Drama               | 2016 |    7.4 |   |
| The Conjuring 2                                               | Horror,Mystery,Thriller    | 2016 |    7.4 |   |
| 20th Century Women                                            | Comedy,Drama               | 2016 |    7.4 |   |
| A Street Cat Named Bob                                        | Biography,Comedy,Drama     | 2016 |    7.4 |   |
| Eddie the Eagle                                               | Biography,Comedy,Drama     | 2016 |    7.4 |   |
| Queen of Katwe                                                | Biography,Drama,Sport      | 2016 |    7.4 |   |
| Rogue One                                                     | Action,Adventure,Sci-Fi    | 2016 |    7.9 |   |
| Manchester by the Sea                                         | Drama                      | 2016 |    7.9 |   |
| Captain America: Civil War                                    | Action,Adventure,Sci-Fi    | 2016 |    7.9 |   |
| Captain Fantastic                                             | Comedy,Drama               | 2016 |    7.9 |   |
| Kubo and the Two Strings                                      | Animation,Adventure,Family | 2016 |    7.9 |   |
| Hunt for the Wilderpeople                                     | Adventure,Comedy,Drama     | 2016 |    7.9 |   |
| La La Land                                                    | Comedy,Drama,Music         | 2016 |    8.3 |   |
| Sing                                                          | Animation,Comedy,Family    | 2016 |    7.2 |   |
| The Founder                                                   | Biography,Drama,History    | 2016 |    7.2 |   |
| Don't Breathe                                                 | Crime,Horror,Thriller      | 2016 |    7.2 |   |
| Deepwater Horizon                                             | Action,Drama,Thriller      | 2016 |    7.2 |   |
| 10 Cloverfield Lane                                           | Drama,Horror,Mystery       | 2016 |    7.2 |   |
| The Light Between Oceans                                      | Drama,Romance              | 2016 |    7.2 |   |
| Anthropoid                                                    | Biography,History,Thriller | 2016 |    7.2 |   |
| A Quiet Passion                                               | Biography,Drama            | 2016 |    7.2 |   |
| Kung Fu Panda 3                                               | Animation,Action,Adventure | 2016 |    7.2 |   |
| The Age of Shadows                                            | Action,Drama,Thriller      | 2016 |    7.2 |   |
| Moana                                                         | Animation,Adventure,Comedy | 2016 |    7.7 |   |
| Hell or High Water                                            | Crime,Drama,Thriller       | 2016 |    7.7 |   |
| Mr. Church                                                    | Comedy,Drama               | 2016 |    7.7 |   |
|                                                               |                            |      |        |   |



