# TFT-Set4-EDA

## Introduction

Over the past five months, I have been very obsessed with the game, 'Teamfight Tactics' (or for short, TFT). TFT is an 'autochess' based game where you compete against seven other players to build a board of units to defeat every other player. There's a lot to this game, which I don't really want to spend a lot of time to talk about in detail, so I may just summarise some important information in a list of dot points:
- The objective of the game is to buy different units from a shop, place them on your board to defeat your opponents (who are doing the same thing).
- There are only five units per shop, however, you can always spend 2 gold to refresh for a new shop
- Each unit has at least one 'Origin' and one 'Class'. Having multiple units sharing the same 'Origin' or 'Class' often strengthens your team with synergy bonuses. These will vary depending on the set
- Each unit has a certain cost to them, ranging from 1 to 5 gold. Higher cost units are (most of the time) stronger than lower cost units, but will be rarer at lower levels. 
- There is a leveling system, ranging from 1 to 9. Increasing your level also increases the number of units you are allowed to have on your board
- The odds of finding certain units depend on your current level.
- In addition there are a set number of units available in the total pool (depending on the cost of the unit). If the many people are hoarding the same unit, it is less likely for you to find that unit in your shop.
- You may also equip your units with items. There are 9 basic items which give your unit a certain boost in stats (attack, defense, spell power etc.)
- You can combine any two basic items to create a stronger item. There are a total of 45 of these items, each with their unique ability.

That's just some of the basic ideas of the game. There is a lot more to the game once you understand the basics, ranging from playstyles, game flow, composition structures and so on. A combination of all these ideas make the game extremely fun to play. 

<img src="images/5_moonlight.png"
     alt="Finally Hit Grandmaster!"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 1: An example of a team in TFT (Moonlight Hunters)__

## EDA
In the whole dataset collected, there are a total of 555 different games of TFT played over the course of about four months (from mid September to present). TFT is a game which regularly has balance patches to ensure that the 'best units', 'best compositions', and 'best items' don't stay constant, and will keep the compeitive side of the game more interesting. As a result, I have decided to limit my analysis to a single patch - 10.25 (spanning from December 9 2020 to January 5 2021). This patch was chosen because it was the longest span of time without balance patches (the balance team was on holidays). This also meant that I personally played a lot of games, making the findings more interesting. In addition, since the most recent balance patch (as of writing this blogpost) has not changed the meta too drastically, it may also help me with my climb to Grandmaster (UPDATE: It did help). 


### Sample data
Here's a sample of the dataset:

__Table 1: Sample of the Dataset__

|  | __Date__ | __Patch__ | __Account__ | __Starting Item__ | __Chosen__ | __Comp__ | __Place__ | __Rank__ | __LP__ | __LP Diff__ | __Winning Comp (if saw)__ | __Comment__ | __Week__ | __chosen_trait__ | __chosen_unit__ |
|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|-:|
| 527 | 2021-01-03 | 10.25 | phillipluong | Cloak | Duelist Yasuo | 6 Duelists | 5 | M1 | 366 | -10.0 | NaN | no yone :(; I probably should've rolled for yo... | 4 | Duelist | Yasuo |
| 528 | 2021-01-03 | 10.25 | phillipluong | Bow | Assassin Akali | Ninja Shade | 8 | M1 | 356 | -42.0 | NaN | that game felt so doomed; that kench did nothi... | 4 | Assassin | Akali |
| 529 | 2021-01-03 | 10.25 | phillipluong | Tear | Mystic Cassie | 4 Dusk 4 Sharpshooters | 7 | M1 | 314 | -27.0 | NaN | sold my fortune before I cashed out…............, | 4 | Mystic | Cassie |
| 530 | 2021-01-03 | 10.25 | phillipluong | Rod | Warlord Garen | 9 Warlords | 4 | M1 | 287 | 10.0 | NaN | NaN | 4 | Warlord | Garen |
| 531 | 2021-01-03 | 10.25 | phillipluong | Sword | none | Divine Hunters | 7 | M1 | 297 | -38.0 | NaN | should've gotten dazzler morgana; the items we... | 4 | none | none |


### Column Descriptions
There are a total of 15 columns in the data, comprising of the former 12 that were filled out as I played each game, and the latter 3 created for the analysis. I will now explain the details of these columns:

__Table 2: Dataset Column Descriptions__

| Col Name | Column Description | Data Type |
|:-|-|:-|
| Date | The date that the game was played | datetime64[ns] |
| Patch | The Balance Patch the game was played on | object |
| Account | Since I played 2 active accounts, I keep track of which of the two accounts I played on | object |
| Starting Item | What item did I start the game with | object |
| Chosen | The chosen unit I had by the end of the game | object |
| Comp | A brief description of the composition I ran | object |
| Place | My placement at the end of the game (ranging from 1st to 8th) | object |
| Rank | The Rank I was at during the game (Ranging from Iron 4 (I4) to Grandmaster (GM1) | object |
| LP | The amount of 'League Points' I was at before the game. This determines my overall rank | int64 |
| LP Diff | The change in my LP after I finished the game | float64 |
| Winning Comp (if saw) | I would sometimes write the winning composition if I followed the game until the end | object |
| Comment | A comment on the game (if I had one) | object |
| Week | Which week of the patch this game was played (week 1-4). This only applied for patch 10.25 since the patch ran for 4 weeks | int64 |
| chosen_trait | A specific breakdown of the trait (origin/class) of the chosen unit | object |
| chosen_unit | A specific breakdown of the chosen unit itself | object |


## Primary Statistics
Over the span of 4 weeks, a total of 134 games were played. All of these games were played on accounts that were of 'Masters' Rank or above (the top 0.36% of the playerbase). Through this time, my primary account, _phillipluong_, dropped from 430 League Points (LP) to 259 LP (mostly on the last day). Meanwhile, my secondary account, had increased from 144 LP to 404 LP. This means there was a total increase of 89 LP over the four week period (equivalent to two 1st place finishes). Over the 134 games, there were a fairly even amount of placements over the period.

<img src="images/main_placements.png"
     alt="Placements Over time"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 2: Overall Number of Placements in Patch 10.25__

Notably, there are far fewer 1st and 8th placements compared to all other rankings. I had a 8.96% win rate (12/134), which is much lower than the expected 12.5% winrate. Conversely, my loss rate was also 8.96%, which shows that I did quite well to prevent the maximal LP loss each game. Also of note, you always gain at least 10 LP for coming in the top 4. Over the four weeks, I had a 69/134 top 4 placement rate (51.49%), which is better than the expected rate. 

- Wins were mostly collected from playing: Dusk, Hunter Adept, Ninja Shade, and Legendary Comps. There was also 1 win from 9 elderwood. 
- Top 4 Comps also included: 9 Mages, Divine Hunters, Enlightened, Moonlight Reroll 

Here's a word cloud of my personal summary of the compositions I played. Since I consider myself a 'semi-flexible' player, the descriptions of my compositions will differ depending on the kind of units that appear in my shop. 

__Figure 3: A word cloud of the typical compositions I played during Patch 10.25__

<img src="images/compositions_word_cloud.png"
     alt="Composition Word Cloud"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

## Analysis based on weeks and Accounts

### Analysis each week

My gameplay wasn't always the same each week (hopefully, it's all in part of a steady improvement). Regardless, there were definitely some weeks where I performed better than others, as shown by these summary statistics:

__Table 3: Performance based on different weeks__

| Week No. | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| Week 1 | 43 | 6 (13.95%) | 25 (58.14%) | 4.16 (2.13) | 4 (3-6) | +202 |
| Week 2 | 23 | 1 (4.35%) | 12 (52.17%) | 4.65 (2.10) | 4 (3-6) | -40 |
| Week 3 | 40 | 4 (10%) | 23 (57.5%) | 4.08 (2.09) | 4 (2-6) | +239 |
| Week 4 | 28 | 1 (3.57%) | 9 (32.14%) | 5.32 (2.18) | 5.5 (4-7) | -312 |

On average, I played 33.5 games per week. Notably, I played more games and had a higher win rate on weeks 1 and 3, rather than weeks 2 and 4. In addition, I only had a higher than expected win rate in Week 1, at 13,95% (instead of the expected 12.5%). 

### Analysis based on Account

<img src="images/comparison_of_LP_by_accounts.png"
     alt="ILoveAnt after 300LP"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 4: A comparison of LP change by each account__

NOTE: The vertical green lines separate each of the weeks of the patch.

__Table 4: Performance based on different accounts__

| Account | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| phillipluong | 79 | 4 (5.06%) | 35 (44.30%) | 4.67 (2.04) | 5 (3-6) | -171 |
| ILoveAnt | 55 | 8 (14.55%) | 34 (61.82%) | 4.16 (2.28) | 4 (2.5-6) | +260 |

Overall, it appeared that my gameplay was better on the _ILoveAnt_ account rather than my primary account, _phillipluong_. Even with 24 fewer games, _ILoveAnt_, netted 4 more wins and essentially the same number of Top 4s. The mean placements of _ILoveAnt_ is also 0.51 lower than _phillipluong_. Finally, _ILoveAnt_ has gained 260 LP, whereas _phillipluong_ lost 171 LP. I believe that the clear reason may likely be because 'ILoveAnt' started off playing games against lower ranked users, thus increasing its odds of winning or appearing in the Top 4. Let's observe if this was indeed the case.

There was indeed a day where I played in the account 'phillipluong' and ran it all the way down, after I was about 1 game off hitting Grandmaster. Here are the details of my account if we remove that period. I am defining this as all the games before the 29th of December. 

<img src="images/phillipluong_before_boom.png"
     alt="phillipluong before I lost all the LP"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 5: Placements on _phillipluong_ before the loss streak__

__Table 5: Performance of _phillipluong_ before and during the loss streak__

| Account | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| phillipluong (before) | 55 | 3 (5.45%) | 27 (49.09%) | 4.44 (1.93) | 5 (3-6) | +53 |
| phillipluong (after) | 24 | 1 (4.17%) | 8 (33.33%) | 5.21 (2.25) | 5.5 (3.75-7) | -224 |

Based off this segmentation, the first 55 games played on _phillipluong_ indeed had a stronger performance compared to the last 24. The result of this is the net change in LP over the two time periods (+53 vs -224). The mean placement is also an exemplification of the LP change. Before 29/12, the mean placement of 4.44 netted a small gain of LP, while 5.21 ('far' greater) resulted in a great decrease in LP. 

If I removed the games 'ILoveAnt' played after hitting 300 LP, here are the results:

<img src="images/ILoveAnt_after_300LP.png"
     alt="ILoveAnt after 300LP"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 6: Placements of _ILoveAnt_ after hitting 300LP__

__Table 6: Performance of _ILoveAnt_ before and after 300LP__

| Account | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| ILoveAnt (before) | 20 | 4 (20%) | 13 (65%) | 3.9 (2.29) | 3.5 (2-6) | +169 |
| ILoveAnt (after) | 35 | 4 (11.43%) | 21 (60%) | 4.31 (2.98) | 4 (3-6.5) | +91 |

_ILoveAnt_ passed 300LP on the 15th of December. This means that the games played under 300LP were approximately in the first week and a half, while the latter being in the period of 2.5 weeks. Interestingly, there is a good difference between LP change before and after the 300 LP mark, which may have contributed to the net LP change over those periods. The same number of wins were identical in these two periods, with the former having a slightly greater Top 4 rate (65% vs 60%). I believe the difference in these results can be contributed to the greater difficulty of the games, since I would be likely placed in more difficult lobbies when playing at a higher LP. 

To compare _ILoveAnt_ after hitting 300LP and _phillipluong_ before 29th of December, it appears that my performance was much better on _ILoveAnt_ regardless. This may suggest that I had a perceived mental pressure from playing in an account with my name attached to it, rather than their higher ELO. I may have wanted my name to be perceived well and had my mentality focused on getting a higher LP. I had this realisation when watching a streamer in December give myself a better idea of how to enjoy playing 'Ranked' games. This was the idea of _playing to have more opportunities to play against better opponents, and learn from those games, rather than gaining LP'_. I believe this is still helping me climb today. 

### Analysis based on Account, by week
__Table 7: Performance of _ILoveAnt_ per week__

| Week No. | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| Week 1 | 21 | 5 (23.81%) | 14 (66.67%) | 3.76 (2.32) | 3 (2-6) | +221 |
| Week 2 | 15 | 1 (6.67%) | 10 (66.67%) | 4.33 (2.41) | 3 (3-6) | +40 |
| Week 3 | 15 | 2 (13.33%) | 9 (60%) | 4.06 (2.15) | 4 (2.5-6) | +87 |
| Week 4 | 4 | 1 (25%) | 1 (25%) | 6.00 (1.82) | 6 (4.75 - 7.25) | -88 |

__Table 8: Performance of _phillipluong_ per week__

| Week No. | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| Week 1 | 22 | 1 (4.54%) | 11 (50%) | 4.55 (1.89) | 4.5 (3-6) | -19 |
| Week 2 | 8 | 0 (0%) | 2 (25%) | 5.25 (1.28) | 5.5 (4.75-6) | -80 |
| Week 3 | 25 | 2 (8%) | 14 (56%) | 4.08 (2.10) | 4 (2-6) | +152 |
| Week 4 | 24 | 1 (4.17%) | 8 (33.33%) | 5.20 (2.25) | 5.5 (3.75 - 7) | -224 |


I was also curious on my performance of each account, per week. I wouldn't say that there were any drastic changes per account, per week. From what it looks like, the final week was probably that only 'drastic' difference. The account, 'ILoveAnt' had some steady progression throughout each week, besides week 4. Conversely, philipluong only really made a lot of success in Week 3 and lost LP every other week. 


### Analysis based on starting item
- There is basis that the starting item normally dictates the flow of the game, and hence, may be a good determinant of the overall placement. I would tend to agree with this idea, especially after looking at my own data. 

Traditionally, the more 'popular' items to collect in this patch appeared to be: Tears and Swords, tben Rods, Gloves, Bows and finally Cloaks, Vests and Belts. These patterns are often associated with the strongest kinds of compositions often being played at the time. In this patch, the data was leaning towards compotiions that played around Jhin, Ashe, Veigar, Riven, and sometimes, Zed. Many of these units would prefer Sword-based items (Jhin, Ashe), whilst some users prefered magic damage items (like Riven and Veigar). Compositions based around Zed were reliant on a lot of bows. 

<img src="images/freq_ave_placement_items.png"
     alt="Frequency and Average placement based on starting item"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 7: Frequency and Average placement of opening items__

By far, the most selected beginning item was the tear. The tear was perceived to be the greatest item for the patch, due to certain units using items that required tear components well (namely Veigar, and Riven), but can also be used to flexibly create items that fit (Hand of Justice) for the main carries. The other frequently used items were Rods Swords, Cloaks, Bows and Vests (in that order). 


<img src="images/top4_win_rate_items.png"
     alt="Top 4 and win rate based on starting item"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 8: Top 4 and Win Rate of opening items__

__Table 9: Performance based on starting items__

| Starting Item | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| Tear | 34 | 4 (11.76%) | 18 (52.94%) | 4.29 (2.21) | 4 (3-6) | +75 |
| Rod | 22 | 0 (0%) | 8 (36.36%) | 5.23 (2.07) | 5.5 (4-7) | -205 |
| Cloak | 18 | 2 (11.11%) | 9 (50%) | 4.27 (2.22) | 4.5 (2.25-6) | +51 |
| Sword | 18 | 1 (5.56%) | 10 (55.56%) | 4.44 (2.25) | 4 (2.25-6) | +18 |
| Bow | 16 | 2 (12.5%) | 9 (56.25%) | 4.19 (2.13) | 4 (2.75-5.25) | +69 |
| Vest | 14 | 1 (7.14%) | 8 (57.14%) | 4.5 (2.14) | 4 (3.25-6) | +26 |
| Belt | 6 | 2 (33.33%) | 4 (66.67%) | 3.33 (2.06) | 3.5 (1.5-4.75) | +96 |
| Glove | 3 | 0 (0%) | 1 (33.33%) | 6 (2.65) | 7 (5-7.5) | -62 |
| FON | 2 | 0 (0%) | 2 (100%) | 3.5 (0.71) | 3.5 (3.25-3.75) | +31 |
| Spatula | 1 | 0 (0%) | 0 (0%) | 5 (n/a) | 5 | -10 |

Out of all the items, I think the performance based on starting with a Rod and a Belt has been most interesting.

Interestingly, despite how frequently I had selected the Rod (spell power) as the starting item, I was severely underperforming in those games. Rod start netted 0 wins, and a top 4 rate far lower than than other items. Also, the Rod has been my worst LP change out of all items (-205 LP)

On the contrary, even though Belts were a less common first item starter, I performed surprisingly well when playing those items, with the highest win rate and top 4 rate out of all the items (with greater than 5 games). In addition, the belt has netted me the the best LP change (+96 LP). 

The two rarer items, the _Force of Nature (FON)_ and Spatula appeared in 3 out of the 134 games. In these instances, the starting carousel would give everyone these items, which really changes the flow of the game, due to how impactful spatula items (combined spatula items give units a particular new trait) and the FON (allows you to play an extra unit). From these fringe game, I did not win the lone spatula game, but managed to top 4 the FON games. What I found more interesting are the odds of getting 2 or more FON games in this sample is about 14.5%. Given how well I do in these games, I am not complaining. 

## Analysis based on the _Chosen_ mechanic

### Analysis based on the _Chosen_ trait

<img src="images/freq_chosen_traits.png"
     alt="Frequency of Chosen Trait"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 9: Frequency of Chosen Traits selected in game__

Not surprisingly, the most frequently selected units revolve around the compositions I enjoy playing (such as Hunter Adept, Elderwood Mages, Dusk). There are also traits that were often chosen due to their ability to win (Divine, Shade, Moonlight). In 8 of the games, I did not end the game with a chosen unit.

It would be very interesting to see the correlation plots between certain chosen traits and the starting item, because I expect to see some high correlation between, say, tear and Elderwoods or mages, or bow and Shade. 

<img src="images/chosen_trait_analysis.png"
     alt="Detailed Chosen Trait Analysis"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 10: Chosen Traits selected in game details__

The figure above gives a clear description of my performance. When observing the average placements of the chosen trait, the traditional traits that fit my favoured compositions do well (besides Divine and Mage). Beyond the sharpshooter trait, the traits would generally also underperform. Surprisingly, the traits that I moderately choose (have chosen \~ 6 times) result in the lowest average placement, and the greatest LP gain. These traits are: Adept, Brawler, Keeper, Shade, Duelist, and Sharpshooter. This category also nets the greatest win rates as well. I decided to include the table of this analysis below:

__Table 10: Performance based on Chosen Unit Trait__

| Chosen Trait | Games Played | Wins (%) | Top rate (%) | mean placements (SD) | median placements (IQR) | LP Diff |
|-|-|-|-|-|-|-|
| Elderwood | 19 | 1 (5.26%) | 11 (57.89%) | 4.10 (2.00) | 3 (3-5.5) | +113 |
| Hunter | 13 | 2 (15.38%) | 6 (46.15%) | 4.54 (2.26) | 5 (3-7) | +16 |
| Dusk | 10 | 0 (0%) | 5 (50%) | 4.5 (2.22) | 4.5 (2.25-6) | -8 |
| Divine | 9 | 0 (0%) | 3 (33.33%) | 5.44 (1.94) | 5 (4-7) | -128 |
| Moonlight | 9 | 0 (0%) | 5 (55.56%) | 4.44 (1.59) | 4 (3-5) | -5 |
| Mage | 7 | 0 (0%) | 3 (42.86%) | 4.71 (2.05) | 6 (3-6) | -29 |
| Duelist | 6 | 1 (16.67%) | 4 (66.67%) | 3.33 (1.86) | 3 (2.25-4.5) | +82 |
| Adept | 6 | 1 (16.67%) | 6 (100%) | 3.17 (1.33) | 4 (2.5-4) | +126 |
| Shade | 6 | 1 (16.67%) | 4 (66.67%) | 3.83 (2.64) | 3 (2-6.25) | +45 |
| Keeper | 6 | 2 (33.33%) | 3 (50%) | 4 (2.68) | 4.5 (1.75-5) | +27 |
| Sharpshooter | 6 | 3 (50%) | 5 (83.33%) | 2.5 (2.35) | 1.5 (1-2.75) | +162 |
| Brawler | 6 | 0 (0%) | 5 (83.33%) | 3.33 (1.21) | 3.5 (2.25-4) | +102 |
| Warlord | 4 | 1 (25%) | 2 (50%) | 4.5 (2.89) | 4.5 (3.25-5.75) | +1 |
| Vanguard | 4 | 0 (0%) | 1 (25%) | 5.5 (2.38) | 6.5 (5-5.75) | -44 |
| Assassin | 3 | 0 (0%) | 2 (66.66%) | 5 (2.65) | 4 (3.5-6) | -10 |
| Mystic | 3 | 0 (0%) | 1 (33.33%) | 5 (2.65) | 6 (4-6.5) | -9 |
| Fortune | 2 | 0 (0%) | 1 (50%) | 4 (2.83) | 4 (3-5) | +12 |
| Cultist | 2 | 0 (0%) | 1 (50%) | 4.5 (2.12) | 4.5 (3.75-5.25) | +1 |
| Spirit | 2 | 0 (0%) | 0 (0%) | 5.5 (0.71) | 5.5 (5.25-5.75) | -36 |
| Enlightened | 2 | 0 (0%) | 1 (50%) | 5.5 (2.12) | 5.5 (4.75-6.25) | -20 |
| Dazzler | 2 | 0 (0%) | 0 (0%) | 7 (1.41) | 7 (6.5-7.5) | -65 |
| none | 7 | 0 (0%) | 0 (0%) | 7.14 (0.90) | 7 (6.5-8) | -244 |

One chosen trait I find interesting is the _Fortune_ trait, which I perceive as quite bad, but within the two games I have played, I have had a net LP gain and an average placement below 4.5. 

Notably, when I don't end with a chosen unit, I have a 0% top 4 rate, a very high average placement, and the greatest LP loss, showing the importance of selecting a chosen in my gameplay.

### Analysis based on key _Chosen_ units

<img src="images/frequent_top4.png"
     alt="Word Cloud of Frequency of Top 4 Compositions"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 11: Word Cloud of Chosen Units based on Top 4 Frequency__

Winning compositions (played by me):

<img src="images/wordcloud_wins.png"
     alt="Word Cloud of Frequency of Winning Compositions"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 12: Word Cloud of Chosen Units based on Win Frequency__

__Table 11: Performance based on Chosen Unit__

<img src="images/individual_units_win_rate.png"
     alt="Table of Individual Unit Chosen Stats"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

I created this table outside of the markdown format to allow a better visualisation of the unit costs (Black names are 1-cost, green names are 2-cost, blue 3, purple 4, and yellow 5). As you can see, my most commonly selected chosen units were Ashe, Warwick, and Riven. Funnily enough, selecting chosen Ashe resulted in only a net gain of 1 LP throughout the four weeks. On the other hand, chosen Riven would actually result in a net loss of 56 LP. Taking a specific look at these games, I believe one big contribution to why chosen Ashe and Riven did not give me too much success was because of my inclinations towards the Dusk and Hunter compositions, regardless of whether I was winning or losing. Looking at the net changes in LP, this might have been the incorrect decision at times anyway. Warwick was also a very commonly selected unit, due to his versatility as a supporting unit in the _Hunters_ composition, as well as his ability ot be the main damage dealer in other compositions. Although I netted no wins with chosen Warwick over the period, there was an increase of 12 LP. 

The other 4-cost chosens that I normally go for are Jhin and Ahri (to a much lesser extent). Chosen Jhin would normally net me a top 4 or a win. On the flip side, I wouldn't be as successful with Ahri, knowing that compositions around Ahri realistically couldn't win games in this patch. However, this mindset may have hindered my performance when playing chosen Ahri during those games.

Looking at the reroll chosen units (Yasuo, Vayne and Zed, Aphelios, Diana and Lissandra), it appears that I played quite well when playing with a chosen unit selected early in the game. Zed was my most common selected unit in this group, where I performed quite well while playing him (+45 LP, 66% top 4 rate, 16% win rate). The most notable reroll chosen was Yasuo, which I played 5 times, top 4'ed 4 of them and won one of them, giving me a mean placement of 2.8 and a +102 LP gain, the highest of all chosen units. 

Three cost chosen units overall were an underperforming group (net -91 LP). I often only ended with a three cost chosen when I don't have an option to continue rolling for another chosen. 

The last 3 chosen units I wanted to look at were Adept units: Irelia, Shen, and Yone. On the previous section, you may notice that I had a 100% Top 4 rate when selecting a chosen Adept unit, and I wanted to observe which compositions worked best with these units. Most of the time, the best performing compositions would revolve around Hunter Adept, or Legendaries, with a couple of games where I added in Adept just for the strong unit. Irelia did not perform as well as the other two units, which was only played in Enlightened and Warwick compositions. 

### Analysis of winning and top 4 comps

Winning compositions (that I saw win):

<img src="images/winning_comps.png"
     alt="Word Cloud of winning comps"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 13: World cloud of descriptions of winning compositions (that I saw)__

Not too much to say about the winning and top compositions other than the general theme of top units I normally use (Hunter Adept, Elderwood, Dusk etc.). 

__Table 12: Performance with Legendary Chosens__

<img src="images/legendaries_win_rate.png"
     alt="Table of Legendaries Chosen Stats"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

I think one that stands out the most are the the 'Legendaries' composition, which comprise of a team of mostly (if not all) of the 5 cost units. This only happens when I happen to be playing really well with luck on my side. This allows me to comfortably secure myself a top 4, if not a first place.

## Future Directions

There are a handful of things that can be done to progress this EDA in the future, namely relating to the data categorisation and data collection aspect.

On the analysis side, I would love to explore other ways of representing the data. There are specific graphs that I would have represented differently as they probably give a better visualisation of my performance in the 4 week period. For example, representing net wins ([Figure xxx]) as a singular value rather than a percentage may be better since the percentage is skewed in favour of the 2 wins I had with a belt start. In addition, I would love to explore other ways to represent the compositions I used rather than the word clouds. 

When it comes to data collection, there could be some way to use the Riot Games API to collect a list of all the teams I have used (and maybe the teams my opponents used) in each game. That way, I can then determine which units I perform well with and against (and vice versa). A couple of analytic tools already accomplish such a feat already, such as tactics.tools, which allow me to analyse my performance on the last 20, 50, and 100 games. 

In addition, I wish to potentially replicate this EDA using SQL in order to develop my SQL toolbox. Hopefully, by learning SQL, I will also figure out new findings I can get from the same dataset.

Game-wise, I have very much been enjoying the changes in the 'meta' of the game, and hope to continue climbing the ladder. Recently, I have managed to finally reach one of my bigger goals for playing the game, which was to hit the 'Grandmaster' title (meaning that I am in the top 150 players in the Oceania server). 

<img src="images/gm_210116.png"
     alt="Finally Hit Grandmaster!"
     style="float: left; margin-right: 5px;" 
     width="200px;" />

__Figure 14: I hit Grandmaster!!!__

Very soon, there will be a huge balance patch, which changes out 20 characters for new ones, completely changing the flow of the game. Along with these changes, my short-term goal is to hit the top 100 in the Oceania Server, then maybe hit top 50 (giving me the Challenger title).  

## Other Resources

A huge thanks to a bunch of external tools that I regularly use to help my climb and feed my craving for data in TFT. These tools have incredible information taken from the Riot Games API and have a great User Interface. These include:

- lolchess.gg
- tactics.tools
- metatft.com
- tftactics.gg
- the competitive tft reddit site

Many of these tools have include a lot of analyses that I wish to incorporate myself, including analysing which units to use, combinations of units statistically work well together and which items that work better with units. I have a bunch of snapshots below from some of these websites that include information that I find extremely helpful and useful. 

<img src="images/lolchess_item_trends.png"
     alt="lolchess item trends"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 15: lolchess.gg item trends__

<img src="images/lolchess_match_history.png"
     alt="lolchess match history"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 16: lolchess.gg match history__

<img src="images/unit_selection_lolchess.png"
     alt="lolchess match history"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 17: lolchess.gg frequency of unit selection__

[lolchess.gg](lolchess.gg) is probably the most popular resource for regular players in the game, as you are able to get all the information that you need for the game. They also have lists of recommended compositions to play and for you to build your own teams in theory. In addition, lolchess also collects game information to allow you to look at players' match histories (including your own). I would love to try to use the information of my own match history to analyse unit and composition performance.

<img src="images/tactics_tools_iloveant_profile.png"
     alt="tacticstools profile"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 18: tactics.tools general profile__

<img src="images/tactics_tools_progression_100.png"
     alt="tactics tools progression"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 19: tactics.tools LP progression + GM/Challenger cutoff__

Another website, [tactic.tools](tactics.tools), provides addional information about match history, as well as an artificial 'stats bar', which comes from an inbuilt formula to calculate your performance on economy, compositions, execution, and flexibility.  

The website also has ways to analyse how well you play depending on the units you use, so you can get a good understanding of how well you perform with certain units. I would love to have these formulations in my on analyses, and have these visualisations in my analysis in the future.

<img src="images/metatft_bestcomps.png"
     alt="lolchess match history"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 20: metatft.com list of best compositions__

<img src="images/metatft_comp_details.png"
     alt="lolchess match history"
     style="float: left; margin-right: 5px;" 
     width="500px;" />

__Figure 21: metatft.com details of the Hunter Adept Composition__

My favourite analytics website, [metatft.com](metatft.com), gives you information about the current metagame trends by performing a clustering algorithm on over one million games. This includes all the units in the compositions, ideal chosen traits to have in these compositions, and the best items to equip onto these units. You can view item trends (best items for units, and vice versa), composition pick and win rates, and average placements.

Also, there are ways to analyse individual players to see how they pilot certain compositions, which you can use to improve your own gameplay. To me, this is the benchmark analytics resource for TFT, and probably my most frequented website at the moment. 
