![lolimg](/images/lolbanner.jpeg)
## Introduction
League of Legends is a 5v5 multiplayer online battle arena. Each player fulfills one of 5 roles (Top, Mid, ADC, Support, and Jungle) and has the objective of destroying the enemy team's Nexus. Since its release, League of Legends has become one of the most played games in the world, ranking 5th overall for the [most popular PC games by monthly active users](https://newzoo.com/resources/rankings/top-20-pc-games){:target="_blank"}. 

Along with being one of the most popular games globally, League of Legends is also the world's largest [esport](https://en.wikipedia.org/wiki/Esports){:target="_blank"}. During League of Legends esport tournaments, each player on both teams has the chance to ban a champion. When a champion is banned, they are removed from the pool of available champions and cannot be selected. Since each player can ban a champion, there are a total of 10 bans per game. During tournaments some champions are more banned than others. This leads us to our question:

### If a team doesn't ban the most banned champions, are they more likely to lose?


We want to see the impact a champion's presence, or lack thereof, can have on the results of the match. Depending on our results, viewers of these tournaments can potentially predict the outcome of the match before it even starts and the teams playing in them can be better informed on the importance of their bans and better decide who to ban.
   
In order to answer this question, we'll use a permutation test to analyze whether banning a commonly banned champion yields a higher win rate than not banning one. Before we get to that, we will clean the data, perform an EDA, and assess and determine what to do about the missing data.

For this project, we are going to look at Oracle's Elixer's League of Legends Competitive Matches data from 2022. 

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

`lol_2022` contains 149400 rows that have information about each player during a game and 123 columns that describe different attributes of the game. Let's look at what the columns of `lol_2022` are.
```py
print(lol_2022.columns.tolist())
['gameid', 'datacompleteness', 'url', 'league', 'year', 'split', 'playoffs', 'date', 'game', 'patch', 'participantid', 'side', 'position', 'playername', 'playerid', 'teamname', 'teamid', 'champion', 'ban1', 'ban2', 'ban3', 'ban4', 'ban5', 'gamelength', 'result', 'kills', 'deaths', 'assists', 'teamkills', 'teamdeaths', 'doublekills', 'triplekills', 'quadrakills', 'pentakills', 'firstblood', 'firstbloodkill', 'firstbloodassist', 'firstbloodvictim', 'team kpm', 'ckpm', 'firstdragon', 'dragons', 'opp_dragons', 'elementaldrakes', 'opp_elementaldrakes', 'infernals', 'mountains', 'clouds', 'oceans', 'chemtechs', 'hextechs', 'dragons (type unknown)', 'elders', 'opp_elders', 'firstherald', 'heralds', 'opp_heralds', 'firstbaron', 'barons', 'opp_barons', 'firsttower', 'towers', 'opp_towers', 'firstmidtower', 'firsttothreetowers', 'turretplates', 'opp_turretplates', 'inhibitors', 'opp_inhibitors', 'damagetochampions', 'dpm', 'damageshare', 'damagetakenperminute', 'damagemitigatedperminute', 'wardsplaced', 'wpm', 'wardskilled', 'wcpm', 'controlwardsbought', 'visionscore', 'vspm', 'totalgold', 'earnedgold', 'earned gpm', 'earnedgoldshare', 'goldspent', 'gspd', 'total cs', 'minionkills', 'monsterkills', 'monsterkillsownjungle', 'monsterkillsenemyjungle', 'cspm', 'goldat10', 'xpat10', 'csat10', 'opp_goldat10', 'opp_xpat10', 'opp_csat10', 'golddiffat10', 'xpdiffat10', 'csdiffat10', 'killsat10', 'assistsat10', 'deathsat10', 'opp_killsat10', 'opp_assistsat10', 'opp_deathsat10', 'goldat15', 'xpat15', 'csat15', 'opp_goldat15', 'opp_xpat15', 'opp_csat15', 'golddiffat15', 'xpdiffat15', 'csdiffat15', 'killsat15', 'assistsat15', 'deathsat15', 'opp_killsat15', 'opp_assistsat15', 'opp_deathsat15']
```

Upon looking at this list, we can see that not every columns will be useful to answering our question. We are interested in are `league`, `gameid`, `teamname`, `ban1`, `ban2`, `ban3`, `ban4`, `ban5`, `champion`, and `result`. 

- `league`(str): The league/tournament the game took place
- `gameid`(str): The game's id
- `teamname`(str): The name of the team playing during the match
- `ban1`(str): The name of the champion that was banned first
- `ban2`(str): The name of the champion that was banned second
- `ban3`(str): The name of the champion that was banned third
- `ban4`(str): The name of the champion that was banned fourth
- `ban5`(str): The name of the champion that was banned fifth
- `champion`(str): The name of the champion the player is playing
- `result`(int): The result of the match (0 = Team lost, 1 = Team won)

We filter our DataFrame to contain only these columns:

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

## Data Cleaning and Analysis
![cute poros :D](/images/trsnsiont2.webp)
Before we begin analysis, we must first clean, organize and aggregate our data.

> Region Filtration

For this analysis, we are going to be focusing on tier-one leagues, Worlds, and MSI, since these leagues contain the best players and highest quality gameplay. We filter for these leagues in our DataFrame rows

> Dropping Summary Rows

If we take a look at our DataFrame, we notice it contains two summary rows for each match. We will drop these rows in order to combine values in `champion`.

> Correcting Result Column

We renamed the `result` column to `win` and converted it to type bool, as we thought this would make more sense intuitively. 

> Grouping and Aggregations

In order to create a DataFrame containing information about champions played and banned per match, we created two DataFrames. For both DataFrames, we grouped by `league`, `gameid`, and `teamname`. In the first DataFrame we created a custom aggregation to combine the champions played for each team into a list. As for the second DataFrame, we aggregate by the first series value to get champions banned, as this value is repeated for each match. We then performed an inner merge between the two DataFrames together by index. 

> Finding the Most Banned Champions

Using our DataFrame from the previous step, we counted how many times each champion was banned and sorted by count. 

These were the top 15 most banned champions and their ban counts:
1. Zeri: 1608
2. Gwen: 1097
3. Kalista: 1074
4. Ahri: 984
5. LeBlanc: 906
6. Lucian: 885
7. Twisted Fate: 798
8. Sylas: 790
9. Caitlyn: 776
10. Lee Sin: 748
11. Wukong: 697
12. Yuumi: 693
13. Ryze: 650
14. Poppy: 648
15. Renata Glasc: 642

We consider a champion to be a "top ban" if it is in the top 15 most banned champions. We chose to set 15 as our cutoff, as the top 15 champions banned make up 40% of the total bans. 

> Adding a `num_top_banned` and `num_top_drafted` column 

Using a custom function, we then count how many times a top ban was banned in each match from our merged DataFrame, and add it to a `num_top_banned` column. Using a similar aggregation function, we count how many times a top ban was drafted, and add it to a `num_top_drafted` column and reset the index of our DataFrame. 

Here are the first 10 rows of our cleaned DataFrame!

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
      <th>win</th>
      <th>champion</th>
      <th>num_top_banned</th>
      <th>num_top_drafted</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695708</td>
      <td>FURIA</td>
      <td>Lee Sin</td>
      <td>Thresh</td>
      <td>Twisted Fate</td>
      <td>Kai'Sa</td>
      <td>Caitlyn</td>
      <td>False</td>
      <td>[Akali, Xin Zhao, Orianna, Jhin, Leona]</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695708</td>
      <td>LOUD</td>
      <td>Gwen</td>
      <td>Diana</td>
      <td>Jinx</td>
      <td>Vex</td>
      <td>Tryndamere</td>
      <td>True</td>
      <td>[Renekton, Viego, Corki, Aphelios, Nautilus]</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695774</td>
      <td>Flamengo Esports</td>
      <td>Nidalee</td>
      <td>Corki</td>
      <td>Diana</td>
      <td>Lee Sin</td>
      <td>Jayce</td>
      <td>False</td>
      <td>[Gwen, Xin Zhao, Orianna, Jhin, Maokai]</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695774</td>
      <td>Netshoes Miners</td>
      <td>Jinx</td>
      <td>Twisted Fate</td>
      <td>Caitlyn</td>
      <td>Viktor</td>
      <td>Syndra</td>
      <td>True</td>
      <td>[Tryndamere, Viego, Vex, Kai'Sa, Leona]</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695807</td>
      <td>INTZ</td>
      <td>Corki</td>
      <td>Jayce</td>
      <td>Akali</td>
      <td>Kennen</td>
      <td>Jax</td>
      <td>False</td>
      <td>[Gwen, Xin Zhao, LeBlanc, Sivir, Karma]</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695807</td>
      <td>KaBuM! e-Sports</td>
      <td>Ziggs</td>
      <td>Renekton</td>
      <td>Twisted Fate</td>
      <td>Jhin</td>
      <td>Ezreal</td>
      <td>True</td>
      <td>[Graves, Lee Sin, Viktor, Caitlyn, Nautilus]</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695835</td>
      <td>RED Canids</td>
      <td>Thresh</td>
      <td>Caitlyn</td>
      <td>Jinx</td>
      <td>Braum</td>
      <td>Karma</td>
      <td>True</td>
      <td>[Gwen, Xin Zhao, Akali, Samira, Rell]</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2695835</td>
      <td>Rensga eSports</td>
      <td>Lee Sin</td>
      <td>Leona</td>
      <td>Twisted Fate</td>
      <td>Nautilus</td>
      <td>Rakan</td>
      <td>False</td>
      <td>[Gragas, Viego, Corki, Ezreal, Yuumi]</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2696159</td>
      <td>Liberty</td>
      <td>Twisted Fate</td>
      <td>Leona</td>
      <td>Vex</td>
      <td>LeBlanc</td>
      <td>Akali</td>
      <td>True</td>
      <td>[Graves, Jarvan IV, Zoe, Caitlyn, Lux]</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <td>CBLOL</td>
      <td>ESPORTSTMNT01_2696159</td>
      <td>Rensga eSports</td>
      <td>Gwen</td>
      <td>Corki</td>
      <td>Thresh</td>
      <td>Camille</td>
      <td>Renekton</td>
      <td>False</td>
      <td>[Jayce, Viego, Viktor, Jhin, Karma]</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

## Univariate Analysis

Now that we have our cleaned DataFrame, let's take a look at generally how many top bans a team bans. We can do so by plotting a histogram.

<div class="table-wrapper" markdown="block">

<iframe src="assets/numfreqbanned.html" width=725 height=500 frameBorder=0></iframe>

</div>

We can see that most teams ban 1 - 3 top bans during a match. Very rarely do teams use all their bans on top bans. 

## Bivariate Analysis

Let's take a look at the average win rate per number of top bans banned. We utilize `num_top_banned` and `win`.
<div class="table-wrapper" markdown="block">

<iframe src="assets/winratepernumbanned.html" width=725 height=500 frameBorder=0></iframe>

</div>

It seems like the more a team bans a "top ban" the more likely they are to lose! This is a bit counterintuitive, as one would think that banning more powerful champions would lead to higher win rate. However, we have yet to consider the fact that just because a champion wasn't banned doesn't mean that they were played. If no one chose to play that champion, it would be as if they were banned from the game.

Let's take a look at how a top ban's presence in a team's draft impacts win rate. We can find the number of top bans present in `champion` and find the mean win rate per number of top bans present in a team. 

<div class="table-wrapper" markdown="block">

<iframe src="assets/topbanpresentinteam.html" width=725 height=500 frameBorder=0></iframe>

</div>

This graph tells a very different story than our previous one. It seems that if a team drafts a "top ban" then their chances of winning increase! This makes sense, as top bans should be strong champions, helping to increace the overall strength of a team. 

## Interesting Aggregates

In our bivariate analysis, we analyzed the relationship between banning a top ban and win rate, and drafting a top ban and win rate. Let's explore the relationship between `num_top_banned`, `num_top_drafted`, and win rate. The idea behind this is to look at what happens when a team chooses to ban a certain number of champions from `top_bans` and when they decide to play a certain number of them. 

To do so we can utilize a pivot table that shows the mean win rate for each value of `num_top_banned` conditioned on the values of `num_top_drafted`. Essentially, our pivot table shows the mean win rate given `x` number of top bans banned, and `y` number of top bans drafted.

To ensure proper sample size, we only considered scenarios where there were at least 5 games played.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>num_top_drafted</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
    <tr>
      <th>num_top_banned</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.524590</td>
      <td>0.552326</td>
      <td>0.644444</td>
      <td>0.588235</td>
      <td>0.444444</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.468085</td>
      <td>0.509954</td>
      <td>0.586558</td>
      <td>0.567073</td>
      <td>0.473684</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.451115</td>
      <td>0.485774</td>
      <td>0.520958</td>
      <td>0.532338</td>
      <td>0.612903</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.450450</td>
      <td>0.456753</td>
      <td>0.489855</td>
      <td>0.489130</td>
      <td>0.722222</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.427273</td>
      <td>0.453988</td>
      <td>0.549451</td>
      <td>0.458333</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.368421</td>
      <td>0.692308</td>
      <td>0.285714</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

It appears the fewer top bans a team bans, and the more a team drafts top bans, the greater the team's win rate. However, it is important to note that this is not always true. For instance, banning 0 top bans and drafting 4 seems to be an exception. 

In addition to that, there are times where when a team chooses too much from top_bans, their win rate also goes down. This could imply that there are other factors at play here outside the scope of our analysis that impacts the chances of a team winning. Another reason behind these discrepancies is that there is not as much data on these scenarios, so the win rate varies more.

## Assessment of Missingness 
![caitlyndetective](images/missingness.webp)

## NMAR Analysis
Before performing hypothesis testing, we need to first deal with missing values. We can begin by generating a dictionary containing the number of missing values per column 

```py
{'league': 0,
 'gameid': 0,
 'teamname': 0,
 'ban1': 5,
 'ban2': 4,
 'ban3': 12,
 'ban4': 9,
 'ban5': 20,
 'win': 0,
 'champion': 0,
 'num_top_banned': 0,
 'top_ban_present': 0}
```
All of our data that is missing is in a ban column. Perhaps this is because players chose to not ban a champion! Let's investigate further. 

Consider the match below:
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
      <th>win</th>
      <th>champion</th>
      <th>num_top_banned</th>
      <th>top_ban_present</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LCK</td>
      <td>ESPORTSTMNT01_2691557</td>
      <td>Fredit BRION</td>
      <td>Yuumi</td>
      <td>Caitlyn</td>
      <td>Twisted Fate</td>
      <td>Viktor</td>
      <td>Ryze</td>
      <td>False</td>
      <td>[Gragas, Xin Zhao, Corki, Varus, Karma]</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <td>LCK</td>
      <td>ESPORTSTMNT01_2691557</td>
      <td>T1</td>
      <td>Lee Sin</td>
      <td>Renekton</td>
      <td>NaN</td>
      <td>Camille</td>
      <td>LeBlanc</td>
      <td>True</td>
      <td>[Gwen, Jarvan IV, Vex, Aphelios, Lulu]</td>
      <td>2</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

If we take a look at the [recording](https://www.youtube.com/live/fbbsRe2eTLg?feature=shared&t=20375){:target="_blank"}, we can see that T1 did not ban a champion for their third slot! According to the announcers, players will sometimes ban no one because they want to leave a powerful champion available to be picked for their own team.  

Additionally, players sometimes forgo a ban because they see it as an opportunity to improve. Forcing oneself to go against some of the most powerful champions in the game can help players to learn how to counter such champions and improve.

Finally, there may be some misreports. Consider the match below: 

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
      <th>win</th>
      <th>champion</th>
      <th>num_top_banned</th>
      <th>top_ban_present</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LPL</td>
      <td>8473-8473_game_1</td>
      <td>JD Gaming</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>False</td>
      <td>[Gragas, Viego, Viktor, Zeri, Leona]</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>LPL</td>
      <td>8473-8473_game_1</td>
      <td>Top Esports</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>[Gnar, Lee Sin, Vex, Draven, Nautilus]</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

At first glance, it may appear no one on either team banned a champion. If we take a look at the [recording](https://www.twitch.tv/videos/1302904867?t=05h29m25s){:target="_blank"}, we can see that the teams did ban champions. Even though this occurrence would be a case of MCAR, it appears that the majority of the bans were correctly reported. As a result, we can conclude that the missing values in the ban columns are missing by design. When a player chooses not to ban a champion, there is no banned champion to report, so the data is missing. 

## Missingness Dependency

Although we have concluded that our data is missing by design, running analysis to see if the missigness is dependent on other columns can still prove valuable. Since `ban5` contains the most missing values, we will perform our analysis on this column. We will run permutation tests to see `ban5` is missing depending on both `gameid` and `ban1`.

> `ban5` and `gameid`

**Null Hypothesis:** The distribution of `gameid` when `ban5` is missing is about the same as the distribution of the `gameid` when `ban5` is not missing\
**Alternative Hypothesis:** The distribution of `gameid` when `ban5` is missing is different than the distribution of the `gameid` when `ban5` is not missing\
Test statistic: TVD between `gameid` and `ban5`, since `gameid` is categorical

<div class="table-wrapper" markdown="block">

<iframe src="assets/gameidvsban5.html" width=725 height=500 frameBorder=0></iframe>

</div>

We calculate a p-value of 0.0308. Since this is less than our significance level of .05, we reject the null, and conclude that the missingness of `ban5` is dependent on `gameid`. Essentially, whether or not a team forgoes their last ban is dependent on the game. 

Certain teams may be more comfortable forfeiting a ban depending on who they are up against. Forfeiting a ban is generally considered a bad idea. Since it isn't advisable to not use a ban, it may be the case that teams forfeit bans only in matches where they feel very confident against their opponent. As a result, teams may be more willing to forfeit a ban depending on the match up, making the missing data in `ban5` dependent on `gameid`.

> `ban5` and `ban1`

**Null Hypothesis:** The distribution of `ban1` when `ban5` is missing is about the same as the distribution of the `ban1` when `ban5` is not missing\
**Alternative Hypothesis:** The distribution of `ban1` when `ban5` is missing is different than the distribution of the `ban1` when `ban5` is not missing\
TVD between `ban1` and `ban5`, since `ban1` is categorical

<div class="table-wrapper" markdown="block">

<iframe src="assets/ban1vsban5.html" width=725 height=500 frameBorder=0></iframe>

</div>

We calculate a p-value of 0.0682. Since this is greater than our significance level of .05 we fail to reject the null, and conclude that the missingness of `ban5` is not dependent on `ban1`. Essentially, whether or not a team choses to forfeit their last ban is not dependent on their first ban. 

## Hypothesis Testing
![heimerdinger](images/heimer.webp)
Now that we've cleaned the data, performed an exploratory data analysis, and assessed the missing data in our dataset, we are now ready to answer our question.

We will perform a permutation test with a significance level of 0.05 and with the following null and alternate hypothesis:

**Null Hypothesis:** If a team doesn't ban at least 1 of the top banned champions, they have the same win rate as those who did ban at least 1 of the top banned champions.\\
**Alternate Hypothesis:** If a team doesn't ban at least 1 of the top banned champions, they have a lower win rate as those who did ban at least 1 of the top banned champions.\\

As for our test statistic, we will use the difference in means since we are interested in a direction and we can calculate the mean win rate depending on if at least one top champion was banned.

<div class="table-wrapper" markdown="block">

<iframe src="assets/permutationtestfinal.html" width=725 height=500 frameBorder=0></iframe>

</div>

We calculate a p-value of 0.0008. Since this is below our significance level of .05, we reject our null. From this we can say that the data suggests that banning at least one top ban leads to a lower win rate in comparison to teams that did not ban a top ban. Since League of Legends is such a complex game, we cannot fully attribute lower win rate to banning more top bans; too many confounding factors exist.


