# Final-Project
Predicting March Madness games with machine learning. This is inspired by the [Kaggle March Mania](https://www.kaggle.com/c/mens-march-mania-2022) competition. Our data is sourced from this competition.


## Proposal
We are going to use a group of college basketball datasets to predict which team is most likely to win in a head to head match in the March Madness competition.  We'll compare features such as historic rankings and average points, rebounds, and turnovers per game to predict this probability.

## Communication 
We will use Slack for team communications. 
Google Drive will house our data files, due to GitHub file size constraints. 

## Segment 1 Deliverables
Our project roadmap can be found in these [Google Slides](https://docs.google.com/presentation/d/1cj5roKmtqg1G50iBWTQ_k9QtFI_a5Rb9JQhdKWZx1qg/edit#slide=id.g127d0f87571_0_5)

### Database
Our database will consist of the following tables: Teams, Team_Rankings, Compact Results (both Regular season and tourney versions) and Detailed Regular Season Results (both regular season and tourney versions). The database will be hosted through AWS's RDS. A non-exhaustive, provisional ERD is shown below.

<img width="549" alt="image" src="https://user-images.githubusercontent.com/93338132/167052157-aa6ddba3-f874-4035-a90e-0777cdb01a8b.png">


### Model
Our model will be a logistic regression algorithm that produces the probability that Team A will win against Team B for all possible 2,278 March Madness games. 

Our features will be in-game basketball statistics (shooting percentage, rebounds, turnovers, etc.) that pertain to both the Winner and Loser of a game. We plan to use detailed box score results from historic games during the 2003 season onward to train and test the model.  The model will determine feature importance, and based on logistic regression, output probability that a given team (Team A) will beat another given team (Team B).

The raw output will be formatted as below.

<img width="730" alt="image" src="https://user-images.githubusercontent.com/93338132/167050740-f49f2dfd-620a-429d-b491-a1b846b53ce0.png">


### Visualizations
We will use a variety of tools, including Tableau, Plotly, and Matplotlib to make an interactive head to head matchup predictor for users. We will also show a variety of Exploratory Data Analysis (EDA) visuals to tell the story of the nation's greatest tournament!

![Cities](https://user-images.githubusercontent.com/95720986/167307458-9574b2dc-1ba4-4eed-a8d5-7360c93dbaf3.png)

### Tableau Story
https://public.tableau.com/app/profile/angie.greene/viz/FinalProject_16518756794360/WhosGoingtoWin?publish=yes
