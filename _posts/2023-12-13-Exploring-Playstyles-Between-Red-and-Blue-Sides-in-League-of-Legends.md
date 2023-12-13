---
layout: post
title:  "Exploring Playstyles Between Red and Blue-Sides in League of Legends"
author: Paul Crowley
description: "Scraping and cleaning publicly available data for comparisons in playstyle across both sides."
image: /assets/images/red_blue.jpg
---

### A quick look at the data
In [my last post](https://crowleyp5.github.io/crowleyp5blog/2023/11/17/Collecting-Data-To-Analyze-Red-Side-vs.-Blue-Side-in-Professional-League-of-Legends.html), I talked about the process I went through to scrape a data set with information from professional league of legends games. Before we begin exploring the data, I want to show what it looks like in tabular format. After taking a look at that, we will begin posing some questions and answering them with the data.
|index|Tournament|Date|Game Time|Blue Team|Red Team|Blue Kills|Blue Turrets|Blue Dragons|Blue Barons|Red Kills|Red Turrets|Red Dragons|Red Barons|Blue Wards Placed|Blue Wards Destroyed|Red Wards Placed|Red Wards Destroyed|First Dragon Team|First Dragon Time|First Rift Herald Team|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|Worlds Main Event 2023|11/12/2023|24\.85|T1|JD Gaming|23|7|2|0|8|0|1|0|71|31|98|34|Red|6\.133333333333334|Red|
|1|Worlds Main Event 2023|11/12/2023|37\.98333333333333|JD Gaming|T1|20|11|3|2|7|3|2|0|152|88|167|97|Red|9\.65|Blue|
|2|Worlds Main Event 2023|11/12/2023|30\.716666666666665|T1|JD Gaming|18|6|4|1|10|4|1|1|138|51|99|62|Blue|6\.416666666666667|Blue|
|3|Worlds Main Event 2023|11/12/2023|31\.416666666666668|JD Gaming|T1|6|3|0|0|16|11|4|2|134|41|104|59|Red|10\.933333333333334|Blue|
|4|Worlds Main Event 2023|11/11/2023|29\.366666666666667|Weibo Gaming|Bilibili Gaming|18|10|3|1|3|2|1|0|99|30|92|41|Red|8\.866666666666667|Blue|

### Which side generates more gold from CS and Kills?
In League of Legends, gold makes your character stronger. Accumulating gold efficiently it key to establishing an early lead and pushing your advantage to victory. Creep score (CS) and kills measure gold income, but income can also be earned from objectives. While this is an important aspect of the game, to in some ways represents a playstyle or win condition rather than a metric of winning or losing.
