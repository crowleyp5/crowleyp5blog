---
layout: post
title:  "Exploring Playstyles Between Red and Blue Sides in League of Legends"
author: Paul Crowley
description: "Exploratory data analysis of playstyles on both sides."
image: /assets/images/red_blue2.jpg
---

<style>
    .margin-image img {
        position: absolute;
        right: -100px;
        top: 0;
        width: 460px;
        height: auto;
    }
</style>

### Preface
In [my last post](https://crowleyp5.github.io/crowleyp5blog/2023/11/17/Collecting-Data-To-Analyze-Red-Side-vs.-Blue-Side-in-Professional-League-of-Legends.html), I talked about the process I went through to scrape a data set with information from professional league of legends games. Before we begin exploring the data, You may want to explore what the data looks like. The repository with the data and code for scraping and data analysis is [here](https://github.com/crowleyp5/red-blue-lol-analysis/tree/main).

<div class="margin-image">
    <img src="/crowleyp5blog/assets/images/map.png" alt="Map" style="position: absolute; right: -100px; top: 500px; height: auto;">
</div>

### Which characters are played more on both sides?
Since characters often differ in playstyles, analyzing the most played characters on each side could reveal some insights about team playstyles. For example, some team compositions rely on long ranged abilities, while others rely on strong 5 on 5 team fighting potential. These are the 5 most played characters at each role for both sides:
![Picks](/crowleyp5blog/assets/images/top_5_picks.png)
From this table, we can see that there are hardly any differences across both sides. This would indicate that both sides opt for a healthy balance of team compositions, choosing to mix up their approaches to each game. Although there appear to be some differences in the most played support characters, they generally serve the same purpose as a low-damage and hard-to-kill form of crowd control, meaning that they create offensive or defensive imbalances for the team rather than being a threat on their own. Given their similarity in playstles, I would say that the compositions across both sides tends to be the same.

### Which side generates more gold from CS and Kills?
In League of Legends, gold makes your character stronger. Accumulating gold efficiently is key to establishing an early lead and pushing your advantage to victory. Creep score (CS) and kills measure gold income, but income can also be earned from objectives. While this is an important aspect of the game, it in some ways represents a playstyle or win condition rather than a metric of winning or losing. Let's take a look at the numbers.

![CS](/crowleyp5blog/assets/images/CS_Diff_Roles.png)

![Kills](/crowleyp5blog/assets/images/Kill_Diff_Roles.png)

From these graphs, we can see that players in the top role have a wide range but fairly symmetric distribution of CS differential. The mid role for the blue side tends to have a slight edge in this category, and the bot role for the red side tends to have a slight edge. In terms of kills, it appears that the blue side has slight edge. This likely means that the blue team likely tends to have better 5 on 5 team fight potential, but as we learned from the previous table, this is likely not caused by the team composition. Overall, it appears that the blue side generates more gold from CS and kills.

### Which objectives are taken more on both sides?
<div class="margin-image">
    <img src="/crowleyp5blog/assets/images/turret.png" alt="Turret" style="position: absolute; right: -100px; top: 3500px; height: auto;">
</div>
The other main source of income comes from objectives, which include turrets, dragons, rift heralds, and barons. Rift heralds are only available from minute 8 until minute 20 of the game, and the baron is available after minute 20. Pursuing an objective, especially during the early stages of the game, generally but not always results in a traded objective on the other side of the map. Simply put, a team that puts pressure on the top side tower or baron may not have the resources to prevent pressure on the bottom side tower or dragon, so the other team will counterattack. We can use the data to see of teams tend to prefer a certain side of the baron and dragon trade, and to see if both teams are able to take the same number of turrets.
<div class="margin-image">
    <img src="/crowleyp5blog/assets/images/rift.png" alt="Rift Herald" style="position: absolute; right: -100px; top: 2400px; height: auto;">
</div>

![Objectives](/crowleyp5blog/assets/images/Obj_Diff_Teams.png)

We can see that the red side and blue side are able to secure similar numbers of barons and dragons, but the blue side is getting about a full turret more per game on average. One theory could be that the CS advantage for the blue team in the mid role gives their mid priority. If the mid role has priority, they can rotate to the dragon or baron before their red side counterpart. It can be hard to take down the mid turret due to its proximity to the other objectives, so blue may not necessarily have to trade the turret for the objective because of its mid priority, whereas red may have to make the trade if they struggle to get mid priority. If this is the case, this would stem from more pressure being exerted on mid by the blue side.
<div class="margin-image">
    <img src="/crowleyp5blog/assets/images/dragon.jpg" alt="Dragon" style="position: absolute; right: -100px; top: 4400px; height: auto;">
</div>

![Dragons](/crowleyp5blog/assets/images/DragonsVsTurrets.png)
![DragonsRed](/crowleyp5blog/assets/images/red.png)

The hexbin plot reaffirms what the previous graph showed in regards to the blue side getting more turrets. However, it suggests that objective trades are not often being done with dragons and turrets. In most matches, the winning team tends to get more of both over the course of the game.

### How quickly are the first objectives taken on both sides?
We can also take a look at when dragons and rift heralds are being taken. Securing each dragon provides bonuses to the team, and the fourth dragon provides a significant bonus that is incredibly difficult for the opponent to overcome. This is a late game strategy where you may be struggling during the early phases, but you plan to scale better into the later phases. Since dragons spawn only periodically, it is important to secure them quickly so as no to delay the win condition. On the other hand, the rift herald provides early game gold advantages and provides a bonus that makes it easier to secure turrets, but this strategy typically loses in the late game to a team with 4 dragons. We can better understand the gameplan and execution for each team if we check how early these teams are able to secure their first objectives of choice.

![Combinations](/crowleyp5blog/assets/images/comb_prop.png)

![Times](/crowleyp5blog/assets/images/Obj_Times_Teams.png)

First, we can see that the most common outcome is a trade where the red team gets the dragon and the blue team gets the rift herald, indicating that the blue team tends to play for the early win condition and the red team for the late win condition. However, the time taken for both teams to secure their first chosen objective is very similar. Thus, the execution for effectively securing objectives appears to be the same, but what differs is the choice of which objective to pursue. Based on the path the jungle role takes, it may be more convenient for the red jungle to end up on the bottom side with the dragon and the blue jungle on the top side with the rift herald. It could also be that the blue mid is establishing priority, and the rift herald is seen as the better objective. It could also be that the red bot and support are estblishing priority on the bot side, which allows them to secure the dragon more easily than the blue team. Ultimately, is could be a combination of these factors that influences game strategy.

### Which side has an easier time establishing vision control?
Wards are essential to game strategy because they provide vision on parts of the map players normally cannot see. Finding and destroying these wards is essential because they keep your opponent guessing as to the next moves. Therefore, the ability do sominate vision control can influence how a team plays. 

<div class="margin-image">
    <img src="/crowleyp5blog/assets/images/ward.png" alt="Ward" style="position: absolute; right: -100px; top: 6700px; height: auto;">
</div>

Teams with good vision control could be more inclined to fight 5 on 5 or pursue objectives based on information wards provide. It allows a team to know or anticipate opponents' moves and react accordingly. Poor vision control results in failed trades and team fights. Let's compare the number of wards the opponent places with the number of wards the team destroys as a metric for quality vision control.

![Wards](/crowleyp5blog/assets/images/Wards_Teams.png)

These graphs are nearly identical, meaning that both teams are able to remove about the same proportion of wards their opponents place. This means that any disparity in kills or objectives is likely not the result of a lack of information.

### Conclusion
Based on this analysis, we have learned that the blue side tends to have better team fight potential and is likely better able to exert pressure on the middle of the map and the red side is better able to exert pressure on the bottom of the map. This results in CS differentials in favor of the blue mid and the red bot. The blue team overall gets more kills and turrets. The priority established by the blue mid and the red bot usually prompt the blue team to take the rift herald on the top side and the red team to take the dragon on the bottom side. The priority established by the mid lane also makes easier for the blue team to pursue objectives on the top or bottom side without having to sacrifice their middle turret.
