Problem definition:
The basic aim of the project is to predict the probability of the result of a soccer match given the current state of the match at a particular minute. However, the problem is, there is no data available that gives us the probability/odds of a particular team winning at a particular minute. So we transform our current probability prediction problem into a classification problem with three classes “Home win”, “Away win” and “Draw”. Given a data point (state of the match), we predict the probability with which it belongs to all of those classes, and that probability is our actual desired output.

Dataset
We obtain data from two primary sources, details of which are as follows:
European Soccer Database (featured on Kaggle)
Betting data: This dataset provides us before match odds as published on the website Bet365.com. Bet365 is an online betting service which predicts odds for the results of a particular match. This betting data is crucial in predicting the in-game probability of results, once we account for the other events that have occurred since the match started. These odds are provided as input to our model to help it better predict the probability of results. The betting data from Bet365 is used as the starting point for our probability predictor.
Player Attributes: FIFA releases a soccer game every year which can be played on a PC and different consoles. In this game, all players are given specific ratings based on their performance in the previous year. The match data we have also contains a list of all players that are playing in each team. We use this data to get the ratings for each player in the teams and we calculate the average player rating for both, home and away teams. This attribute gives us a better idea of how good both the teams are. The better a particular team, the more are its chances of winning compared to that of a lower quality team.

Key event data
In a soccer match, there are specific events that occur which affect the end result directly       or indirectly. Example of such events are goals scored and cards issued to players for fouls committed. In order to accurately predict the probability of a result of a match at a particular instant, it is imperative that we have data about the key events that have happened during the match. 
Goal Data:
There are three different types of goal events that we have recorded are:
Goal (Scoring team gets a point)
Penalty Goal (Scoring team gets a point)
Own Goal (The opposite team gets the point)


Foul Cards:
There are two types of Foul cards that can be issued to players, a Yellow Card and a Red Card. If a player gets a Red Card, that player is expelled from the field and the team has to play with less number of players. Two Yellow Cards are equivalent to a Red Card. We keep a running count of the number of cards that are issued to players of each team.


Data Spread: Currently we are only considering soccer matches from the English Premier League (EPL) from 2009-2014

This is the data spread out amongst the 3 possible classes, 
-1  : “Away Win”
 0  :  “Draw”
 1  : “Home Win”


Linear offset error (L)
The Linear offset error (L) is robust to the model predicting values in opposite directions of the ideal slope value
We calculate the RMSD between all predicted probability values and ideal values for a closed range of 0 to 1 and a step of 0.05.
This gives us a more accurate evaluation of the model.

Baseline Model
Our Baseline Model is Logistic Regression, which is based on a subset of the actual features we will be using for our advanced models. 
For the logistic regression, the features that have been used are home and away team goals, initial betting odds and time elapsed.

Advanced Models 
The following features have been used for the advanced models:
1. Away Yellow Cards
2. Bet365 Home Odds
3. Home Red Cards
4. Bet365 Draw Odds
5. Bet365 Away Odds
6. Home Yellow Cards
7. Away Players Avg Rating
8. Home Players Avg Rating
9. Away Players Avg Potential
10. Home Players Avg Potential
11. Minutes Elapsed
12. Away goals
13. Home goals
14. Goal Difference

K-Nearest Neighbors Classifier
Another way to look at our current problem is as a nearest neighbors problem. We tried to predict the outcome of a match state based on the outcome of similar match states in the past. We consider the values of 15 nearest neighbours to predict the value of a particular game state. The Linear offset error (L) for the model is 1.0874.

Random Forest Classifier
Ensemble methods like Random Forest are also known to incorporate different hidden features in the data that might be overlooked by single classifiers. Hence we will evaluate the performance of a Random Forest Classifier on our data, with and without team attributes provided. The Linear Offset Error (L) for this model is 1.0564.

MLP Classifier
We built a neural network that uses the Softmax activation function to predict the end result of a game. We extract the probability values from the penultimate layer of the network for our prediction. The Linear Offset Error (L) for this model is 0.2366.

Please Refer Final_model.ipynb for detailed analysis
