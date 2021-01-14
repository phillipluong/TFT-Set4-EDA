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



## EDA
In the whole dataset collected, there are a total of 555 different games of TFT played over the course of about four months (from mid September to present). TFT is a game which regularly has balance patches to ensure that the 'best units', 'best compositions', and 'best items' don't stay constant, and will keep the compeitive side of the game more interesting. As a result, I have decided to limit my analysis to a single patch - 10.25 (spanning essentially the whole of December until January 5 2021). This patch was chosen because it was the longest span of time without balance patches (the balance team was on holidays). This also meant that I personally played a lot of games, making the findings more interesting. In addition, since the most recent balance patch (as of writing this blogpost) has not changed the meta too drastically, it may also help me with my climb to Grandmaster. 


### Primary Statistics



### Analysis based on week



### Analysis based on Account



### Analysis based on starting item



### Analysis based on final chosen unit/trait



## Future Directions

There are a handful of things that can be done to progress this EDA in the future, namely relating to the data categorisation and data collection aspect.

When it comes to data collection, there could be some way to use the Riot Games API to collect a list of all the teams I have used (and maybe the teams my opponents used) in each game. That way, I can then determine which units I perform well with and against (and vice versa). A couple of analytic tools already accomplish such a feat already, such as tactics.tools, which allow me to analyse my performance on the last 20, 50, and 100 games. 

In addition, I wish to potentially replicate this EDA using SQL in order to develop my SQL toolbox. Hopefully, by learning SQL, I will also figure out new findings I can get from the same dataset.

## Other Resources

A huge thanks to a bunch of external tools that I regularly use to help my climb and feed my craving for data in TFT. These tools have incredible information taken from the Riot Games API and have a great User Interface. These include:

- lolchess.gg
- tactics.tools
- metatft.com
- tftactics.gg
- the competitive tft reddit site

Many of these tools have include a lot of analyses that I wish to incorporate myself, including analysing which units to use, combinations of units statistically work well together and which items that work better with units. I have a bunch of snapshots below from some of these websites that include information that I find extremely helpful and useful. 
