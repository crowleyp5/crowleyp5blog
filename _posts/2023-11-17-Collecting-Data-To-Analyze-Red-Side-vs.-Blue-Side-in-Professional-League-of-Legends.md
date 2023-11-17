---
layout: post
title:  "Collecting Data To Analyze Red Side vs. Blue Side in Professional League of Legends"
author: Paul Crowley
description: "Scraping and cleaning publicly available data for comparisons in playstyle across both sides."
image: /assets/images/red_blue.jpg
---
### For Those Unfamiliar with League of Legends
League of Legends is easily one of the most popular online games played on PC. It has a large casual following and a very large professional scene worldwide. It is a strategic, team-based game with 5 players on each team. The game is played on a symmetric map with three lanes and jungle inbetween them. Although the map is symmetric, the players are mirrored, so the two sides of the map (referred to as red side and blue side) are not equal. Due to the complexity of the game and time it would take to explain everything, I will not be giving much more details than this.

### Motivation, Purpose, and Research Question
Every year, there is a worldwide tournament where the best professional teams from across the world are invitied to compete to become the best team in the world. This tournament started again last month, and I have been following along. Although League of Legends players and analysts know that the blue side has a slightly higher win rate (55%) than the red side, not much analysis is done to explain why. I wanted to find data that would help examine differences in playstyles. How do playstyles differ from red side and blue side?

## Scraping the Data
Data was scraped from the Games of Legends site, which posts game statistics from leagues around the world. Scraping the data took a considerable amount of time due to how frequently it had to navigate to a new page, so I would not recommend scraping your own data set unless you have the passion and patience like I did. The format of this site is a table with 10 of the most recent professional sets of League of Legends. There is a back button to show the previous 10 sets that does not redirect to a new page. In the row corresponding to each set, there is a link that redirects us to a stats page where I scraped most of the info. Since this redirects to a new page with the game stats, it nagivates back to the home page, and it has to push the previous 10 button again to get back to the set being analyzed. Thus, it had to keep track of the back count. Each set has anywhere from 1 to 5 games. It is important to note that some games did not have the required stats, so the program throws errors. At first, I tried to filter the offending tournaments out, but this was not feasible because of how many there were. If the program throws errors, I simply adjusted the back button count and started the program again.

## Cleaning the Data
The data was fairly clean to begin with, but there were a few steps necessary to make the data usable. The program scraped duplicate games because of insufficient sleep times and inconsistent load times. It probably would have been more efficient to use expected condition statements instead of manually putting the program to sleep. After removing duplicate rows, there were 509 game observations in the data set. I converted the times that were formatted in minutes and seconds to just minutes with decimals, which simplified the units for numeric comparisons. I converted the date to datetime format. There were some extra commas in the KDA and CS column, which I removed. I then split the strings by commas in that column and in the picks and bans columns to create separate columns for eaach KDA, CS, pick, and ban. The KDA, CS, and picks were in order of roles of top, jungle, mid, bot, and support, so ther columns are labeled as such on each side. The bans are labeled from one to five on each side. The other columns were already formatted properly.

## Ethical Considerations
Games of Legends profits from subscriptions to analytical products and services that aid in making informed bets on games. I puposefully did not scrape a win/loss column for this reason. The scope of this data set and analysis is to examine playstyles between red and blue sides, not make predictions on outcomes, so I feel that the scraping is not unethical. Additionally, the robots.txt file does not disallow scraping from any of the pages visited.

## Conclusion
I intended to get more data than I scraped, but I realized that the time constraints were more than I anticipated given the number of page redirects, pushed buttons, and fetched javascript graphs. Aside from this, the data set is complete and ready for analysis. [Visit my GitHub repository](https://github.com/yourusername/yourrepository) for more details.
