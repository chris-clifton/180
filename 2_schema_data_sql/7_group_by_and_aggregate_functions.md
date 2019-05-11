# Write query that turns film year into decade and gets average of each decade
``` SELECT year / 10 * 10 as decade, ROUND(AVG(duration)) as average_duration FROM films GROUP BY decade ORDER BY decade; ```

# string_agg string aggregate
- Return list of comma separated values
``` SELECT year / 10 * 10 AS decade, genre, string_agg(title, ', ') AS films FROM films GROUP BY decade, genre ORDER BY decade, genre;```
 decade |   genre   |                  films
--------+-----------+------------------------------------------
   1940 | drama     | Casablanca
   1950 | drama     | 12 Angry Men
   1950 | scifi     | 1984
   1970 | crime     | The Godfather
   1970 | thriller  | The Conversation
   1980 | action    | Die Hard
   1980 | comedy    | Hairspray
   1990 | comedy    | Home Alone, The Birdcage, Wayne's World
   1990 | scifi     | Godzilla
   2000 | espionage | Bourne Identity
   2000 | horror    | 28 Days Later
   2010 | espionage | Tinker Tailor Soldier Spy
   2010 | scifi     | Midnight Special, Interstellar, Godzilla
(13 rows)

