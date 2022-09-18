# NBA championship - can you tell which team will win it all before All-Star Game starts?
- resume points xxx


# Framing the business and analytical problem
- Business question
  - How confidently can we tell which team will win the championship 4 months in advance (around when All-Star Game is held)?
  - Timeline of an NBA season
    - <img src="../data/image/2022-09-11-14-37-33.png">

- Analytical problem
  - To predict the probability of a team winning the championship given its performance in the regular season before All-Star Game
  - This is a supervised classification problem which can be trained offline

# How will my solution be used
- It is a common debate among fans, critics and teams that whether a team can win this year
  - This debate is often the most heated around the All-Star Game in February
    - As a mid-season cutoff, teams have played against each other for a few months already so there is a large enough sample size to analyze
  - Fans argue that despite having a losing record by then, their favorite team just needs more time to make things work
  - Critics would argue that the teams which have been playing well so far don't necessarily play as well in the playoffs (often described as "a different paradigm" vs the regular season)
  - Team managers and coaches would like to know if they can improve the team by adjusting their lineup with some player trades before the trade deadline at around All-Star Game
- My solution as a propensity model with interpretable features will be able to offer insights into which areas a team can focus on / ignore when it comes to improving one's chance to win a championship

# Background
  
- 30 teams (15 in each conference) will compete against each other for 82 games within the regular season
- 16 teams (8 in each conference) will then enter the playoffs with 4 elimination rounds
  - The definition of "top 8" has become more complicated with the recently established play-in tournament ([more details](https://www.nba.com/news/nba-play-in-tournament))
- Final team to survive through all 4 elimination rounds will win the championship (Larry O'Brien Championship Trophy)
  - NBA 2022 champion: Golden State Warriors
  - <img src="../data/image/2022-09-11-14-19-57.png">



- limitation of existing solutions


- existing knowledge that I can reuse
- is human expertise available
- how would you solve the problem manually
- list assumptions I made so far
- verify assumptions

# How should performance be measured
- Model performance = ROC AUC score
- To align with business objective: 
  - Emphasis on precision instead of recall
  - As a team manager / fan, it would be more useful to err on the side of caution and be confident that my prediction is correct, rather than to capture all the winning teams
  - At least 80% precision should be achieved

# Source of data
- NBA team statistics in regular season and playoffs from [NBA.com/stats](https://www.nba.com/stats/teams/traditional/?sort=W_PCT&dir=-1&Season=2021-22&SeasonType=Regular%20Season&SeasonSegment=Pre%20All-Star) using [nba_api from github](https://github.com/swar/nba_api/blob/master/docs/nba_api/stats/endpoints/leaguedashteamstats.md)
- <img src="../data/image/2022-09-12-14-53-32.png">
- Type of statistics available: 
  - Base / Advanced / Misc / Four Factors / Scoring / Opponent / Usage / Defense
  - Each measures a different aspect of a team's or its opponent's performance in the regular season
- Assumption: setting the scope of data to pre All-Star Game is a good cutoff as mid-season performance
  - <img src="../data/image/2022-09-12-15-06-12.png">
  - Some seasons have abnormally high and low number of games played before All-Star Game, e.g. 1997-98 (82 games) and 1998-99 (4 games) due to NBA lockout
  - Removed those abnormal seasons such that all of them represent a good estimate of mid-season cutoff

# Findings

# Issues discovered with suggested improvements


# Future improvements
- ordinal regression using neural network with multilabel binary classifier output layer + rank conformity check in cost function

# References
- nba api
- towardsdatascience lift and gain chart

 with SGDClassifier(loss='modified_huber')
- ROC AUC of train set much lower than 10-fold CV AUC
- didn't happen when loss = 'log' for logistic regression or 'hinge' for linear SVM 
<img src="../master/data/image/2022-09-06-13-04-41.png">