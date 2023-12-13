---
layout: post
title:  "Exploring Playstyles Between Red and Blue-Sides in League of Legends"
author: Paul Crowley
description: "Scraping and cleaning publicly available data for comparisons in playstyle across both sides."
image: /assets/images/red_blue.jpg
---

### A quick look at the data
In [my last post](https://crowleyp5.github.io/crowleyp5blog/2023/11/17/Collecting-Data-To-Analyze-Red-Side-vs.-Blue-Side-in-Professional-League-of-Legends.html), I talked about the process I went through to scrape a data set with information from professional league of legends games. Before we begin exploring the data, I want to show what it looks like in tabular format. After taking a look at that, we will begin posing some questions and answering them with the data.
| index | Tournament            | Date       | Game Time | Blue Team     | Red Team      | Blue Kills | Blue Turrets | Blue Dragons | Blue Barons | Red Kills | Red Turrets | Red Dragons | Red Barons | Blue Wards Placed | Blue Wards Destroyed | Red Wards Placed | Red Wards Destroyed | First Dragon Team | First Dragon Time | First Rift Herald Team |
|-------|-----------------------|------------|-----------|---------------|---------------|------------|--------------|--------------|-------------|-----------|-------------|-------------|------------|-------------------|---------------------|------------------|--------------------|--------------------|-------------------|---------------------|
| 0     | Worlds Main Event 2023| 11/12/2023 | 24.85     | T1            | JD Gaming     | 23         | 7            | 2            | 0           | 8         | 0           | 1           | 0          | 71                 | 31                  | 98               | 34                 | Red                | 6.133              | Red                   |
...


### Which characters are played more or banned more on both sides?
image: /assets/images/.jpg

### Which side generates more gold from CS and Kills?
In League of Legends, gold makes your character stronger. Accumulating gold efficiently it key to establishing an early lead and pushing your advantage to victory. Creep score (CS) and kills measure gold income, but income can also be earned from objectives. While this is an important aspect of the game, to in some ways represents a playstyle or win condition rather than a metric of winning or losing.

![CS Difference by Role](/assets/images/CS_Diff_Roles.png)

![Kill Difference by Role](/assets/images/Kill_Diff_Roles.png)

### Which objectives are taken more on both sides?

![Objective Differences by Team](/assets/images/Obj_Diff_Teams.png)

### How quickly are the first objectives taken on both sides?

![First Objective Times by Team](/assets/images/Objective_Times_Teams.png)

### Which side has an easier time establishing vision control?

![Opponents Wards Placed and Team Wards Deestroyed](/assets/images/Wards_Teams.png)
