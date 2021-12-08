# Introduction

The reality TV show Survivor has been airing for over 20 years, mainly due to its great success and popularity in the United States. The general plot of the show is that 16-20 selected people are taken to an uninhabited location with little supplies. These people are expected to survive, participate in challenges, and vote one person off the game every 3 days, until there are only a few left. The winner is then chosen by the contestants who have already been voted off.  One aspect of the game that fascinates viewers is the fact that the winner is always seemingly impossible to predict among the players at first glance. Because the game not only includes fitness and intelligence, but also social factors, there is no specific "type" of person that consistently wins the game. Therefore, it is our intention in this analysis to see if a model can be created that accurately predicts whether a player will win the game, based solely on geographical factors. This will help in determining whether there are some types of people who have a higher tendency to win the game, regardless of how they played.

# Collecting and Cleaning Data

We begin our study by gathering several datasets from online that hold information about the Survivor show and its contestants. Among these datasets, we find physical information on each contestant (gender, age, home state, etc.), as well as personality types (described on the Myers-Briggs Type Indicator Scale), and the ranking and achievements of each contestant in various games and challenges within the show. These datasets are formatted specifically for use in the R language, so we export them as .csv files, and then pull them into Jupyter Notebook for use in Python.

We then clean the data, filling in missing data where possible or removing rows with missing values. From there, we put together the data frame that will be used for our analysis. This includes only those details about a contestant that one could find at the start of a season, as well as whether the contestant won the competition as the “Sole Survivor”.  This final variable, “win”, serves as our response in the study, while age, personality type, home state, and gender serve as our explanatory variables.

Following is our initial exploratory data analysis on the data that has been collected and cleaned.

# Exploratory Data Analysis

With some initial plots, we can see the relationship between the various explanatory variables and the ultimate result of winning the game. While these displays are not definitive, there is certainly something to be learned from them.

We see below the proportion of contestants from each state to have won the game in the past. Those states not shown have never had a contestant win the game before and are therefore proportioned at 0. It is shown that Rhode Island and Idaho both have a win proportion of .33. That is to say, of all the contestants from each of these states to have played the game, 33% have ended up winning.

![State Prop.](/State_Wins1.png)


Below we have a boxplot representation of the age range of winners and all other contestants on Survivor, split between men and women. We can see that the age range of winners for both men and women is smaller than the range of all contestants, however the median appears to be close to the same amongst both winning and losing groups.

![Age Ranges](/Age_Range.png)

Additionally, we see below a plot of the proportion of winners amongst the different personality types, again split between men and women. It is interesting to note that ENFJ, INFJ, ESTP, and ISTP all seem to have seen relatively high success in past games amongst men and women, with some variation.

![Personality Prop.](/Personality_Gender_Rate.png)

From our EDA, we can see some of the relationships that we might find after fitting our model. Moving forward, we fit the data to a model and find the model that gives us the best accuracy. We then interpret our results and make suggestions.

# Modeling

For this study, we test our data on several different models and parameter types to choose the best model to fit the data to. These models include a naïve bayes model, a logistic regression model, a decision tree model, a random forest model, and a gradient boosting model. We first encode our categorical variables and split the data into training and testing sets. Next, we create a function that accepts a model type, as well as the training and testing data sets for both the dependent and independent variables. The function then fits the data to the given model, and returns accuracy scores, precision and recall scores, F1 scores, a confusion matrix, and AUC scores for both the training and testing datasets. An explanation of these scores is given below. However, it will be noted here that in splitting our data into testing and training, we use two different methods of splitting. Splitting the data randomly returns overall better results than stratifying the full data before splitting, and so the following scores are being compared using the results from data being split randomly into training and testing sets.

An accuracy assessment allows us to evaluate the ability of the model to correctly predict the results within a dataset. It is the percentage of predicted values that match the actual value. The random forest and logistic regression models both returned the highest accuracy score of 89% on the test data sets. It should be noted that our data is imbalanced (due to there being so fewer winners of the competition than losers), and an accuracy score should therefore be “taken with a grain of salt”. With highly imbalanced data, models will be able to correctly predict whatever value has more representation in the full dataset (losers) but struggle to predict the less represented value (winners).

The F1 score is used to measure the harmonic mean of the precision and recall of a model. Precision is the proportion of positive identifications that are correct. Recall is the proportion of actual positives that were correctly identified by the model. A confusion matrix is used to show how many correct and incorrect positive and negative predictions are made by a model. With these scores, all models in our study struggle. This is due to the imbalanced nature of our data, as well as the relatively small amount of data that we have to work with. That being said, the random forest and logistic regression models perform better than the others.

Finally, the AUC score is also used to assess the performance of our models. It is a measurement of the area under the ROC curve, which compares false positive predictions to true positive predictions. The higher the AUC score, the better. Again, the logistic regression models and the random forest model score similarly as well as higher than other models. They both return a .68 AUC score.

We ultimately choose to use the random forest model due to its performance with the training and testing splits, as well as its lower risk of overfitting. We then use some trial and error in order to find the optimal parameters for the random forest model. Using 100 estimators and a maximum depth of 3, we fit the model to the entire dataset and find the following performance metrics:

|Metric|Value|
|:-------:|:------:|
|Accuracy| 0.92|
|F1| 0.43|
|Precision| 0.43|
|Recall| 0.43|
|AUC| 0.69|

We also use the model to extract those factors that most influence the prediction made, as well as each factor’s level of importance. In the case of this study, the variable importance levels are as seen below:

|Factor| Importance Level|
|:-------:|:----------------------:|
|Age| 40%|
|Personality| 30%|
|State| 23%|
|Gender| 7%|

Below, we fit the model to the new data, the current season of Survivor, to make a prediction on the winner of the current season.

# Results

Having fit the model to the data from the current season, we return the probabilities associated with each contestant winning the competition. We then find the contestant with the highest probability of winning, and that is our predicted winner.

Following this procedure, we find that our predicted winner of the competition is:
Liana Wallace, with a prediction probability of 0.1125.
Realistically, the prediction probability of Liana Wallace winning the competition is fairly low. In fact, at the point of writing this report, she has already been voted out of the competition. She did, however, make it further than most, and placed 7th overall.

# Conclusion and Suggestions

With such imbalanced and relatively small data, it is difficult to reliably predict the winner of any given season of Survivor. However, in this study, we have found certain factors that may influence the outcome.

Going forward, further studies could benefit from defining victory as making it to the final three contestants. This would help balance the data and would improve the F1 score of the model used. In addition, each season provides more data that can be used to make better informed predictions.

