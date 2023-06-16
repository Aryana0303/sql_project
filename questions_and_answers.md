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
HAVING AVG(Rating) > (SELECT AVG(Rating) FROM movies.movie_ratings);
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
| Denis Villeneuve                 | Lubna Azabal, Mélissa Désormeaux-Poulin, Maxim Gaudette, Mustafa Kamel        |            8.2 |   |   |
| Gavin O'Connor                   | Tom Hardy, Nick Nolte, Joel Edgerton, Jennifer Morrison                       |            8.2 |   |   |
| Martin Scorsese                  | Leonardo DiCaprio, Jonah Hill, Margot Robbie,Matthew McConaughey              |            8.2 |   |   |
| Rajkumar Hirani                  | Aamir Khan, Anushka Sharma, Sanjay Dutt,Boman Irani                           |            8.2 |   |   |
| Lenny Abrahamson                 | Brie Larson, Jacob Tremblay, Sean Bridgers,Wendy Crewson                      |            8.2 |   |   |
| Pete Docter                      | Amy Poehler, Bill Hader, Lewis Black, Mindy Kaling                            |            8.2 |   |   |
| Mel Gibson                       | Andrew Garfield, Sam Worthington, Luke Bracey,Teresa Palmer                   |            8.2 |   |   |
| Ethan Coen                       | Tommy Lee Jones, Javier Bardem, Josh Brolin, Woody Harrelson                  |            8.1 |   |   |
| Sean Penn                        | Emile Hirsch, Vince Vaughn, Catherine Keener, Marcia Gay Harden               |            8.1 |   |   |
| Paul Thomas Anderson             | Daniel Day-Lewis, Paul Dano, Ciarán Hinds,Martin Stringer                     |            8.1 |   |   |
| Paul Greengrass                  | Matt Damon, Edgar Ramírez, Joan Allen, Julia Stiles                           |            8.1 |   |   |
| Martin Scorsese                  | Leonardo DiCaprio, Emily Mortimer, Mark Ruffalo,Ben Kingsley                  |            8.1 |   |   |
| Dean DeBlois                     | Jay Baruchel, Gerard Butler,Christopher Mintz-Plasse, Craig Ferguson          |            8.1 |   |   |
| Tate Taylor                      | Emma Stone, Viola Davis, Octavia Spencer, Bryce Dallas Howard                 |            8.1 |   |   |
| Joss Whedon                      | Robert Downey Jr., Chris Evans, Scarlett Johansson,Jeremy Renner              |            8.1 |   |   |
| Denis Villeneuve                 | Hugh Jackman, Jake Gyllenhaal, Viola Davis,Melissa Leo                        |            8.1 |   |   |
| Steve McQueen                    | Chiwetel Ejiofor, Michael Kenneth Williams, Michael Fassbender, Brad Pitt     |            8.1 |   |   |
| Ron Howard                       | Daniel Brühl, Chris Hemsworth, Olivia Wilde,Alexandra Maria Lara              |            8.1 |   |   |
| James Gunn                       | Chris Pratt, Vin Diesel, Bradley Cooper, Zoe Saldana                          |            8.1 |   |   |
| David Fincher                    | Ben Affleck, Rosamund Pike, Neil Patrick Harris,Tyler Perry                   |            8.1 |   |   |
| Morten Tyldum                    | Benedict Cumberbatch, Keira Knightley, Matthew Goode, Allen Leech             |            8.1 |   |   |
| Wes Anderson                     | Ralph Fiennes, F. Murray Abraham, Mathieu Amalric,Adrien Brody                |            8.1 |   |   |
| Xavier Dolan                     | Anne Dorval, Antoine-Olivier Pilon, Suzanne Clément,Patrick Huard             |            8.1 |   |   |
| Damián Szifron                   | Darío Grandinetti, María Marull, Mónica Villa, Rita Cortese                   |            8.1 |   |   |
| J.J. Abrams                      | Daisy Ridley, John Boyega, Oscar Isaac, Domhnall Gleeson                      |            8.1 |   |   |
| George Miller                    | Tom Hardy, Charlize Theron, Nicholas Hoult, Zoë Kravitz                       |            8.1 |   |   |
| Tom McCarthy                     | Mark Ruffalo, Michael Keaton, Rachel McAdams, Liev Schreiber                  |            8.1 |   |   |
| Garth Davis                      | Dev Patel, Nicole Kidman, Rooney Mara, Sunny Pawar                            |            8.1 |   |   |
| Byron Howard                     | Ginnifer Goodwin, Jason Bateman, Idris Elba, Jenny Slate                      |            8.1 |   |   |
| Chan-wook Park                   | Min-hee Kim, Jung-woo Ha, Jin-woong Jo, So-ri Moon                            |            8.1 |   |   |
| Martin Campbell                  | Daniel Craig, Eva Green, Judi Dench, Jeffrey Wright                           |              8 |   |   |
| Gabriele Muccino                 | Will Smith, Thandie Newton, Jaden Smith, Brian Howe                           |              8 |   |   |
| Edward Zwick                     | Leonardo DiCaprio, Djimon Hounsou, Jennifer Connelly, Kagiso Kuypers          |              8 |   |   |
| Brad Bird                        | Brad Garrett, Lou Romano, Patton Oswalt,Ian Holm                              |              8 |   |   |
| Danny Boyle                      | Dev Patel, Freida Pinto, Saurabh Shukla, Anil Kapoor                          |              8 |   |   |
| J.J. Abrams                      | Chris Pine, Zachary Quinto, Simon Pegg, Leonard Nimoy                         |              8 |   |   |
| Neill Blomkamp                   | Sharlto Copley, David James, Jason Cope, Nathalie Boltt                       |              8 |   |   |
| Darren Aronofsky                 | Natalie Portman, Mila Kunis, Vincent Cassel,Winona Ryder                      |              8 |   |   |
| Tom Hooper                       | Colin Firth, Geoffrey Rush, Helena Bonham Carter,Derek Jacobi                 |              8 |   |   |
| Stephen Chbosky                  | Logan Lerman, Emma Watson, Ezra Miller, Paul Rudd                             |              8 |   |   |
| Spike Jonze                      | Joaquin Phoenix, Amy Adams, Scarlett Johansson,Rooney Mara                    |              8 |   |   |
| Jean-Marc Vallée                 | Matthew McConaughey, Jennifer Garner, Jared Leto, Steve Zahn                  |              8 |   |   |
| Bryan Singer                     | Patrick Stewart, Ian McKellen, Hugh Jackman, James McAvoy                     |              8 |   |   |
| Ridley Scott                     | Matt Damon, Jessica Chastain, Kristen Wiig, Kate Mara                         |              8 |   |   |
| Alejandro González Iñárritu      | Leonardo DiCaprio, Tom Hardy, Will Poulter, Domhnall Gleeson                  |              8 |   |   |
| Denis Villeneuve                 | Amy Adams, Jeremy Renner, Forest Whitaker,Michael Stuhlbarg                   |              8 |   |   |
| Tim Miller                       | Ryan Reynolds, Morena Baccarin, T.J. Miller, Ed Skrein                        |              8 |   |   |
| Asghar Farhadi                   | Taraneh Alidoosti, Shahab Hosseini, Babak Karimi,Farid Sajjadi Hosseini       |              8 |   |   |
| John Carney                      | Ferdia Walsh-Peelo, Aidan Gillen, Maria Doyle Kennedy, Jack Reynor            |              8 |   |   |
| Alfonso Cuarón                   | Julianne Moore, Clive Owen, Chiwetel Ejiofor,Michael Caine                    |            7.9 |   |   |
| Tarsem Singh                     | Lee Pace, Catinca Untaru, Justine Waddell, Kim Uylenbroek                     |            7.9 |   |   |
| Edgar Wright                     | Simon Pegg, Nick Frost, Martin Freeman, Bill Nighy                            |            7.9 |   |   |
| Jon Favreau                      | Robert Downey Jr., Gwyneth Paltrow, Terrence Howard, Jeff Bridges             |            7.9 |   |   |
| Martin McDonagh                  | Colin Farrell, Brendan Gleeson, Ciarán Hinds,Elizabeth Berrington             |            7.9 |   |   |
| Duncan Jones                     | Sam Rockwell, Kevin Spacey, Dominique McElligott,Rosie Shaw                   |            7.9 |   |   |
| Peter Jackson                    | Martin Freeman, Ian McKellen, Richard Armitage,Andy Serkis                    |            7.9 |   |   |
| Ang Lee                          | Suraj Sharma, Irrfan Khan, Adil Hussain, Tabu                                 |            7.9 |   |   |
| Peter Jackson                    | Ian McKellen, Martin Freeman, Richard Armitage,Ken Stott                      |            7.9 |   |   |
| Dan Gilroy                       | Jake Gyllenhaal, Rene Russo, Bill Paxton, Riz Ahmed                           |            7.9 |   |   |
| Doug Liman                       | Tom Cruise, Emily Blunt, Bill Paxton, Brendan Gleeson                         |            7.9 |   |   |
| Richard Linklater                | Ellar Coltrane, Patricia Arquette, Ethan Hawke,Elijah Smith                   |            7.9 |   |   |
| Dean DeBlois                     | Jay Baruchel, Cate Blanchett, Gerard Butler, Craig Ferguson                   |            7.9 |   |   |
| F. Gary Gray                     | O'Shea Jackson Jr., Corey Hawkins, Jason Mitchell,Neil Brown Jr.              |            7.9 |   |   |
| Gareth Edwards                   | Felicity Jones, Diego Luna, Alan Tudyk, Donnie Yen                            |            7.9 |   |   |
| Kenneth Lonergan                 | Casey Affleck, Michelle Williams, Kyle Chandler,Lucas Hedges                  |            7.9 |   |   |
| Anthony Russo                    | Chris Evans, Robert Downey Jr.,Scarlett Johansson, Sebastian Stan             |            7.9 |   |   |
| Matt Ross                        | Viggo Mortensen, George MacKay, Samantha Isler,Annalise Basso                 |            7.9 |   |   |
| Travis Knight                    | Charlize Theron, Art Parkinson, Matthew McConaughey, Ralph Fiennes            |            7.9 |   |   |
| Taika Waititi                    | Sam Neill, Julian Dennison, Rima Te Wiata, Rachel House                       |            7.9 |   |   |
| Mel Gibson                       | Gerardo Taracena, Raoul Max Trujillo, Dalia Hernández,Rudy Youngblood         |            7.8 |   |   |
| Jonathan Dayton                  | Steve Carell, Toni Collette, Greg Kinnear, Abigail Breslin                    |            7.8 |   |   |
| Paul McGuigan                    | Josh Hartnett, Ben Kingsley, Morgan Freeman, Lucy Liu                         |            7.8 |   |   |
| Ridley Scott                     | Denzel Washington, Russell Crowe, Chiwetel Ejiofor,Josh Brolin                |            7.8 |   |   |
| Pierre Morel                     | Liam Neeson, Maggie Grace, Famke Janssen, Leland Orser                        |            7.8 |   |   |
| David Fincher                    | Brad Pitt, Cate Blanchett, Tilda Swinton, Julia Ormond                        |            7.8 |   |   |
| Mark Herman                      | Asa Butterfield, David Thewlis, Rupert Friend, Zac Mattoon O'Brien            |            7.8 |   |   |
| Clint Eastwood                   | Angelina Jolie, Colm Feore, Amy Ryan, Gattlin Griffith                        |            7.8 |   |   |
| David Yates                      | Daniel Radcliffe, Emma Watson, Rupert Grint, Michael Gambon                   |            7.8 |   |   |
| James Cameron                    | Sam Worthington, Zoe Saldana, Sigourney Weaver, Michelle Rodriguez            |            7.8 |   |   |
| Todd Phillips                    | Zach Galifianakis, Bradley Cooper, Justin Bartha, Ed Helms                    |            7.8 |   |   |
| Niels Arden Oplev                | Michael Nyqvist, Noomi Rapace, Ewa Fröling,Lena Endre                         |            7.8 |   |   |
| Wes Anderson                     | George Clooney, Meryl Streep, Bill Murray, Jason Schwartzman                  |            7.8 |   |   |
| Nathan Greno                     | Mandy Moore, Zachary Levi, Donna Murphy, Ron Perlman                          |            7.8 |   |   |
| David O. Russell                 | Mark Wahlberg, Christian Bale, Amy Adams,Melissa Leo                          |            7.8 |   |   |
| Nicolas Winding Refn             | Ryan Gosling, Carey Mulligan, Bryan Cranston, Albert Brooks                   |            7.8 |   |   |
| Matthew Vaughn                   | James McAvoy, Michael Fassbender, Jennifer Lawrence, Kevin Bacon              |            7.8 |   |   |
| David Fincher                    | Daniel Craig, Rooney Mara, Christopher Plummer,Stellan Skarsgård              |            7.8 |   |   |
| Sam Mendes                       | Daniel Craig, Javier Bardem, Naomie Harris, Judi Dench                        |            7.8 |   |   |
| David O. Russell                 | Bradley Cooper, Jennifer Lawrence, Robert De Niro, Jacki Weaver               |            7.8 |   |   |
| Wes Anderson                     | Jared Gilman, Kara Hayward, Bruce Willis, Bill Murray                         |            7.8 |   |   |
| Rich Moore                       | John C. Reilly, Jack McBrayer, Jane Lynch, Sarah Silverman                    |            7.8 |   |   |
| Abdellatif Kechiche              | Léa Seydoux, Adèle Exarchopoulos, Salim Kechiouche, Aurélien Recoing          |            7.8 |   |   |
| Richard Curtis                   | Domhnall Gleeson, Rachel McAdams, Bill Nighy,Lydia Wilson                     |            7.8 |   |   |
| J.J. Abrams                      | Chris Pine, Zachary Quinto, Zoe Saldana, Benedict Cumberbatch                 |            7.8 |   |   |
| Alfonso Cuarón                   | Sandra Bullock, George Clooney, Ed Harris, Orto Ignatiussen                   |            7.8 |   |   |
| Paul Greengrass                  | Tom Hanks, Barkhad Abdi, Barkhad Abdirahman,Catherine Keener                  |            7.8 |   |   |
| Giuseppe Tornatore               | Geoffrey Rush, Jim Sturgess, Sylvia Hoeks,Donald Sutherland                   |            7.8 |   |   |
| Anthony Russo                    | Chris Evans, Samuel L. Jackson,Scarlett Johansson, Robert Redford             |            7.8 |   |   |
| Alejandro González Iñárritu      | Michael Keaton, Zach Galifianakis,Edward Norton, Andrea Riseborough           |            7.8 |   |   |
| Josh Boone                       | Shailene Woodley, Ansel Elgort, Nat Wolff, Laura Dern                         |            7.8 |   |   |
| Phil Lord                        | Chris Pratt, Will Ferrell, Elizabeth Banks, Will Arnett                       |            7.8 |   |   |
| Don Hall                         | Ryan Potter, Scott Adsit, Jamie Chung,T.J. Miller                             |            7.8 |   |   |
| Quentin Tarantino                | Samuel L. Jackson, Kurt Russell, Jennifer Jason Leigh, Walton Goggins         |            7.8 |   |   |
| Adam McKay                       | Christian Bale, Steve Carell, Ryan Gosling, Brad Pitt                         |            7.8 |   |   |
| Alfonso Gomez-Rejon              | Thomas Mann, RJ Cyler, Olivia Cooke, Nick Offerman                            |            7.8 |   |   |
| Theodore Melfi                   | Taraji P. Henson, Octavia Spencer, Janelle Monáe,Kevin Costner                |            7.8 |   |   |
| Gauri Shinde                     | Alia Bhatt, Shah Rukh Khan, Kunal Kapoor, Priyanka Moodley                    |            7.8 |   |   |
| Claude Barras                    | Gaspard Schlatter, Sixtine Murat, Paulin Jaccoud,Michel Vuillermoz            |            7.8 |   |   |
| Zack Snyder                      | Gerard Butler, Lena Headey, David Wenham, Dominic West                        |            7.7 |   |   |
| David Fincher                    | Jake Gyllenhaal, Robert Downey Jr., Mark Ruffalo,Anthony Edwards              |            7.7 |   |   |
| Matthew Vaughn                   | Charlie Cox, Claire Danes, Sienna Miller, Ian McKellen                        |            7.7 |   |   |
| David Cronenberg                 | Naomi Watts, Viggo Mortensen, Armin Mueller-Stahl, Josef Altin                |            7.7 |   |   |
| Ben Affleck                      | Morgan Freeman, Ed Harris, Casey Affleck, Michelle Monaghan                   |            7.7 |   |   |
| Gabriele Muccino                 | Will Smith, Rosario Dawson, Woody Harrelson,Michael Ealy                      |            7.7 |   |   |
| John Lee Hancock                 | Quinton Aaron, Sandra Bullock, Tim McGraw,Jae Head                            |            7.7 |   |   |
| Ruben Fleischer                  | Jesse Eisenberg, Emma Stone, Woody Harrelson,Abigail Breslin                  |            7.7 |   |   |
| Henry Selick                     | Dakota Fanning, Teri Hatcher, John Hodgman, Jennifer Saunders                 |            7.7 |   |   |
| Marc Webb                        | Zooey Deschanel, Joseph Gordon-Levitt, Geoffrey Arend, Chloë Grace Moretz     |            7.7 |   |   |
| Matthew Vaughn                   | Aaron Taylor-Johnson, Nicolas Cage, Chloë Grace Moretz, Garrett M. Brown      |            7.7 |   |   |
| David Fincher                    | Jesse Eisenberg, Andrew Garfield, Justin Timberlake,Rooney Mara               |            7.7 |   |   |
| Pierre Coffin                    | Steve Carell, Jason Segel, Russell Brand, Julie Andrews                       |            7.7 |   |   |
| David Yates                      | Daniel Radcliffe, Emma Watson, Rupert Grint, Bill Nighy                       |            7.7 |   |   |
| Woody Allen                      | Owen Wilson, Rachel McAdams, Kathy Bates, Kurt Fuller                         |            7.7 |   |   |
| Jonathan Levine                  | Joseph Gordon-Levitt, Seth Rogen, Anna Kendrick, Bryce Dallas Howard          |            7.7 |   |   |
| Ben Affleck                      | Ben Affleck, Bryan Cranston, John Goodman, Alan Arkin                         |            7.7 |   |   |
| David Ayer                       | Jake Gyllenhaal, Michael Peña, Anna Kendrick, America Ferrera                 |            7.7 |   |   |
| Matthew Vaughn                   | Colin Firth, Taron Egerton, Samuel L. Jackson,Michael Caine                   |            7.7 |   |   |
| Alex Garland                     | Alicia Vikander, Domhnall Gleeson, Oscar Isaac,Sonoya Mizuno                  |            7.7 |   |   |
| James Marsh                      | Eddie Redmayne, Felicity Jones, Tom Prior, Sophie Perry                       |            7.7 |   |   |
| Hannes Holm                      | Rolf Lassgård, Bahar Pars, Filip Berg, Ida Engvoll                            |            7.7 |   |   |
| Ron Clements                     | Auli'i Cravalho, Dwayne Johnson, Rachel House, Temuera Morrison               |            7.7 |   |   |
| David Mackenzie                  | Chris Pine, Ben Foster, Jeff Bridges, Gil Birmingham                          |            7.7 |   |   |
| Bruce Beresford                  | Eddie Murphy, Britt Robertson, Natascha McElhone, Xavier Samuel               |            7.7 |   |   |
| Neil Burger                      | Edward Norton, Jessica Biel, Paul Giamatti, Rufus Sewell                      |            7.6 |   |   |
| Spike Lee                        | Denzel Washington, Clive Owen, Jodie Foster,Christopher Plummer               |            7.6 |   |   |
| Greg Mottola                     | Michael Cera, Jonah Hill, Christopher Mintz-Plasse, Bill Hader                |            7.6 |   |   |
| Kathryn Bigelow                  | Jeremy Renner, Anthony Mackie, Brian Geraghty,Guy Pearce                      |            7.6 |   |   |
| Steve McQueen                    | Stuart Graham, Laine Megaw, Brian Milligan, Liam McMahon                      |            7.6 |   |   |
| Mark Osborne                     | Jack Black, Ian McShane,Angelina Jolie, Dustin Hoffman                        |            7.6 |   |   |
| Zack Snyder                      | Jackie Earle Haley, Patrick Wilson, Carla Gugino,Malin Akerman                |            7.6 |   |   |
| Guy Ritchie                      | Robert Downey Jr., Jude Law, Rachel McAdams, Mark Strong                      |            7.6 |   |   |
| Ben Affleck                      | Ben Affleck, Rebecca Hall, Jon Hamm, Jeremy Renner                            |            7.6 |   |   |
| Ethan Coen                       | Jeff Bridges, Matt Damon, Hailee Steinfeld,Josh Brolin                        |            7.6 |   |   |
| Danny Boyle                      | James Franco, Amber Tamblyn, Kate Mara, Sean Bott                             |            7.6 |   |   |
| Rupert Wyatt                     | James Franco, Andy Serkis, Freida Pinto, Karin Konoval                        |            7.6 |   |   |
| Bennett Miller                   | Brad Pitt, Robin Wright, Jonah Hill, Philip Seymour Hoffman                   |            7.6 |   |   |
| Pedro Almodóvar                  | Antonio Banderas, Elena Anaya, Jan Cornet,Marisa Paredes                      |            7.6 |   |   |
| Tom Hooper                       | Hugh Jackman, Russell Crowe, Anne Hathaway,Amanda Seyfried                    |            7.6 |   |   |
| J.A. Bayona                      | Naomi Watts, Ewan McGregor, Tom Holland, Oaklee Pendergast                    |            7.6 |   |   |
| Francis Lawrence                 | Jennifer Lawrence, Josh Hutcherson, Liam Hemsworth, Philip Seymour Hoffman    |            7.6 |   |   |
| Matt Reeves                      | Gary Oldman, Keri Russell, Andy Serkis, Kodi Smit-McPhee                      |            7.6 |   |   |
| David Ayer                       | Brad Pitt, Shia LaBeouf, Logan Lerman, Michael Peña                           |            7.6 |   |   |
| Jemaine Clement                  | Jemaine Clement, Taika Waititi,Cori Gonzalez-Macuer, Jonny Brugh              |            7.6 |   |   |
| Denis Villeneuve                 | Emily Blunt, Josh Brolin, Benicio Del Toro, Jon Bernthal                      |            7.6 |   |   |
| Ryan Coogler                     | Michael B. Jordan, Sylvester Stallone, Tessa Thompson, Phylicia Rashad        |            7.6 |   |   |
| Steven Spielberg                 | Tom Hanks, Mark Rylance, Alan Alda, Amy Ryan                                  |            7.6 |   |   |
| Scott Derrickson                 | Benedict Cumberbatch, Chiwetel Ejiofor, Rachel McAdams, Benedict Wong         |            7.6 |   |   |
| Maren Ade                        | Sandra Hüller, Peter Simonischek, Michael Wittenborn,Thomas Loibl             |            7.6 |   |   |
| Michael Dudok de Wit             | Emmanuel Garijo, Tom Hudson, Baptiste Goy, Axel Devillers                     |            7.6 |   |   |
| Alejandro González Iñárritu      | Brad Pitt, Cate Blanchett, Gael García Bernal, Mohamed Akhzam                 |            7.5 |   |   |
| Tom Tykwer                       | Ben Whishaw, Dustin Hoffman, Alan Rickman,Francesc Albiol                     |            7.5 |   |   |
| David Yates                      | Daniel Radcliffe, Emma Watson, Rupert Grint, Brendan Gleeson                  |            7.5 |   |   |
| Jason Reitman                    | Ellen Page, Michael Cera, Jennifer Garner, Jason Bateman                      |            7.5 |   |   |
| Andrew Dominik                   | Brad Pitt, Casey Affleck, Sam Shepard, Mary-Louise Parker                     |            7.5 |   |   |
| Kirsten Sheridan                 | Freddie Highmore, Keri Russell, Jonathan Rhys Meyers, Terrence Howard         |            7.5 |   |   |
| Richard LaGravenese              | Hilary Swank, Imelda Staunton, Patrick Dempsey, Scott Glenn                   |            7.5 |   |   |
| Edgar Wright                     | Michael Cera, Mary Elizabeth Winstead, Kieran Culkin, Alison Pill             |            7.5 |   |   |
| Guy Ritchie                      | Robert Downey Jr., Jude Law, Jared Harris, Rachel McAdams                     |            7.5 |   |   |
| Duncan Jones                     | Jake Gyllenhaal, Michelle Monaghan, Vera Farmiga,Jeffrey Wright               |            7.5 |   |   |
| Lynne Ramsay                     | Tilda Swinton, John C. Reilly, Ezra Miller, Jasper Newell                     |            7.5 |   |   |
| Martin Scorsese                  | Asa Butterfield, Chloë Grace Moretz, Christopher Lee, Ben Kingsley            |            7.5 |   |   |
| Tom Tykwer                       | Tom Hanks, Halle Berry, Hugh Grant, Hugo Weaving                              |            7.5 |   |   |
| Chris Buck                       | Kristen Bell, Idina Menzel, Jonathan Groff, Josh Gad                          |            7.5 |   |   |
| James Wan                        | Patrick Wilson, Vera Farmiga, Ron Livingston, Lili Taylor                     |            7.5 |   |   |
| Peter Berg                       | Mark Wahlberg, Taylor Kitsch, Emile Hirsch, Ben Foster                        |            7.5 |   |   |
| Brian Helgeland                  | Chadwick Boseman, T.R. Knight, Harrison Ford,Nicole Beharie                   |            7.5 |   |   |
| John Lee Hancock                 | Emma Thompson, Tom Hanks, Annie Rose Buckley, Colin Farrell                   |            7.5 |   |   |
| John Crowley                     | Saoirse Ronan, Emory Cohen, Domhnall Gleeson,Jim Broadbent                    |            7.5 |   |   |
| David Yates                      | Eddie Redmayne, Katherine Waterston, Alison Sudol,Dan Fogler                  |            7.5 |   |   |
| Tom Ford                         | Amy Adams, Jake Gyllenhaal, Michael Shannon, Aaron Taylor-Johnson             |            7.5 |   |   |
| Barry Jenkins                    | Mahershala Ali, Shariff Earp, Duan Sanderson, Alex R. Hibbert                 |            7.5 |   |   |
| Clint Eastwood                   | Tom Hanks, Aaron Eckhart, Laura Linney, Valerie Mahaffey                      |            7.5 |   |   |
| Robin Swicord                    | Bryan Cranston, Jennifer Garner, Beverly D'Angelo,Jason O'Mara                |            7.5 |   |   |
| J.A. Bayona                      | Lewis MacDougall, Sigourney Weaver, Felicity Jones,Toby Kebbell               |            7.5 |   |   |
| Jon Favreau                      | Neel Sethi, Bill Murray, Ben Kingsley, Idris Elba                             |            7.5 |   |   |
| Julia Ducournau                  | Garance Marillier, Ella Rumpf, Rabah Nait Oufella,Laurent Lucas               |            7.5 |   |   |
| Jim Jarmusch                     | Adam Driver, Golshifteh Farahani, Nellie, Rizwan Manji                        |            7.5 |   |   |
| Sang-ho Yeon                     | Yoo Gong, Soo-an Kim, Yu-mi Jung, Dong-seok Ma                                |            7.5 |   |   |
| François Ozon                    | Pierre Niney, Paula Beer, Ernst Stötzner, Marie Gruber                        |            7.5 |   |   |
| Cristian Mungiu                  | Adrian Titieni, Maria-Victoria Dragus, Lia Bugnar,Malina Manovici             |            7.5 |   |   |
| Hong-jin Na                      | Jun Kunimura, Jung-min Hwang, Do-won Kwak, Woo-hee Chun                       |            7.5 |   |   |
| Tim Burton                       | Johnny Depp, Helena Bonham Carter, Alan Rickman,Timothy Spall                 |            7.4 |   |   |
| Julie Taymor                     | Evan Rachel Wood, Jim Sturgess, Joe Anderson, Dana Fuchs                      |            7.4 |   |   |
| F. Gary Gray                     | Gerard Butler, Jamie Foxx, Leslie Bibb, Colm Meaney                           |            7.4 |   |   |
| Derek Cianfrance                 | Ryan Gosling, Michelle Williams, John Doman,Faith Wladyka                     |            7.4 |   |   |
| Glenn Ficarra                    | Steve Carell, Ryan Gosling, Julianne Moore, Emma Stone                        |            7.4 |   |   |
| Brad Bird                        | Tom Cruise, Jeremy Renner, Simon Pegg, Paula Patton                           |            7.4 |   |   |
| Neil Burger                      | Bradley Cooper, Anna Friel, Abbie Cornish, Robert De Niro                     |            7.4 |   |   |
| Cary Joji Fukunaga               | Mia Wasikowska, Michael Fassbender, Jamie Bell, Su Elliot                     |            7.4 |   |   |
| Steven Spielberg                 | Daniel Day-Lewis, Sally Field, David Strathairn,Joseph Gordon-Levitt          |            7.4 |   |   |
| Rian Johnson                     | Joseph Gordon-Levitt, Bruce Willis, Emily Blunt, Paul Dano                    |            7.4 |   |   |
| Kathryn Bigelow                  | Jessica Chastain, Joel Edgerton, Chris Pratt, Mark Strong                     |            7.4 |   |   |
| Pierre Coffin                    | Steve Carell, Kristen Wiig, Benjamin Bratt, Miranda Cosgrove                  |            7.4 |   |   |
| John Carney                      | Keira Knightley, Mark Ruffalo, Adam Levine, Hailee Steinfeld                  |            7.4 |   |   |
| Peter Jackson                    | Ian McKellen, Martin Freeman, Richard Armitage,Cate Blanchett                 |            7.4 |   |   |
| David Dobkin                     | Robert Downey Jr., Robert Duvall, Vera Farmiga, Billy Bob Thornton            |            7.4 |   |   |
| Joss Whedon                      | Robert Downey Jr., Chris Evans, Mark Ruffalo, Chris Hemsworth                 |            7.4 |   |   |
| Christopher McQuarrie            | Tom Cruise, Rebecca Ferguson, Jeremy Renner, Simon Pegg                       |            7.4 |   |   |
| Antoine Fuqua                    | Jake Gyllenhaal, Rachel McAdams, Oona Laurence,Forest Whitaker                |            7.4 |   |   |
| Thea Sharrock                    | Emilia Clarke, Sam Claflin, Janet McTeer, Charles Dance                       |            7.4 |   |   |
| Peter Berg                       | Mark Wahlberg, Michelle Monaghan, J.K. Simmons, John Goodman                  |            7.4 |   |   |
| Gavin O'Connor                   | Ben Affleck, Anna Kendrick, J.K. Simmons, Jon Bernthal                        |            7.4 |   |   |
| Shane Black                      | Russell Crowe, Ryan Gosling, Angourie Rice, Matt Bomer                        |            7.4 |   |   |
| Andrew Stanton                   | Ellen DeGeneres, Albert Brooks,Ed O'Neill, Kaitlin Olson                      |            7.4 |   |   |
| Kelly Fremon Craig               | Hailee Steinfeld, Haley Lu Richardson, Blake Jenner, Kyra Sedgwick            |            7.4 |   |   |
| James Wan                        | Vera Farmiga, Patrick Wilson, Madison Wolfe, Frances O'Connor                 |            7.4 |   |   |
| Mike Mills                       | Annette Bening, Elle Fanning, Greta Gerwig, Billy Crudup                      |            7.4 |   |   |
| Roger Spottiswoode               | Luke Treadaway, Bob the Cat, Ruta Gedmintas, Joanne Froggatt                  |            7.4 |   |   |
| Dexter Fletcher                  | Taron Egerton, Hugh Jackman, Tom Costello, Jo Hartley                         |            7.4 |   |   |
| Mira Nair                        | Madina Nalwanga, David Oyelowo, Lupita Nyong'o, Martin Kabanza                |            7.4 |   |   |
| Gore Verbinski                   | Johnny Depp, Orlando Bloom, Keira Knightley, Jack Davenport                   |            7.3 |   |   |
| Darren Aronofsky                 | Hugh Jackman, Rachel Weisz, Sean Patrick Thomas, Ellen Burstyn                |            7.3 |   |   |
| Werner Herzog                    | Christian Bale, Steve Zahn, Jeremy Davies, Zach Grenier                       |            7.3 |   |   |
| Danny Boyle                      | Cillian Murphy, Rose Byrne, Chris Evans, Michelle Yeoh                        |            7.3 |   |   |
| Bruce A. Evans                   | Kevin Costner, Demi Moore, William Hurt, Dane Cook                            |            7.3 |   |   |
| Guy Ritchie                      | Gerard Butler, Tom Wilkinson, Idris Elba, Thandie Newton                      |            7.3 |   |   |
| Sam Mendes                       | Leonardo DiCaprio, Kate Winslet, Christopher Fitzgerald, Jonathan Roumie      |            7.3 |   |   |
| Yorgos Lanthimos                 | Christos Stergioglou, Michele Valley, Angeliki Papoulia, Hristos Passalis     |            7.3 |   |   |
| Lee Daniels                      | Gabourey Sidibe, Mo'Nique, Paula Patton, Mariah Carey                         |            7.3 |   |   |
| Tom McGrath                      | Will Ferrell, Jonah Hill, Brad Pitt, Tina Fey                                 |            7.3 |   |   |
| Justin Lin                       | Vin Diesel, Paul Walker, Dwayne Johnson, Jordana Brewster                     |            7.3 |   |   |
| Alexander Payne                  | George Clooney, Shailene Woodley, Amara Miller, Nick Krause                   |            7.3 |   |   |
| Derek Cianfrance                 | Ryan Gosling, Bradley Cooper, Eva Mendes,Craig Van Hook                       |            7.3 |   |   |
| John Hillcoat                    | Tom Hardy, Shia LaBeouf, Guy Pearce, Jason Clarke                             |            7.3 |   |   |
| Robert Zemeckis                  | Denzel Washington, Nadine Velazquez, Don Cheadle, John Goodman                |            7.3 |   |   |
| Baz Luhrmann                     | Leonardo DiCaprio, Carey Mulligan, Joel Edgerton,Tobey Maguire                |            7.3 |   |   |
| Louis Leterrier                  | Jesse Eisenberg, Common, Mark Ruffalo, Woody Harrelson                        |            7.3 |   |   |
| David O. Russell                 | Christian Bale, Amy Adams, Bradley Cooper,Jennifer Lawrence                   |            7.3 |   |   |
| Dan Scanlon                      | Billy Crystal, John Goodman, Steve Buscemi, Helen Mirren                      |            7.3 |   |   |
| Ben Stiller                      | Ben Stiller, Kristen Wiig, Jon Daly, Kathryn Hahn                             |            7.3 |   |   |
| Woody Allen                      | Cate Blanchett, Alec Baldwin, Peter Sarsgaard, Sally Hawkins                  |            7.3 |   |   |
| Clint Eastwood                   | Bradley Cooper, Sienna Miller, Kyle Gallner, Cole Konis                       |            7.3 |   |   |
| Mike Cahill                      | Michael Pitt, Steven Yeun, Astrid Bergès-Frisbey, Brit Marling                |            7.3 |   |   |
| Jorge R. Gutiérrez               | Diego Luna, Zoe Saldana, Channing Tatum, Ron Perlman                          |            7.3 |   |   |
| Jon Favreau                      | Jon Favreau, Robert Downey Jr., Scarlett Johansson,Dustin Hoffman             |            7.3 |   |   |
| Guy Ritchie                      | Henry Cavill, Armie Hammer, Alicia Vikander, Elizabeth Debicki                |            7.3 |   |   |
| Simon Curtis                     | Helen Mirren, Ryan Reynolds, Daniel Brühl, Katie Holmes                       |            7.3 |   |   |
| Peyton Reed                      | Paul Rudd, Michael Douglas, Corey Stoll, Evangeline Lilly                     |            7.3 |   |   |
| Paolo Sorrentino                 | Michael Caine, Harvey Keitel, Rachel Weisz, Jane Fonda                        |            7.3 |   |   |
| Rick Famuyiwa                    | Shameik Moore, Tony Revolori, Kiersey Clemons,Kimberly Elise                  |            7.3 |   |   |
| Gavin Hood                       | Helen Mirren, Aaron Paul, Alan Rickman, Barkhad Abdi                          |            7.3 |   |   |
| M. Night Shyamalan               | James McAvoy, Anya Taylor-Joy, Haley Lu Richardson, Jessica Sula              |            7.3 |   |   |
| John Madden                      | Jessica Chastain, Mark Strong, Gugu Mbatha-Raw,Michael Stuhlbarg              |            7.3 |   |   |
| Martin Scorsese                  | Andrew Garfield, Adam Driver, Liam Neeson,Tadanobu Asano                      |            7.3 |   |   |
| Denzel Washington                | Denzel Washington, Viola Davis, Stephen Henderson, Jovan Adepo                |            7.3 |   |   |
| Michael Bay                      | John Krasinski, Pablo Schreiber, James Badge Dale,David Denman                |            7.3 |   |   |
| Oliver Stone                     | Joseph Gordon-Levitt, Shailene Woodley, Melissa Leo,Zachary Quinto            |            7.3 |   |   |
| Sylvester Stallone               | Sylvester Stallone, Antonio Tarver, Milo Ventimiglia, Burt Young              |            7.2 |   |   |
| Francis Lawrence                 | Will Smith, Alice Braga, Charlie Tahan, Salli Richardson-Whitfield            |            7.2 |   |   |
| Antoine Fuqua                    | Mark Wahlberg, Michael Peña, Rhona Mitra, Danny Glover                        |            7.2 |   |   |
| Frank Darabont                   | Thomas Jane, Marcia Gay Harden, Laurie Holden,Andre Braugher                  |            7.2 |   |   |
| Len Wiseman                      | Bruce Willis, Justin Long, Timothy Olyphant, Maggie Q                         |            7.2 |   |   |
| Gregory Hoblit                   | Anthony Hopkins, Ryan Gosling, David Strathairn,Rosamund Pike                 |            7.2 |   |   |
| Gabor Csupo                      | Josh Hutcherson, AnnaSophia Robb, Zooey Deschanel, Robert Patrick             |            7.2 |   |   |
| Nicholas Stoller                 | Kristen Bell, Jason Segel, Paul Rudd, Mila Kunis                              |            7.2 |   |   |
| Roman Polanski                   | Ewan McGregor, Pierce Brosnan, Olivia Williams,Jon Bernthal                   |            7.2 |   |   |
| Matt Reeves                      | Kodi Smit-McPhee, Chloë Grace Moretz, Richard Jenkins, Cara Buono             |            7.2 |   |   |
| Allen Coulter                    | Robert Pattinson, Emilie de Ravin, Caitlyn Rund,Moisés Acevedo                |            7.2 |   |   |
| Steve McQueen                    | Michael Fassbender, Carey Mulligan, James Badge Dale, Lucy Walters            |            7.2 |   |   |
| Gary Ross                        | Jennifer Lawrence, Josh Hutcherson, Liam Hemsworth,Stanley Tucci              |            7.2 |   |   |
| Phil Lord                        | Jonah Hill, Channing Tatum, Ice Cube,Brie Larson                              |            7.2 |   |   |
| Jason Moore                      | Anna Kendrick, Brittany Snow, Rebel Wilson, Anna Camp                         |            7.2 |   |   |
| Mark Andrews                     | Kelly Macdonald,Billy Connolly, Emma Thompson, Julie Walters                  |            7.2 |   |   |
| Martin McDonagh                  | Colin Farrell, Woody Harrelson, Sam Rockwell,Christopher Walken               |            7.2 |   |   |
| Shane Black                      | Robert Downey Jr., Guy Pearce, Gwyneth Paltrow,Don Cheadle                    |            7.2 |   |   |
| James Ward Byrkit                | Emily Baldoni, Maury Sterling, Nicholas Brendon, Elizabeth Gracen             |            7.2 |   |   |
| Jordan Vogt-Roberts              | Nick Robinson, Gabriel Basso, Moises Arias,Nick Offerman                      |            7.2 |   |   |
| Chad Stahelski                   | Keanu Reeves, Michael Nyqvist, Alfie Allen, Willem Dafoe                      |            7.2 |   |   |
| Antoine Fuqua                    | Denzel Washington, Marton Csokas, Chloë Grace Moretz, David Harbour           |            7.2 |   |   |
| Angelina Jolie                   | Jack O'Connell, Miyavi, Domhnall Gleeson, Garrett Hedlund                     |            7.2 |   |   |
| Christian Ditter                 | Lily Collins, Sam Claflin, Christian Cooke, Jaime Winstone                    |            7.2 |   |   |
| James Wan                        | Vin Diesel, Paul Walker, Dwayne Johnson, Jason Statham                        |            7.2 |   |   |
| Danny Boyle                      | Michael Fassbender, Kate Winslet, Seth Rogen, Jeff Daniels                    |            7.2 |   |   |
| Lee Toland Krieger               | Blake Lively, Michiel Huisman, Harrison Ford,Kathy Baker                      |            7.2 |   |   |
| Todd Haynes                      | Cate Blanchett, Rooney Mara, Sarah Paulson, Kyle Chandler                     |            7.2 |   |   |
| Christophe Lourdelet             | Matthew McConaughey,Reese Witherspoon, Seth MacFarlane, Scarlett Johansson    |            7.2 |   |   |
| John Lee Hancock                 | Michael Keaton, Nick Offerman, John Carroll Lynch, Linda Cardellini           |            7.2 |   |   |
| Fede Alvarez                     | Stephen Lang, Jane Levy, Dylan Minnette, Daniel Zovatto                       |            7.2 |   |   |
| Peter Berg                       | Mark Wahlberg, Kurt Russell, Douglas M. Griffin, James DuMont                 |            7.2 |   |   |
| Dan Trachtenberg                 | John Goodman, Mary Elizabeth Winstead, John Gallagher Jr., Douglas M. Griffin |            7.2 |   |   |
| Derek Cianfrance                 | Michael Fassbender, Alicia Vikander, Rachel Weisz, Florence Clery             |            7.2 |   |   |
| Sean Ellis                       | Jamie Dornan, Cillian Murphy, Brian Caspe, Karel Hermánek Jr.                 |            7.2 |   |   |
| Terence Davies                   | Cynthia Nixon, Jennifer Ehle, Duncan Duff, Keith Carradine                    |            7.2 |   |   |
| Alessandro Carloni               | Jack Black, Bryan Cranston, Dustin Hoffman, Angelina Jolie                    |            7.2 |   |   |
| Jee-woon Kim                     | Byung-hun Lee, Yoo Gong, Kang-ho Song, Ji-min Han                             |            7.2 |   |   |
| John Lasseter                    | Owen Wilson, Bonnie Hunt, Paul Newman, Larry the Cable Guy                    |            7.1 |   |   |
| Gore Verbinski                   | Johnny Depp, Orlando Bloom, Keira Knightley,Geoffrey Rush                     |            7.1 |   |   |
| Kevin Lima                       | Amy Adams, Susan Sarandon, James Marsden, Patrick Dempsey                     |            7.1 |   |   |
| Ridley Scott                     | Leonardo DiCaprio, Russell Crowe, Mark Strong,Golshifteh Farahani             |            7.1 |   |   |
| Woody Allen                      | Rebecca Hall, Scarlett Johansson, Javier Bardem,Christopher Evan Welch        |            7.1 |   |   |
| Sylvester Stallone               | Sylvester Stallone, Julie Benz, Matthew Marsden, Graham McTavish              |            7.1 |   |   |
| Ron Clements                     | Anika Noni Rose, Keith David, Oprah Winfrey, Bruno Campos                     |            7.1 |   |   |
| Will Gluck                       | Emma Stone, Amanda Bynes, Penn Badgley, Dan Byrd                              |            7.1 |   |   |
| Robert Schwentke                 | Bruce Willis, Helen Mirren, Morgan Freeman,Mary-Louise Parker                 |            7.1 |   |   |
| J.J. Abrams                      | Elle Fanning, AJ Michalka, Kyle Chandler, Joel Courtney                       |            7.1 |   |   |
| Tomas Alfredson                  | Gary Oldman, Colin Firth, Tom Hardy, Mark Strong                              |            7.1 |   |   |
| Lars von Trier                   | Kirsten Dunst, Charlotte Gainsbourg, Kiefer Sutherland, Alexander Skarsgård   |            7.1 |   |   |
| Shawn Levy                       | Hugh Jackman, Evangeline Lilly, Dakota Goyo,Anthony Mackie                    |            7.1 |   |   |
| Pete Travis                      | Karl Urban, Olivia Thirlby, Lena Headey, Rachel Wood                          |            7.1 |   |   |
| Justin Lin                       | Vin Diesel, Paul Walker, Dwayne Johnson, Michelle Rodriguez                   |            7.1 |   |   |
| Zack Snyder                      | Henry Cavill, Amy Adams, Michael Shannon, Diane Lane                          |            7.1 |   |   |
| James Ponsoldt                   | Miles Teller, Shailene Woodley, Kyle Chandler,Jennifer Jason Leigh            |            7.1 |   |   |
| Steven Knight                    | Tom Hardy, Olivia Colman, Ruth Wilson, Andrew Scott                           |            7.1 |   |   |
| Phil Lord                        | Channing Tatum, Jonah Hill, Ice Cube,Nick Offerman                            |            7.1 |   |   |
| Michaël R. Roskam                | Tom Hardy, Noomi Rapace, James Gandolfini,Matthias Schoenaerts                |            7.1 |   |   |
| Jean-Marc Vallée                 | Reese Witherspoon, Laura Dern, Gaby Hoffmann,Michiel Huisman                  |            7.1 |   |   |
| Yorgos Lanthimos                 | Colin Farrell, Rachel Weisz, Jessica Barden,Olivia Colman                     |            7.1 |   |   |
| Paul Feig                        | Melissa McCarthy, Rose Byrne, Jude Law, Jason Statham                         |            7.1 |   |   |
| Jocelyn Moorhouse                | Kate Winslet, Judy Davis, Liam Hemsworth,Hugo Weaving                         |            7.1 |   |   |
| Baltasar Kormákur                | Jason Clarke, Ang Phula Sherpa, Thomas M. Wright, Martin Henderson            |            7.1 |   |   |
| George Tillman Jr.               | Scott Eastwood, Britt Robertson, Alan Alda, Jack Huston                       |            7.1 |   |   |
| S. Craig Zahler                  | Kurt Russell, Patrick Wilson, Matthew Fox, Richard Jenkins                    |            7.1 |   |   |
| Joel Edgerton                    | Jason Bateman, Rebecca Hall, Joel Edgerton, Allison Tolman                    |            7.1 |   |   |
| Nancy Meyers                     | Robert De Niro, Anne Hathaway, Rene Russo,Anders Holm                         |            7.1 |   |   |
| James Gray                       | Charlie Hunnam, Robert Pattinson, Sienna Miller, Tom Holland                  |            7.1 |   |   |
| Bryan Singer                     | James McAvoy, Michael Fassbender, Jennifer Lawrence, Nicholas Hoult           |            7.1 |   |   |
| Justin Lin                       | Chris Pine, Zachary Quinto, Karl Urban, Zoe Saldana                           |            7.1 |   |   |
| Robert Zemeckis                  | Brad Pitt, Marion Cotillard, Jared Harris, Vincent Ebrahim                    |            7.1 |   |   |
| Todd Phillips                    | Jonah Hill, Miles Teller, Steve Lantz, Gregg Weiner                           |            7.1 |   |   |
| Joseph Cedar                     | Richard Gere, Lior Ashkenazi, Michael Sheen,Charlotte Gainsbourg              |            7.1 |   |   |
| Brad Furman                      | Bryan Cranston, John Leguizamo, Diane Kruger, Amy Ryan                        |            7.1 |   |   |
| Dan Kwan                         | Paul Dano, Daniel Radcliffe, Mary Elizabeth Winstead, Antonia Ribero          |            7.1 |   |   |
| Jeff Nichols                     | Ruth Negga, Joel Edgerton, Will Dalton, Dean Mumford                          |            7.1 |   |   |
| Mia Hansen-Løve                  | Isabelle Huppert, André Marcon, Roman Kolinka,Edith Scob                      |            7.1 |   |   |
| Bong Joon Ho                     | Kang-ho Song, Hee-Bong Byun, Hae-il Park, Doona Bae                           |              7 |   |   |
| Judd Apatow                      | Seth Rogen, Katherine Heigl, Paul Rudd, Leslie Mann                           |              7 |   |   |
| Juan Carlos Fresnadillo          | Jeremy Renner, Rose Byrne, Robert Carlyle, Harold Perrineau                   |              7 |   |   |
| Ben Stiller                      | Ben Stiller, Jack Black, Robert Downey Jr., Jeff Kahn                         |              7 |   |   |
| Matt Reeves                      | Mike Vogel, Jessica Lucas, Lizzy Caplan, T.J. Miller                          |              7 |   |   |
| Guillermo del Toro               | Ron Perlman, Selma Blair, Doug Jones, John Alexander                          |              7 |   |   |
| David Gordon Green               | Seth Rogen, James Franco, Gary Cole, Danny McBride                            |              7 |   |   |
| Michael Mann                     | Christian Bale, Johnny Depp, Christian Stolte, Jason Clarke                   |              7 |   |   |
| Jaume Collet-Serra               | Vera Farmiga, Peter Sarsgaard, Isabelle Fuhrman, CCH Pounder                  |              7 |   |   |
| Jon Favreau                      | Robert Downey Jr., Mickey Rourke, Gwyneth Paltrow,Don Cheadle                 |              7 |   |   |
| David Schwimmer                  | Clive Owen, Catherine Keener, Liana Liberato,Jason Clarke                     |              7 |   |   |
| Kenneth Branagh                  | Chris Hemsworth, Anthony Hopkins, Natalie Portman, Tom Hiddleston             |              7 |   |   |
| Greg Mottola                     | Simon Pegg, Nick Frost, Seth Rogen, Mia Stallard                              |              7 |   |   |
| Lone Scherfig                    | Anne Hathaway, Jim Sturgess, Patricia Clarkson,Tom Mison                      |              7 |   |   |
| Ridley Scott                     | Noomi Rapace, Logan Marshall-Green, Michael Fassbender, Charlize Theron       |              7 |   |   |
| Drew Goddard                     | Kristen Connolly, Chris Hemsworth, Anna Hutchison,Fran Kranz                  |              7 |   |   |
| Marc Webb                        | Andrew Garfield, Emma Stone, Rhys Ifans, Irrfan Khan                          |              7 |   |   |
| Christopher McQuarrie            | Tom Cruise, Rosamund Pike, Richard Jenkins, Werner Herzog                     |              7 |   |   |
| Seth MacFarlane                  | Mark Wahlberg, Mila Kunis, Seth MacFarlane, Joel McHale                       |              7 |   |   |
| Guillermo del Toro               | Idris Elba, Charlie Hunnam, Rinko Kikuchi,Charlie Day                         |              7 |   |   |
| Alan Taylor                      | Chris Hemsworth, Natalie Portman, Tom Hiddleston,Stellan Skarsgård            |              7 |   |   |
| Rawson Marshall Thurber          | Jason Sudeikis, Jennifer Aniston, Emma Roberts, Ed Helms                      |              7 |   |   |
| Lars von Trier                   | Charlotte Gainsbourg, Stellan Skarsgård, Stacy Martin, Shia LaBeouf           |              7 |   |   |
| Joseph Kosinski                  | Tom Cruise, Morgan Freeman, Andrea Riseborough, Olga Kurylenko                |              7 |   |   |
| Bong Joon Ho                     | Chris Evans, Jamie Bell, Tilda Swinton, Ed Harris                             |              7 |   |   |
| Marc Forster                     | Brad Pitt, Mireille Enos, Daniella Kertesz, James Badge Dale                  |              7 |   |   |
| Edgar Wright                     | Simon Pegg, Nick Frost, Martin Freeman, Rosamund Pike                         |              7 |   |   |
| Danny Boyle                      | James McAvoy, Rosario Dawson, Vincent Cassel,Danny Sapani                     |              7 |   |   |
| Robert Stromberg                 | Angelina Jolie, Elle Fanning, Sharlto Copley,Lesley Manville                  |              7 |   |   |
| Colin Trevorrow                  | Chris Pratt, Bryce Dallas Howard, Ty Simpkins,Judy Greer                      |              7 |   |   |
| Brian Helgeland                  | Tom Hardy, Emily Browning, Taron Egerton, Paul Anderson                       |              7 |   |   |
| Kenneth Branagh                  | Lily James, Cate Blanchett, Richard Madden,Helena Bonham Carter               |              7 |   |   |
| Tom Hooper                       | Eddie Redmayne, Alicia Vikander, Amber Heard, Ben Whishaw                     |              7 |   |   |
| Jeremy Saulnier                  | Anton Yelchin, Imogen Poots, Alia Shawkat,Patrick Stewart                     |              7 |   |   |
| Jean-Marc Vallée                 | Jake Gyllenhaal, Naomi Watts, Chris Cooper,Judah Lewis                        |              7 |   |   |
| Morten Tyldum                    | Jennifer Lawrence, Chris Pratt, Michael Sheen,Laurence Fishburne              |              7 |   |   |
| Lone Scherfig                    | Gemma Arterton, Sam Claflin, Bill Nighy, Jack Huston                          |              7 |   |   |
| Duncan Jones                     | Travis Fimmel, Paula Patton, Ben Foster, Dominic Cooper                       |              7 |   |   |
| Ben Wheatley                     | Sharlto Copley, Brie Larson, Armie Hammer, Cillian Murphy                     |              7 |   |   |
| Andrea Arnold                    | Sasha Lane, Shia LaBeouf, Riley Keough, McCaul Lombardi                       |              7 |   |   |
| Richard Linklater                | Blake Jenner, Tyler Hoechlin, Ryan Guzman,Zoey Deutch                         |              7 |   |   |
| Antonio Campos                   | Rebecca Hall, Michael C. Hall, Tracy Letts, Maria Dizzia                      |              7 |   |   |
| Patricia Riggen                  | Jennifer Garner, Kylie Rogers, Martin Henderson,Brighton Sharbino             |              7 |   |   |
| Ridley Scott                     | Russell Crowe, Abbie Cornish, Albert Finney, Marion Cotillard                 |            6.9 |   |   |
| J.J. Abrams                      | Tom Cruise, Michelle Monaghan, Ving Rhames, Philip Seymour Hoffman            |            6.9 |   |   |
| Steven Soderbergh                | George Clooney, Brad Pitt, Matt Damon,Michael Mantell                         |            6.9 |   |   |
| Adam McKay                       | Will Ferrell, John C. Reilly, Mary Steenburgen,Richard Jenkins                |            6.9 |   |   |
| Albert Hughes                    | Denzel Washington, Mila Kunis, Ray Stevenson, Gary Oldman                     |            6.9 |   |   |
| Joe Johnston                     | Chris Evans, Hugo Weaving, Samuel L. Jackson,Hayley Atwell                    |            6.9 |   |   |
| Seth Gordon                      | Jason Bateman, Charlie Day, Jason Sudeikis, Steve Wiebe                       |            6.9 |   |   |
| Jaume Collet-Serra               | Liam Neeson, Diane Kruger, January Jones,Aidan Quinn                          |            6.9 |   |   |
| Carlos Saldanha                  | Jesse Eisenberg, Anne Hathaway, George Lopez,Karen Disher                     |            6.9 |   |   |
| Jon Kasdan                       | Dylan O'Brien, Britt Robertson, Victoria Justice, James Frecheville           |            6.9 |   |   |
| Denis Villeneuve                 | Jake Gyllenhaal, Mélanie Laurent, Sarah Gadon,Isabella Rossellini             |            6.9 |   |   |
| Jonathan Levine                  | Nicholas Hoult, Teresa Palmer, John Malkovich,Analeigh Tipton                 |            6.9 |   |   |
| David Robert Mitchell            | Maika Monroe, Keir Gilchrist, Olivia Luccardi,Lili Sepe                       |            6.9 |   |   |
| Chris Evans                      | Chris Evans, Alice Eve, Emma Fitzpatrick, John Cullum                         |            6.9 |   |   |
| Scott Cooper                     | Johnny Depp, Benedict Cumberbatch, Dakota Johnson, Joel Edgerton              |            6.9 |   |   |
| Neill Blomkamp                   | Sharlto Copley, Dev Patel, Hugh Jackman,Sigourney Weaver                      |            6.9 |   |   |
| Ron Howard                       | Chris Hemsworth, Cillian Murphy, Brendan Gleeson,Ben Whishaw                  |            6.9 |   |   |
| Kyle Patrick Alvarez             | Ezra Miller, Tye Sheridan, Billy Crudup, Olivia Thirlby                       |            6.9 |   |   |
| Antoine Fuqua                    | Denzel Washington, Chris Pratt, Ethan Hawke,Vincent D'Onofrio                 |            6.9 |   |   |
| Nicholas Stoller                 | Andy Samberg, Katie Crown,Kelsey Grammer, Jennifer Aniston                    |            6.9 |   |   |
| Stephen Frears                   | Meryl Streep, Hugh Grant, Simon Helberg, Rebecca Ferguson                     |            6.9 |   |   |
| James Schamus                    | Logan Lerman, Sarah Gadon, Tijuana Ricks, Sue Dahlman                         |            6.9 |   |   |
| Hideaki Anno                     | Hiroki Hasegawa, Yutaka Takenouchi,Satomi Ishihara, Ren Ôsugi                 |            6.9 |   |   |

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



