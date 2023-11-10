![lolimg](/images/lolbanner.jpeg)

\
League of Legends is a multiplayer online battle arena that released in 2009 where two teams of five players select unique champions to fight against each other. Each player fulfills one of 5 roles (Top, Mid, ADC, Support, and Jungle) and has the objective of destroying the enemy team's Nexus. Since its release, League of Legends has become one of the most played games in the world, with it ranking 5th overall for the [most popular PC games by monthly active users](https://newzoo.com/resources/rankings/top-20-pc-games) according to NewZoo. The game has over [150,000,000 registered players](https://prioridata.com/data/league-of-legends/#:~:text=With%20over%20150%20million%20registered,games%20worldwide%20as%20of%202023.) globally, many of who are still active today with over [125,000,000 players](https://activeplayer.io/league-of-legends/) having played League of Legends within the last 30 days. 

Along with being one of the most popular games globally, League of Legends is also one of the most popular games in esports. [Esports](https://en.wikipedia.org/wiki/Esports) was created back in 1972 when Stanford University hosted a tournament for the game Spacewar and has grown into its own genre. During League of Legends esport tournaments, each player on both teams has the chance to ban a champion. Whan a champion is banned, they are removed from the pool of available champions and they cannot be played during the game. Since each player can ban a champion, there are a total of 10 bans per game. Certain champions perform better than others depending on the state of the game during the time, and there are spceific ones that are banned more often. This leads us to our question:

## H2 If a team doesn't ban the most banned champions, are they more likely to lose?


We are interested in exploring this question as we want to see the impact a champion's presence, or lack thereof, can have on the results of the match. Depending on our results, viewers of these tournaments can potentially predict the outcome of the match before it even starts and the teams playing in them can be better informed on the importance of their bans and better decide who to ban.
   
In order to answer this question, we'll use a (choose test) to (describe process). Before we get to that, we'll need to clean the data, perform an EDA, and assess and determine what to do about the missing data.

For this project, we are going to look at Oracle's Elixer's League of Legends Competitive Matches data from 2022. This dataset onlines information about the overall stats of the game and the performance of the players/team across multiple matches and leagues. We are choosing to use the 2022 dataset instead of the 2023 one because according to Oracle's Elixer, they update the data once per day, so if we were to use 2023 before the season's end, this analysis would quickly become outdated. By using 2022, we ensure that our analysis uses the most recent and complete dataset available right now.

We'll start by loading in the data as `lol_2022`.