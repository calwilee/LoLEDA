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

```py
filepath = Path('data') / '2022lol.csv' 
lol_2022 = pd.read_csv(filepath)
lol_2022
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gameid</th>
      <th>datacompleteness</th>
      <th>url</th>
      <th>league</th>
      <th>year</th>
      <th>split</th>
      <th>playoffs</th>
      <th>date</th>
      <th>game</th>
      <th>patch</th>
      <th>participantid</th>
      <th>side</th>
      <th>position</th>
      <th>playername</th>
      <th>playerid</th>
      <th>teamname</th>
      <th>teamid</th>
      <th>champion</th>
      <th>ban1</th>
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
      <th>ban5</th>
      <th>gamelength</th>
      <th>result</th>
      <th>kills</th>
      <th>deaths</th>
      <th>assists</th>
      <th>teamkills</th>
      <th>teamdeaths</th>
      <th>doublekills</th>
      <th>triplekills</th>
      <th>quadrakills</th>
      <th>pentakills</th>
      <th>firstblood</th>
      <th>firstbloodkill</th>
      <th>firstbloodassist</th>
      <th>firstbloodvictim</th>
      <th>team kpm</th>
      <th>ckpm</th>
      <th>firstdragon</th>
      <th>dragons</th>
      <th>opp_dragons</th>
      <th>elementaldrakes</th>
      <th>opp_elementaldrakes</th>
      <th>infernals</th>
      <th>mountains</th>
      <th>clouds</th>
      <th>oceans</th>
      <th>chemtechs</th>
      <th>hextechs</th>
      <th>dragons (type unknown)</th>
      <th>elders</th>
      <th>opp_elders</th>
      <th>firstherald</th>
      <th>heralds</th>
      <th>opp_heralds</th>
      <th>firstbaron</th>
      <th>barons</th>
      <th>opp_barons</th>
      <th>firsttower</th>
      <th>towers</th>
      <th>opp_towers</th>
      <th>firstmidtower</th>
      <th>firsttothreetowers</th>
      <th>turretplates</th>
      <th>opp_turretplates</th>
      <th>inhibitors</th>
      <th>opp_inhibitors</th>
      <th>damagetochampions</th>
      <th>dpm</th>
      <th>damageshare</th>
      <th>damagetakenperminute</th>
      <th>damagemitigatedperminute</th>
      <th>wardsplaced</th>
      <th>wpm</th>
      <th>wardskilled</th>
      <th>wcpm</th>
      <th>controlwardsbought</th>
      <th>visionscore</th>
      <th>vspm</th>
      <th>totalgold</th>
      <th>earnedgold</th>
      <th>earned gpm</th>
      <th>earnedgoldshare</th>
      <th>goldspent</th>
      <th>gspd</th>
      <th>total cs</th>
      <th>minionkills</th>
      <th>monsterkills</th>
      <th>monsterkillsownjungle</th>
      <th>monsterkillsenemyjungle</th>
      <th>cspm</th>
      <th>goldat10</th>
      <th>xpat10</th>
      <th>csat10</th>
      <th>opp_goldat10</th>
      <th>opp_xpat10</th>
      <th>opp_csat10</th>
      <th>golddiffat10</th>
      <th>xpdiffat10</th>
      <th>csdiffat10</th>
      <th>killsat10</th>
      <th>assistsat10</th>
      <th>deathsat10</th>
      <th>opp_killsat10</th>
      <th>opp_assistsat10</th>
      <th>opp_deathsat10</th>
      <th>goldat15</th>
      <th>xpat15</th>
      <th>csat15</th>
      <th>opp_goldat15</th>
      <th>opp_xpat15</th>
      <th>opp_csat15</th>
      <th>golddiffat15</th>
      <th>xpdiffat15</th>
      <th>csdiffat15</th>
      <th>killsat15</th>
      <th>assistsat15</th>
      <th>deathsat15</th>
      <th>opp_killsat15</th>
      <th>opp_assistsat15</th>
      <th>opp_deathsat15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>1</td>
      <td>Blue</td>
      <td>top</td>
      <td>Soboro</td>
      <td>oe:player:38e0af7278d6769d0c81d7c4b47ac1e</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>Renekton</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>15768.0</td>
      <td>552.2942</td>
      <td>0.278784</td>
      <td>1072.3993</td>
      <td>777.7933</td>
      <td>8.0</td>
      <td>0.2802</td>
      <td>6.0</td>
      <td>0.2102</td>
      <td>5.0</td>
      <td>26.0</td>
      <td>0.9107</td>
      <td>10934</td>
      <td>7164.0</td>
      <td>250.9282</td>
      <td>0.253859</td>
      <td>10275.0</td>
      <td>NaN</td>
      <td>231.0</td>
      <td>220.0</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.0911</td>
      <td>3228.0</td>
      <td>4909.0</td>
      <td>89.0</td>
      <td>3176.0</td>
      <td>4953.0</td>
      <td>81.0</td>
      <td>52.0</td>
      <td>-44.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5025.0</td>
      <td>7560.0</td>
      <td>135.0</td>
      <td>4634.0</td>
      <td>7215.0</td>
      <td>121.0</td>
      <td>391.0</td>
      <td>345.0</td>
      <td>14.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>2</td>
      <td>Blue</td>
      <td>jng</td>
      <td>Raptor</td>
      <td>oe:player:637ed20b1e41be1c51bd1a4cb211357</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>Xin Zhao</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>2</td>
      <td>5</td>
      <td>6</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>11765.0</td>
      <td>412.0841</td>
      <td>0.208009</td>
      <td>944.2732</td>
      <td>650.1576</td>
      <td>6.0</td>
      <td>0.2102</td>
      <td>18.0</td>
      <td>0.6305</td>
      <td>6.0</td>
      <td>48.0</td>
      <td>1.6813</td>
      <td>9138</td>
      <td>5368.0</td>
      <td>188.0210</td>
      <td>0.190220</td>
      <td>8750.0</td>
      <td>NaN</td>
      <td>148.0</td>
      <td>33.0</td>
      <td>115.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.1839</td>
      <td>3429.0</td>
      <td>3484.0</td>
      <td>58.0</td>
      <td>2944.0</td>
      <td>3052.0</td>
      <td>63.0</td>
      <td>485.0</td>
      <td>432.0</td>
      <td>-5.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>5366.0</td>
      <td>5320.0</td>
      <td>89.0</td>
      <td>4825.0</td>
      <td>5595.0</td>
      <td>100.0</td>
      <td>541.0</td>
      <td>-275.0</td>
      <td>-11.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>3</td>
      <td>Blue</td>
      <td>mid</td>
      <td>Feisty</td>
      <td>oe:player:d1ae0e2f9f3ac1e0e0cdcb86504ca77</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>LeBlanc</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>14258.0</td>
      <td>499.4046</td>
      <td>0.252086</td>
      <td>581.6462</td>
      <td>227.7758</td>
      <td>19.0</td>
      <td>0.6655</td>
      <td>7.0</td>
      <td>0.2452</td>
      <td>7.0</td>
      <td>29.0</td>
      <td>1.0158</td>
      <td>9715</td>
      <td>5945.0</td>
      <td>208.2312</td>
      <td>0.210665</td>
      <td>8725.0</td>
      <td>NaN</td>
      <td>193.0</td>
      <td>177.0</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.7601</td>
      <td>3283.0</td>
      <td>4556.0</td>
      <td>81.0</td>
      <td>3121.0</td>
      <td>4485.0</td>
      <td>81.0</td>
      <td>162.0</td>
      <td>71.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>5118.0</td>
      <td>6942.0</td>
      <td>120.0</td>
      <td>5593.0</td>
      <td>6789.0</td>
      <td>119.0</td>
      <td>-475.0</td>
      <td>153.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>4</td>
      <td>Blue</td>
      <td>bot</td>
      <td>Gamin</td>
      <td>oe:player:998b3e49b01ecc41eacc392477a98cf</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>Samira</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>11106.0</td>
      <td>389.0018</td>
      <td>0.196358</td>
      <td>463.8529</td>
      <td>218.8792</td>
      <td>12.0</td>
      <td>0.4203</td>
      <td>6.0</td>
      <td>0.2102</td>
      <td>4.0</td>
      <td>25.0</td>
      <td>0.8757</td>
      <td>10605</td>
      <td>6835.0</td>
      <td>239.4046</td>
      <td>0.242201</td>
      <td>10425.0</td>
      <td>NaN</td>
      <td>226.0</td>
      <td>208.0</td>
      <td>18.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.9159</td>
      <td>3600.0</td>
      <td>3103.0</td>
      <td>78.0</td>
      <td>3304.0</td>
      <td>2838.0</td>
      <td>90.0</td>
      <td>296.0</td>
      <td>265.0</td>
      <td>-12.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5461.0</td>
      <td>4591.0</td>
      <td>115.0</td>
      <td>6254.0</td>
      <td>5934.0</td>
      <td>149.0</td>
      <td>-793.0</td>
      <td>-1343.0</td>
      <td>-34.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>5</td>
      <td>Blue</td>
      <td>sup</td>
      <td>Loopy</td>
      <td>oe:player:e9741b3a238723ea6380ef2113fae63</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>Leona</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>6</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3663.0</td>
      <td>128.3012</td>
      <td>0.064763</td>
      <td>475.0263</td>
      <td>490.1226</td>
      <td>29.0</td>
      <td>1.0158</td>
      <td>14.0</td>
      <td>0.4904</td>
      <td>11.0</td>
      <td>69.0</td>
      <td>2.4168</td>
      <td>6678</td>
      <td>2908.0</td>
      <td>101.8564</td>
      <td>0.103054</td>
      <td>6395.0</td>
      <td>NaN</td>
      <td>42.0</td>
      <td>42.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.4711</td>
      <td>2678.0</td>
      <td>2161.0</td>
      <td>16.0</td>
      <td>2150.0</td>
      <td>2748.0</td>
      <td>15.0</td>
      <td>528.0</td>
      <td>-587.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>3836.0</td>
      <td>3588.0</td>
      <td>28.0</td>
      <td>3393.0</td>
      <td>4085.0</td>
      <td>21.0</td>
      <td>443.0</td>
      <td>-497.0</td>
      <td>7.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>6</td>
      <td>Red</td>
      <td>top</td>
      <td>DnDn</td>
      <td>oe:player:341e10748bb6d388250fd1f013e45a4</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>Gragas</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>12</td>
      <td>19</td>
      <td>9</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>17455.0</td>
      <td>611.3835</td>
      <td>0.218428</td>
      <td>911.8739</td>
      <td>1210.2977</td>
      <td>15.0</td>
      <td>0.5254</td>
      <td>2.0</td>
      <td>0.0701</td>
      <td>8.0</td>
      <td>30.0</td>
      <td>1.0508</td>
      <td>10001</td>
      <td>6231.0</td>
      <td>218.2487</td>
      <td>0.184530</td>
      <td>9750.0</td>
      <td>NaN</td>
      <td>229.0</td>
      <td>221.0</td>
      <td>8.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.0210</td>
      <td>3176.0</td>
      <td>4953.0</td>
      <td>81.0</td>
      <td>3228.0</td>
      <td>4909.0</td>
      <td>89.0</td>
      <td>-52.0</td>
      <td>44.0</td>
      <td>-8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4634.0</td>
      <td>7215.0</td>
      <td>121.0</td>
      <td>5025.0</td>
      <td>7560.0</td>
      <td>135.0</td>
      <td>-391.0</td>
      <td>-345.0</td>
      <td>-14.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>7</td>
      <td>Red</td>
      <td>jng</td>
      <td>Sylvie</td>
      <td>oe:player:1a75a7cf8c98442be881fed562346f5</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>Viego</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>10</td>
      <td>19</td>
      <td>9</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>10564.0</td>
      <td>370.0175</td>
      <td>0.132195</td>
      <td>838.6690</td>
      <td>530.4378</td>
      <td>8.0</td>
      <td>0.2802</td>
      <td>17.0</td>
      <td>0.5954</td>
      <td>19.0</td>
      <td>39.0</td>
      <td>1.3660</td>
      <td>10293</td>
      <td>6523.0</td>
      <td>228.4764</td>
      <td>0.193177</td>
      <td>8750.0</td>
      <td>NaN</td>
      <td>183.0</td>
      <td>47.0</td>
      <td>136.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.4098</td>
      <td>2944.0</td>
      <td>3052.0</td>
      <td>63.0</td>
      <td>3429.0</td>
      <td>3484.0</td>
      <td>58.0</td>
      <td>-485.0</td>
      <td>-432.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>4825.0</td>
      <td>5595.0</td>
      <td>100.0</td>
      <td>5366.0</td>
      <td>5320.0</td>
      <td>89.0</td>
      <td>-541.0</td>
      <td>275.0</td>
      <td>11.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>8</td>
      <td>Red</td>
      <td>mid</td>
      <td>FIESTA</td>
      <td>oe:player:5ee64eb3feb02e60832a2265db54f71</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>Viktor</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>6</td>
      <td>3</td>
      <td>12</td>
      <td>19</td>
      <td>9</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>20690.0</td>
      <td>724.6935</td>
      <td>0.258910</td>
      <td>531.6287</td>
      <td>426.9352</td>
      <td>15.0</td>
      <td>0.5254</td>
      <td>4.0</td>
      <td>0.1401</td>
      <td>6.0</td>
      <td>29.0</td>
      <td>1.0158</td>
      <td>11532</td>
      <td>7762.0</td>
      <td>271.8739</td>
      <td>0.229868</td>
      <td>8900.0</td>
      <td>NaN</td>
      <td>216.0</td>
      <td>196.0</td>
      <td>20.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.5657</td>
      <td>3121.0</td>
      <td>4485.0</td>
      <td>81.0</td>
      <td>3283.0</td>
      <td>4556.0</td>
      <td>81.0</td>
      <td>-162.0</td>
      <td>-71.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>5593.0</td>
      <td>6789.0</td>
      <td>119.0</td>
      <td>5118.0</td>
      <td>6942.0</td>
      <td>120.0</td>
      <td>475.0</td>
      <td>-153.0</td>
      <td>-1.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>9</td>
      <td>Red</td>
      <td>bot</td>
      <td>vital</td>
      <td>oe:player:252de481e83ab0bc87aada93aeb424c</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>Jinx</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>10</td>
      <td>19</td>
      <td>9</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>26687.0</td>
      <td>934.7461</td>
      <td>0.333955</td>
      <td>385.0088</td>
      <td>186.6550</td>
      <td>9.0</td>
      <td>0.3152</td>
      <td>21.0</td>
      <td>0.7356</td>
      <td>2.0</td>
      <td>40.0</td>
      <td>1.4011</td>
      <td>14018</td>
      <td>10248.0</td>
      <td>358.9492</td>
      <td>0.303486</td>
      <td>12800.0</td>
      <td>NaN</td>
      <td>319.0</td>
      <td>299.0</td>
      <td>20.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.1734</td>
      <td>3304.0</td>
      <td>2838.0</td>
      <td>90.0</td>
      <td>3600.0</td>
      <td>3103.0</td>
      <td>78.0</td>
      <td>-296.0</td>
      <td>-265.0</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>6254.0</td>
      <td>5934.0</td>
      <td>149.0</td>
      <td>5461.0</td>
      <td>4591.0</td>
      <td>115.0</td>
      <td>793.0</td>
      <td>1343.0</td>
      <td>34.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>10</td>
      <td>Red</td>
      <td>sup</td>
      <td>Blessing</td>
      <td>oe:player:f1347562011016753e18334ffe7a5c9</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>Alistar</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>18</td>
      <td>19</td>
      <td>9</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4516.0</td>
      <td>158.1786</td>
      <td>0.056512</td>
      <td>342.4869</td>
      <td>518.0035</td>
      <td>46.0</td>
      <td>1.6112</td>
      <td>7.0</td>
      <td>0.2452</td>
      <td>10.0</td>
      <td>67.0</td>
      <td>2.3468</td>
      <td>6773</td>
      <td>3003.0</td>
      <td>105.1839</td>
      <td>0.088939</td>
      <td>5650.0</td>
      <td>NaN</td>
      <td>29.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0158</td>
      <td>2150.0</td>
      <td>2748.0</td>
      <td>15.0</td>
      <td>2678.0</td>
      <td>2161.0</td>
      <td>16.0</td>
      <td>-528.0</td>
      <td>587.0</td>
      <td>-1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>3393.0</td>
      <td>4085.0</td>
      <td>21.0</td>
      <td>3836.0</td>
      <td>3588.0</td>
      <td>28.0</td>
      <td>-443.0</td>
      <td>497.0</td>
      <td>-7.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>100</td>
      <td>Blue</td>
      <td>team</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Fredit BRION Challengers</td>
      <td>oe:team:68911b3329146587617ab2973106e23</td>
      <td>NaN</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>1713</td>
      <td>0</td>
      <td>9</td>
      <td>19</td>
      <td>19</td>
      <td>9</td>
      <td>19</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.3152</td>
      <td>0.9807</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>56560.0</td>
      <td>1981.0858</td>
      <td>NaN</td>
      <td>3537.1979</td>
      <td>2364.7285</td>
      <td>74.0</td>
      <td>2.5919</td>
      <td>51.0</td>
      <td>1.7863</td>
      <td>33.0</td>
      <td>197.0</td>
      <td>6.9002</td>
      <td>47070</td>
      <td>28222.0</td>
      <td>988.5114</td>
      <td>NaN</td>
      <td>44570.0</td>
      <td>-0.028312</td>
      <td>NaN</td>
      <td>680.0</td>
      <td>160.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>29.4221</td>
      <td>16218.0</td>
      <td>18213.0</td>
      <td>322.0</td>
      <td>14695.0</td>
      <td>18076.0</td>
      <td>330.0</td>
      <td>1523.0</td>
      <td>137.0</td>
      <td>-8.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>24806.0</td>
      <td>28001.0</td>
      <td>487.0</td>
      <td>24699.0</td>
      <td>29618.0</td>
      <td>510.0</td>
      <td>107.0</td>
      <td>-1617.0</td>
      <td>-23.0</td>
      <td>5.0</td>
      <td>10.0</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>ESPORTSTMNT01_2690210</td>
      <td>complete</td>
      <td>NaN</td>
      <td>LCKC</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 07:44:08</td>
      <td>1</td>
      <td>12.01</td>
      <td>200</td>
      <td>Red</td>
      <td>team</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Nongshim RedForce Challengers</td>
      <td>oe:team:d2dc3681437e2beb2bb4742477108ff</td>
      <td>NaN</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>1713</td>
      <td>1</td>
      <td>19</td>
      <td>9</td>
      <td>62</td>
      <td>19</td>
      <td>9</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.6655</td>
      <td>0.9807</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>79912.0</td>
      <td>2799.0193</td>
      <td>NaN</td>
      <td>3009.6673</td>
      <td>2872.3292</td>
      <td>93.0</td>
      <td>3.2574</td>
      <td>51.0</td>
      <td>1.7863</td>
      <td>45.0</td>
      <td>205.0</td>
      <td>7.1804</td>
      <td>52617</td>
      <td>33769.0</td>
      <td>1182.8021</td>
      <td>NaN</td>
      <td>45850.0</td>
      <td>0.028312</td>
      <td>NaN</td>
      <td>792.0</td>
      <td>184.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>34.1856</td>
      <td>14695.0</td>
      <td>18076.0</td>
      <td>330.0</td>
      <td>16218.0</td>
      <td>18213.0</td>
      <td>322.0</td>
      <td>-1523.0</td>
      <td>-137.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>24699.0</td>
      <td>29618.0</td>
      <td>510.0</td>
      <td>24806.0</td>
      <td>28001.0</td>
      <td>487.0</td>
      <td>-107.0</td>
      <td>1617.0</td>
      <td>23.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>10.0</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>

`lol_2022` contains 149400 rows that has information about each player during a game and 123 columns that describes different attributes of the game. Let's look at what the columns of `lol_2022` are.
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

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th>ban1</th>
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
      <th>ban5</th>
      <th>champion</th>
      <th>result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>Renekton</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>Xin Zhao</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>LeBlanc</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>Samira</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>Leona</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>Gragas</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>Viego</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>Viktor</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>Jinx</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>Alistar</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Fredit BRION Challengers</td>
      <td>Karma</td>
      <td>Caitlyn</td>
      <td>Syndra</td>
      <td>Thresh</td>
      <td>Lulu</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCKC</td>
      <td>ESPORTSTMNT01_2690210</td>
      <td>Nongshim RedForce Challengers</td>
      <td>Lee Sin</td>
      <td>Twisted Fate</td>
      <td>Zoe</td>
      <td>Nautilus</td>
      <td>Rell</td>
      <td>NaN</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

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

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th>ban1</th>
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
      <th>ban5</th>
      <th>champion</th>
      <th>result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Gwen</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Jarvan IV</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Syndra</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Jinx</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Nautilus</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Jax</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Xin Zhao</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Vex</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Aphelios</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Thresh</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>NaN</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

We can see from looking at the ban columns in the above DataFrame that there appears to be rows that are repeating. The reason this is happening is because most of the rows represents a player in the game. Since there are 5 players per team and the team has the same bans, all of the columns except for `'champion'` will have repeated values. Our goal now is to combine these repeated rows into one so that we can easily access information about what a team chose in every game and the results of that choice. In order to do that, we need to combine the information in `'champion'` into a single value so that when we aggregate, it won't cause problems. 

Upon further invesigation, we find that some of the values in `'champion'` are missing. When looking into the data, we can see that there are actually summary rows that summarize the results of the match and the statistics of each team. In order to combine the values in `'champion'` into a single value, we will drop these summary rows.

```py
"""
Drops the rows with null values in the 'champion' column by querying for the values that aren't nan
"""

no_summary = lol_2022[lol_2022["champion"].isna() == False]

no_summary
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th>ban1</th>
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
      <th>ban5</th>
      <th>champion</th>
      <th>result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Gwen</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Jarvan IV</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Syndra</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Jinx</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>Oh My God</td>
      <td>Renekton</td>
      <td>Lee Sin</td>
      <td>Caitlyn</td>
      <td>Jayce</td>
      <td>Camille</td>
      <td>Nautilus</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Jax</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Xin Zhao</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Vex</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Aphelios</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8401-8401_game_1</td>
      <td>ThunderTalk Gaming</td>
      <td>Samira</td>
      <td>Diana</td>
      <td>Akali</td>
      <td>LeBlanc</td>
      <td>Rumble</td>
      <td>Thresh</td>
      <td>0</td>
    </tr>
  </tbody>
</table>


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
    <tr>
      <th>league</th>
      <th>gameid</th>
      <th>teamname</th>
      <th>champion</th>
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
      <th>ban2</th>
      <th>ban3</th>
      <th>ban4</th>
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
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">CBLOL</th>
      <th rowspan="2" valign="top">ESPORTSTMNT01_26...</th>
      <th>FURIA</th>
      <td>Lee Sin</td>
      <td>Thresh</td>
      <td>Twisted Fate</td>
      <td>Kai'Sa</td>
      <td>Caitlyn</td>
      <td>0</td>
      <td>[Akali, Xin Zhao, Orianna, Jhin, Leona]</td>
    </tr>
    <tr>
      <th>LOUD</th>
      <td>Gwen</td>
      <td>Diana</td>
      <td>Jinx</td>
      <td>Vex</td>
      <td>Tryndamere</td>
      <td>1</td>
      <td>[Renekton, Viego, Corki, Aphelios, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_26...</th>
      <th>Flamengo Esports</th>
      <td>Nidalee</td>
      <td>Corki</td>
      <td>Diana</td>
      <td>Lee Sin</td>
      <td>Jayce</td>
      <td>0</td>
      <td>[Gwen, Xin Zhao, Orianna, Jhin, Maokai]</td>
    </tr>
    <tr>
      <th>Netshoes Miners</th>
      <td>Jinx</td>
      <td>Twisted Fate</td>
      <td>Caitlyn</td>
      <td>Viktor</td>
      <td>Syndra</td>
      <td>1</td>
      <td>[Tryndamere, Viego, Vex, Kai'Sa, Leona]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_26...</th>
      <th>INTZ</th>
      <td>Corki</td>
      <td>Jayce</td>
      <td>Akali</td>
      <td>Kennen</td>
      <td>Jax</td>
      <td>0</td>
      <td>[Gwen, Xin Zhao, LeBlanc, Sivir, Karma]</td>
    </tr>
    <tr>
      <th>KaBuM! e-Sports</th>
      <td>Ziggs</td>
      <td>Renekton</td>
      <td>Twisted Fate</td>
      <td>Jhin</td>
      <td>Ezreal</td>
      <td>1</td>
      <td>[Graves, Lee Sin, Viktor, Caitlyn, Nautilus]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_26...</th>
      <th>RED Canids</th>
      <td>Thresh</td>
      <td>Caitlyn</td>
      <td>Jinx</td>
      <td>Braum</td>
      <td>Karma</td>
      <td>1</td>
      <td>[Gwen, Xin Zhao, Akali, Samira, Rell]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Lee Sin</td>
      <td>Leona</td>
      <td>Twisted Fate</td>
      <td>Nautilus</td>
      <td>Rakan</td>
      <td>0</td>
      <td>[Gragas, Viego, Corki, Ezreal, Yuumi]</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ESPORTSTMNT01_26...</th>
      <th>Liberty</th>
      <td>Twisted Fate</td>
      <td>Leona</td>
      <td>Vex</td>
      <td>LeBlanc</td>
      <td>Akali</td>
      <td>1</td>
      <td>[Graves, Jarvan IV, Zoe, Caitlyn, Lux]</td>
    </tr>
    <tr>
      <th>Rensga eSports</th>
      <td>Gwen</td>
      <td>Corki</td>
      <td>Thresh</td>
      <td>Camille</td>
      <td>Renekton</td>
      <td>0</td>
      <td>[Jayce, Viego, Viktor, Jhin, Karma]</td>
    </tr>
  </tbody>
</table>

Now we have all the necessary information to move on to the first step of answering our question, determining who are the most banned champions in our dataset. First, we need to determine which champions were banned and the amount of times they were.

```py
ban_amount = bans_and_champions[["ban1", "ban2", "ban3", "ban4", "ban5"]].stack().value_counts()

ban_amount[:10]
```
1. Zeri            1608
2. Gwen            1097
3. Kalista         1074
4. Ahri             984
5. LeBlanc          906
6. Lucian           885
7. Twisted Fate     798
8. Sylas            790
9. Caitlyn          776
10. Lee Sin          748

We can see from `bans` that a total of 144 champions were banned in `bans_and_champions` and that certain champions were banned way more than others. In order to get a better idea of the distribution of bans, we will use a bar chart to graph the number of times a champion was banned.

<div class="table-wrapper" markdown="block">

<iframe src="assets/Number_of_bans_per_champ.html" width=750 height=500 frameBorder=0></iframe>

</div>

We can see that there is a huge pool of champions that were banned, to the point we can't even see all of the champion names on the x-axis. However, we can also notice that a good chunk of the distribution comes from a certain top percentage of the bans. There is a certain point where the next champion in the ban distribution won't contribute much. Now we must determine our cutoff point for the most banned.

By looking at the graph, we can determine that there are drops in the graph. One possible reason behind these drops are that each of the drops are associated with the amount of bans they spend banning the most banned champions. It is more likely that a team may ban a few of the most powerful champions and then spend the rest of their bans banning champions that the other team may be good at. As the team starts banning more champions, they are more likely to start tailoring their bans to the opponent rather than the current game environment. 

Taking this into consideration, we will looking into the first 5 drops to represent the 5 bans each team gets. The following graph shows what we consider the first 5 drops to be and a zoom in of those first 5 drops.

<div class="table-wrapper" markdown="block">

<iframe src="assets/withline.html" width=750 height=500 frameBorder=0></iframe>

</div>

<div class="table-wrapper" markdown="block">

<iframe src="assets/first_five_drops.html" width=750 height=500 frameBorder=0></iframe>

</div>

We can see that from the graph that these champions are in the top 15 of `ban_amount`. Coincidentally, this is associated with the top 10% of `ban_amount`. Let's see the percentage of bans these champions make up.

```py
top_bans.sum() / ban_amount.sum()  = 0.39743119266055044
```
When we calculate the total amount of bans and the number of bans within the top 15, we can see that they make up almost 40% of the bans. 

Therefore, we will set the `top_bans` to be the top 15 or 10% of `ban_amount`.

Now that we've determined who makes up the most banned champions, we will now figure out how many of those champions teams banned per game and record that data into our DataFrame in a new column called `'num_top_banned'`. We'll accomplish this by defining a function that counts the number of times a team banned a champion in `top_bans` and then apply that to the DataFrame.



