# Final-Project
Predicting March Madness games with machine learning. This is inspired by the [Kaggle March Mania](https://www.kaggle.com/c/mens-march-mania-2022) competition. Our data is sourced from this competition.

Our Google Slides [presentation](https://docs.google.com/presentation/d/1HYjOiJzDm9tq-HdAaf0HMkdC65oxDQk9SOGrZIYbI_8/edit#slide=id.g12d996d0a47_1_195) will address relevant deliverables not accomplished in this ReadMe.

## Proposal
We are going to use a group of college basketball datasets to predict which team is most likely to win in a head to head match in the March Madness competition.  We'll compare features such as historic rankings and average points, rebounds, and turnovers per game to predict this probability.

## Communication 
We will use Slack for team communications. 
Google Drive will house our data files, due to GitHub file size constraints. 

Our [project roadmap](https://docs.google.com/presentation/d/1cj5roKmtqg1G50iBWTQ_k9QtFI_a5Rb9JQhdKWZx1qg/edit#slide=id.g127d0f87571_0_5) is maintained in Google Slides.

## Database
Our database will consist of the following tables: Teams, Team_Rankings, Compact Results (both Regular season and tourney versions) and Detailed Regular Season Results (both regular season and tourney versions). The database will be hosted through AWS's RDS. The current ERD is shown below.

![image](https://user-images.githubusercontent.com/93338132/169716800-1ebe99e9-3e16-4120-a878-b948a25e0095.png)

## Model
Our model is a random forest algorithm that produces the probability that Team A will win against Team B for all possible 2,278 March Madness games. 

Our features include in-game basketball statistics (shooting percentage, rebounds, turnovers, etc.) and poll rankings that pertain to both the Winner and Loser of a game. We use detailed box score results from historic games during the 2003 season onward to train and test the model.  The model will determine feature importance and produce probability that a given team (Team A) will beat another given team (Team B). 

The raw output will be formatted as below.

<img width="730" alt="image" src="https://user-images.githubusercontent.com/93338132/167050740-f49f2dfd-620a-429d-b491-a1b846b53ce0.png">

Features will be discussed in more detail in the next section but a random forest was chosen because we are ultimately trying to predict a binary, labeled outcome and have multiple features with an unkown (to us) importance. We want to avoid overfitting, understand our features' importances for communicability, and handle large datasets. While a random forest may not be the best model for accuracy in this situation, it is the best balance of executabiliy, accuracy, and understanding. 

![image](https://user-images.githubusercontent.com/93338132/169670770-676ff636-4619-4d26-885e-d7917a7e99b3.png)

### Model - Preprocessing & Feature Engineering
Fortunately, the Kaggle data comes precleaned. However, to ready our data for random forest classification a few preprocessing steps were taken. 

1. Dropped all results before 2003 season to enable us to pull in rankings for each game
2. Created columns for Season-Day-Team to enable use as a primary key in our database, if needed in the future.
3. Merging rankings into our box score dataframe, so the winner and loser each have their rank from that week of the season

Next, we engineered our features. Feature selection was influenced by the [Four Factors]([url](https://www.basketball-reference.com/about/factors.html)) popularized by Dean Oliver. The logic is that basketball is obviously a game of scoring more points than your opponent. To accomplish this obvious goal, teams want to score efficiently on their possessions, get more possessions than their opponent, and end possessions with scoring attempts vs. turnovers. In addition to in-game stats, we added Rankings as well, to synthetically and indirectly account for strength of schedule. 

One notable omission at this current stage is if the game was played as a Home, Away, or Neutral game for the winning team. This was done for simplicity of the model at this time.

Current features (formatted as the differential between winner and loser): Rankings, effective FG percentage (a measure of shot efficiency), FT percentage, Offensive and Defensive Rebounds, Assists, Turnovers, Steals, Blocks, and Personal Fouls.

Feature importance below:

![image](https://user-images.githubusercontent.com/93338132/169670590-a10d1543-0ae3-49d5-870b-01d046da1d53.png)

Our model was then trained and tested using scikit-learn's train_test_split method on regular season data. This was done because there is over 100,000 regular season games to work with, vs little over 2000 tournament games. We will use the regular season trained model to predict the tournament games.

The model features are formatted as differentials because we will use season averages for teams in the tournament, then take the stat differentials between a given pair of teams, and predict the outcome with our model.

## Visualizations
We will use a variety of tools, including Tableau, to make an interactive head to head matchup predictor for users. We will also show a variety of Exploratory Data Analysis (EDA) visuals to tell the story of the nation's greatest tournament!

This [Tableau Story](https://public.tableau.com/app/profile/angie.greene/viz/FinalProject_16518756794360/WhosGoingtoWin?publish=yes) houses our current visualizations. One example below is a map of all D1 Schools with Men's Basketball Programs.
![Cities](https://user-images.githubusercontent.com/95720986/167307458-9574b2dc-1ba4-4eed-a8d5-7360c93dbaf3.png)







