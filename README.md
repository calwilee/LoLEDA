datatable: true 
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

```py
filepath = Path('data') / '2022lol.csv' 
lol_2022 = pd.read_csv(filepath)
lol_2022
```
We can see that `lol_2022` contains 149400 rows that has information about each player during a game and 123 columns that describes different attributes of the game. Let's look at what the columns of `lol_2022` are.
```py
print(lol_2022.columns.tolist())
['gameid', 'datacompleteness', 'url', 'league', 'year', 'split', 'playoffs', 'date', 'game', 'patch', 'participantid', 'side', 'position', 'playername', 'playerid', 'teamname', 'teamid', 'champion', 'ban1', 'ban2', 'ban3', 'ban4', 'ban5', 'gamelength', 'result', 'kills', 'deaths', 'assists', 'teamkills', 'teamdeaths', 'doublekills', 'triplekills', 'quadrakills', 'pentakills', 'firstblood', 'firstbloodkill', 'firstbloodassist', 'firstbloodvictim', 'team kpm', 'ckpm', 'firstdragon', 'dragons', 'opp_dragons', 'elementaldrakes', 'opp_elementaldrakes', 'infernals', 'mountains', 'clouds', 'oceans', 'chemtechs', 'hextechs', 'dragons (type unknown)', 'elders', 'opp_elders', 'firstherald', 'heralds', 'opp_heralds', 'firstbaron', 'barons', 'opp_barons', 'firsttower', 'towers', 'opp_towers', 'firstmidtower', 'firsttothreetowers', 'turretplates', 'opp_turretplates', 'inhibitors', 'opp_inhibitors', 'damagetochampions', 'dpm', 'damageshare', 'damagetakenperminute', 'damagemitigatedperminute', 'wardsplaced', 'wpm', 'wardskilled', 'wcpm', 'controlwardsbought', 'visionscore', 'vspm', 'totalgold', 'earnedgold', 'earned gpm', 'earnedgoldshare', 'goldspent', 'gspd', 'total cs', 'minionkills', 'monsterkills', 'monsterkillsownjungle', 'monsterkillsenemyjungle', 'cspm', 'goldat10', 'xpat10', 'csat10', 'opp_goldat10', 'opp_xpat10', 'opp_csat10', 'golddiffat10', 'xpdiffat10', 'csdiffat10', 'killsat10', 'assistsat10', 'deathsat10', 'opp_killsat10', 'opp_assistsat10', 'opp_deathsat10', 'goldat15', 'xpat15', 'csat15', 'opp_goldat15', 'opp_xpat15', 'opp_csat15', 'golddiffat15', 'xpdiffat15', 'csdiffat15', 'killsat15', 'assistsat15', 'deathsat15', 'opp_killsat15', 'opp_assistsat15', 'opp_deathsat15']
```

Upon looking at this list, we can see that not every columns will be useful to answering our question. The ones we are interested in are `'league'`, `'gameid'`, `'teamname'`, `'ban1'`, `'ban2'`, `'ban3'`, `'ban4'`, `'ban5'`, `'champion'`, and `'result'`. 

- `'league'`(str): The league/tournament the game took place
- `'gameid'`(str): The game's id
- `'teamname'`(str): The name of the team playing during the match
- `'ban1'`(str): The name of the champion that was banned first
- `'ban2'`(str): The name of the champion that was banned second
- `'ban3'`(str): The name of the champion that was banned third
- `'ban4'`(str): The name of the champion that was banned fourth
- `'ban5'`(str): The name of the champion that was banned fifth
- `'champion'`(str): The name of the champion the player is playing
- `'result'`(int): The result of the match (0 = Team lost, 1 = Team won)

```py
lol_2022 = lol_2022[[ "league", "gameid", "teamname", "ban1", "ban2", "ban3", "ban4", "ban5", "champion", "result"]]
lol_2022
```

| league   | gameid                | teamname                      | ban1    | ...   | ban5   | champion   |   result |
|:---------|:----------------------|:------------------------------|:--------|:------|:-------|:-----------|---------:|
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | Renekton   |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | Xin Zhao   |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | LeBlanc    |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | Samira     |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | Leona      |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | Gragas     |        1 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | Viego      |        1 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | Viktor     |        1 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | Jinx       |        1 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | Alistar    |        1 |
| LCKC     | ESPORTSTMNT01_2690210 | Fredit BRION Challengers      | Karma   | ...   | Lulu   | nan        |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | Nongshim RedForce Challengers | Lee Sin | ...   | Rell   | nan        |        1 |


## Cleaning and EDA
![cute poros :D](/images/trsnsiont2.webp)
Before we can start answering the question, we need to clean the data and extract any information that might be useful to us.
### Data Cleaning

For this analysis, we are going to be focusing on tier-one leagues, Worlds, and MSI. Tier-one leagues consists of the best players and teams playing in tournaments in their region. For example, LCS is the tier-one competition in the US and LPL is the one for China. Worlds is the big tournament that takes place sometimes during October to November where the best teams globally compete against each other for the world. MSI is the is the Mid-Spring Invitational where multiple teams, usually teams from tier-one leagues, around the world complete against one another similar to worlds. 

We chose to focus on these leagues in particular since the players that make up the teams in each of these tournaments are considered the best of the best and are mostly likely to have the highest game knowledge. Due to the professional coaching staff and resources these teams have, they are likely to be on par with one another with little variation in comparison to a tier-one league team vs a low-level team.
```py
"""
Finds the rows associated with tier-one leagues, Worlds, or MSI using the `.loc` method
"""
lol_2022 = lol_2022.loc[(lol_2022['league'] == 'LCK') |
          (lol_2022['league'] == 'LPL') |
          (lol_2022['league'] == 'LEC') |
          (lol_2022['league'] == 'LCS') |
          (lol_2022['league'] == 'PCS') |
          (lol_2022['league'] == 'VCS') |
          (lol_2022['league'] == 'LJL') |
          (lol_2022['league'] == 'CBLOL') |
          (lol_2022['league'] == 'LLA') |
          (lol_2022['league'] == 'MSI') |
          (lol_2022['league'] == 'WLDs')]

lol_2022
```

| league   | gameid           | teamname           | ban1     | ...   | ban5    | champion   |   result |
|:---------|:-----------------|:-------------------|:---------|:------|:--------|:-----------|---------:|
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Gwen       |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Jarvan IV  |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Syndra     |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Jinx       |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Nautilus   |        1 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Jax        |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Xin Zhao   |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Vex        |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Aphelios   |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Thresh     |        0 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | nan        |        1 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | nan        |        0 |

We can see from looking at the ban columns in the above DataFrame that there appears to be rows that are repeating. The reason this is happening is because most of the rows represents a player in the game. Since there are 5 players per team and the team has the same bans, all of the columns except for `'champion'` will have repeated values. Our goal now is to combine these repeated rows into one so that we can easily access information about what a team chose in every game and the results of that choice. In order to do that, we need to combine the information in `'champion'` into a single value so that when we aggregate, it won't cause problems. 

Upon further invesigation, we find that some of the values in `'champion'` are missing. When looking into the data, we can see that there are actually summary rows that summarize the results of the match and the statistics of each team. In order to combine the values in `'champion'` into a single value, we will drop these summary rows.

```py
"""
Drops the rows with null values in the 'champion' column by querying for the values that aren't nan
"""

no_summary = lol_2022[lol_2022["champion"].isna() == False]

no_summary
```

| league   | gameid           | teamname           | ban1     | ...   | ban5    | champion   |   result |
|:---------|:-----------------|:-------------------|:---------|:------|:--------|:-----------|---------:|
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Gwen       |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Jarvan IV  |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Syndra     |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Jinx       |        1 |
| LPL      | 8401-8401_game_1 | Oh My God          | Renekton | ...   | Camille | Nautilus   |        1 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Jax        |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Xin Zhao   |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Vex        |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Aphelios   |        0 |
| LPL      | 8401-8401_game_1 | ThunderTalk Gaming | Samira   | ...   | Rumble  | Thresh     |        0 |


Next we'll define an custom aggregation function to combine the 5 champions each team played into a single value by putting them into a list. 

```py
def combine_champion(series):
    return series.tolist()
```
After that, we'll use a groupby function to index `no_summary` by `'league'`, `'gameid'`, and `'teamname'` and then aggregate the champion column so that we can get one value for all of the champions a team played during each game in a specific league.

```py
champions_played = no_summary.groupby(["league", "gameid", "teamname"])[["champion"]].agg(combine_champion)

champions_played
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>champion</th>
    </tr>
    <tr>
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">CBLOL</th>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695708</th>
      <th>FURIA</th>
      <td>[Akali, Xin Zhao, Orianna, Jhin, Leona]</td>
    </tr>
    <tr>
      <th>LOUD</th>
      <td>[Renekton, Viego, Corki, Aphelios, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695774</th>
      <th>Flamengo Esports</th>
      <td>[Gwen, Xin Zhao, Orianna, Jhin, Maokai]</td>
    </tr>
    <tr>
      <th>Netshoes Miners</th>
      <td>[Tryndamere, Viego, Vex, Kai'Sa, Leona]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695807</th>
      <th>INTZ</th>
      <td>[Gwen, Xin Zhao, LeBlanc, Sivir, Karma]</td>
    </tr>
    <tr>
      <th>KaBuM! e-Sports</th>
      <td>[Graves, Lee Sin, Viktor, Caitlyn, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695835</th>
      <th>RED Canids</th>
      <td>[Gwen, Xin Zhao, Akali, Samira, Rell]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>[Gragas, Viego, Corki, Ezreal, Yuumi]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2696159</th>
      <th>Liberty</th>
      <td>[Graves, Jarvan IV, Zoe, Caitlyn, Lux]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>[Jayce, Viego, Viktor, Jhin, Karma]</td>
    </tr>
  </tbody>
</table>

An additional thing to note is that this DataFrame confirms that the previous missing values in `'champions'` was caused by the summary rows. `champions_play` reveals that out DataFrame contains information on the teams playing in 3,275 games. When we multiply 6,550 by 5 to account for the fact that there are 5 players, we get 32750, which is the same as the amount of rows we have in `no_summary`.

Once we combine all of the champions a team played into a single value, we will now work on removing the repeating ban rows. We'll approach this like how we approached champions by defining a custom aggregation function and then using a groupby to combine everything together. 

```py
def combine_bans(series):
    # Grabs first element of each group since all elements in the group are repeating
    return series.iloc[0]
```
```py
#Aggregates each game and the teams playing in that game into two rows representing each team, their bans, and who won. 

bans_per_team = lol_2022.groupby(["league", "gameid", "teamname"])[["ban1", "ban2", "ban3", "ban4", "ban5", "result"]].agg(combine_bans)

bans_per_team
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>ban1</th>
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
      <th>ban5</th>
      <th>result</th>
    </tr>
    <tr>
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="12" valign="top">CBLOL</th>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695708</th>
      <th>FURIA</th>
      <td>Lee Sin</td>
      <td>Thresh</td>
      <td>Twisted Fate</td>
      <td>Kai'Sa</td>
      <td>Caitlyn</td>
      <td>0</td>
    </tr>
    <tr>
      <th>LOUD</th>
      <td>Gwen</td>
      <td>Diana</td>
      <td>Jinx</td>
      <td>Vex</td>
      <td>Tryndamere</td>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695774</th>
      <th>Flamengo Esports</th>
      <td>Nidalee</td>
      <td>Corki</td>
      <td>Diana</td>
      <td>Lee Sin</td>
      <td>Jayce</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Netshoes Miners</th>
      <td>Jinx</td>
      <td>Twisted Fate</td>
      <td>Caitlyn</td>
      <td>Viktor</td>
      <td>Syndra</td>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695807</th>
      <th>INTZ</th>
      <td>Corki</td>
      <td>Jayce</td>
      <td>Akali</td>
      <td>Kennen</td>
      <td>Jax</td>
      <td>0</td>
    </tr>
    <tr>
      <th>KaBuM! e-Sports</th>
      <td>Ziggs</td>
      <td>Renekton</td>
      <td>Twisted Fate</td>
      <td>Jhin</td>
      <td>Ezreal</td>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2695835</th>
      <th>RED Canids</th>
      <td>Thresh</td>
      <td>Caitlyn</td>
      <td>Jinx</td>
      <td>Braum</td>
      <td>Karma</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Lee Sin</td>
      <td>Leona</td>
      <td>Twisted Fate</td>
      <td>Nautilus</td>
      <td>Rakan</td>
      <td>0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2696159</th>
      <th>Liberty</th>
      <td>Twisted Fate</td>
      <td>Leona</td>
      <td>Vex</td>
      <td>LeBlanc</td>
      <td>Akali</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Gwen</td>
      <td>Corki</td>
      <td>Thresh</td>
      <td>Camille</td>
      <td>Renekton</td>
      <td>0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_2696199</th>
      <th>LOUD</th>
      <td>Gwen</td>
      <td>Lee Sin</td>
      <td>Diana</td>
      <td>Camille</td>
      <td>Jarvan IV</td>
      <td>0</td>
    </tr>
    <tr>
      <th>RED Canids</th>
      <td>Thresh</td>
      <td>Viktor</td>
      <td>Corki</td>
      <td>Zoe</td>
      <td>Jax</td>
      <td>1</td>
    </tr>
  </tbody>
</table>


We will now merge our `champions_played` DataFrame with our `bans_per_team` DataFrame to create one big DataFrame called `bans_and_champions` that contains the information we have so far.

```py
bans_and_champions = bans_per_team.merge(champions_played, left_index = True, right_index = True, how = "inner")
bans_and_champions
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>ban1</th>
      <th>...</th>
      <th>ban5</th>
      <th>result</th>
      <th>champion</th>
    </tr>
    <tr>
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">CBLOL</th>
      <th rowspan="2" valign="top">ESP...</th>
      <th>FURIA</th>
      <td>Lee Sin</td>
      <td>...</td>
      <td>Caitlyn</td>
      <td>0</td>
      <td>[Akali, Xin Zhao, Orianna, Jhin, Leona]</td>
    </tr>
    <tr>
      <th>LOUD</th>
      <td>Gwen</td>
      <td>...</td>
      <td>Tryndamere</td>
      <td>1</td>
      <td>[Renekton, Viego, Corki, Aphelios, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESP...</th>
      <th>Flamengo Esports</th>
      <td>Nidalee</td>
      <td>...</td>
      <td>Jayce</td>
      <td>0</td>
      <td>[Gwen, Xin Zhao, Orianna, Jhin, Maokai]</td>
    </tr>
    <tr>
      <th>Netshoes Miners</th>
      <td>Jinx</td>
      <td>...</td>
      <td>Syndra</td>
      <td>1</td>
      <td>[Tryndamere, Viego, Vex, Kai'Sa, Leona]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESP...</th>
      <th>INTZ</th>
      <td>Corki</td>
      <td>...</td>
      <td>Jax</td>
      <td>0</td>
      <td>[Gwen, Xin Zhao, LeBlanc, Sivir, Karma]</td>
    </tr>
    <tr>
      <th>KaBuM! e-Sports</th>
      <td>Ziggs</td>
      <td>...</td>
      <td>Ezreal</td>
      <td>1</td>
      <td>[Graves, Lee Sin, Viktor, Caitlyn, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESP...</th>
      <th>RED Canids</th>
      <td>Thresh</td>
      <td>...</td>
      <td>Karma</td>
      <td>1</td>
      <td>[Gwen, Xin Zhao, Akali, Samira, Rell]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Lee Sin</td>
      <td>...</td>
      <td>Rakan</td>
      <td>0</td>
      <td>[Gragas, Viego, Corki, Ezreal, Yuumi]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESP...</th>
      <th>Liberty</th>
      <td>Twisted Fate</td>
      <td>...</td>
      <td>Akali</td>
      <td>1</td>
      <td>[Graves, Jarvan IV, Zoe, Caitlyn, Lux]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Gwen</td>
      <td>...</td>
      <td>Renekton</td>
      <td>0</td>
      <td>[Jayce, Viego, Viktor, Jhin, Karma]</td>
    </tr>
  </tbody>
</table>

Now we have all the necessary information to move on to the first step of answering our question, determining who are the most banned champions in our dataset. First, we need to determine which champions were banned and the amount of times they were.

```py
ban_amount = bans_and_champions[["ban1", "ban2", "ban3", "ban4", "ban5"]].stack().value_counts()

ban_amount
```
1.Zeri            1608
2.Gwen            1097
3.Kalista         1074
4.Ahri             984
5.LeBlanc          906
6.Lucian           885
7.Twisted Fate     798
8.Sylas            790
9.Caitlyn          776
10.Lee Sin          748

We can see from `bans` that a total of 144 champions were banned in `bans_and_champions` and that certain champions were banned way more than others. In order to get a better idea of the distribution of bans, we will use a bar chart to graph the number of times a champion was banned.

<iframe src="assets/Number_of_bans_per_champ.html" width=700 height=500 frameBorder=0></iframe>




|   num_top_banned |        0 |        1 |        2 |          3 |          4 |
|-----------------:|---------:|---------:|---------:|-----------:|-----------:|
|                0 | 0.52459  | 0.552326 | 0.644444 |   0.588235 |   0.444444 |
|                1 | 0.468085 | 0.509954 | 0.586558 |   0.567073 |   0.473684 |
|                2 | 0.451115 | 0.485774 | 0.520958 |   0.532338 |   0.612903 |
|                3 | 0.45045  | 0.456753 | 0.489855 |   0.48913  |   0.722222 |
|                4 | 0.427273 | 0.453988 | 0.549451 |   0.458333 |   1        |
|                5 | 0.368421 | 0.692308 | 0.285714 | nan        | nan        |
