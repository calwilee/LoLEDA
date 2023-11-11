![lolimg](/images/lolbanner.jpeg)
## Introduction
League of Legends is a multiplayer online battle arena released in 2009 where two teams of five players select champions to fight against each other. Each player fulfills one of 5 roles (Top, Mid, ADC, Support, and Jungle) and has the objective of destroying the enemy team's Nexus. Since its release, League of Legends has become one of the most played games in the world, ranking 5th overall for the [most popular PC games by monthly active users](https://newzoo.com/resources/rankings/top-20-pc-games) according to NewZoo. The game has over [150,000,000 registered players](https://prioridata.com/data/league-of-legends/#:~:text=With%20over%20150%20million%20registered,games%20worldwide%20as%20of%202023.) globally, many of who are still active today with over [125,000,000 players](https://activeplayer.io/league-of-legends/) having played League of Legends within the last 30 days. 

Along with being one of the most popular games globally, League of Legends is also the world's largest [esport](https://en.wikipedia.org/wiki/Esports). During League of Legends esport tournaments, each player on both teams has the chance to ban a champion. Whan a champion is banned, they are removed from the pool of available champions and cannot be selected. Since each player can ban a champion, there are a total of 10 bans per game. 

League of Legends is a very complex game, and is subject to balencing changes in order to create a fair and enjoyable experience for players. Characters may have their stats imporved or reduced, leading to some champions performing better than others. As a result, champions who have good stats or function well in an competitive enviorment are subject to being banned more often. This leads us to our question:

### If a team doesn't ban the most banned champions, are they more likely to lose?


We want to see the impact a champion's presence, or lack thereof, can have on the results of the match. Depending on our results, viewers of these tournaments can potentially predict the outcome of the match before it even starts and the teams playing in them can be better informed on the importance of their bans and better decide who to ban.
   
In order to answer this question, we'll use a (choose test) to (describe process). Before we get to that, we will clean the data, perform an EDA, and assess and determine what to do about the missing data.

For this project, we are going to look at Oracle's Elixer's League of Legends Competitive Matches data from 2022. This dataset onlines information about the overall stats of the game and the performance of the players/team across multiple matches and leagues. We have selected the 2022 dataset as it is complete; according to Oracle's Elixer,  datasets are updated once per day, so the 2023 dataset would be subject to daily updates before the season's end, and our analysis would quickly become outdated. By using 2022, we ensure that our analysis uses the most recent and complete dataset available right now.

We'll start by loading in the data as `lol_2022`.
![dataframe with uncleaned league of legends data](/images/uncleaneddf.png)
We can see that `lol_2022` contains 149400 rows that contain information about each player during a match and 123 columns that describes different attributes of the game. Let's take a look at what the columns of `lol_2022` are.

## Cleaning and EDA
`filepath = Path('data') / '2022lol.csv'
lol_2022 = pd.read_csv(filepath)
lol_2022`


|   num_top_banned |        0 |        1 |        2 |          3 |          4 |
|-----------------:|---------:|---------:|---------:|-----------:|-----------:|
|                0 | 0.52459  | 0.552326 | 0.644444 |   0.588235 |   0.444444 |
|                1 | 0.468085 | 0.509954 | 0.586558 |   0.567073 |   0.473684 |
|                2 | 0.451115 | 0.485774 | 0.520958 |   0.532338 |   0.612903 |
|                3 | 0.45045  | 0.456753 | 0.489855 |   0.48913  |   0.722222 |
|                4 | 0.427273 | 0.453988 | 0.549451 |   0.458333 |   1        |
|                5 | 0.368421 | 0.692308 | 0.285714 | nan        | nan        |
