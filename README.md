# Introduction

The reality TV show Survivor has been airing for over 20 years, mainly due to its great success and popularity in the United States. The general plot of the show is that 16-20 selected people are taken to an uninhabited location with little supplies. These people are expected to survive, participate in challenges, and vote one person off the game every 3 days, until there are only a few left. The winner is then chosen by the contestants who have already been voted off.  One aspect of the game that fascinates viewers is the fact that the winner is always seemingly impossible to predict among the players at first glance. Because the game not only includes fitness and intelligence, but also social factors, there is no specific "type" of person that consistently wins the game. Therefore, it is our intention in this analysis to see if a model can be created that accurately predicts whether a player will win the game, based solely on geographical factors. This will help in determining whether there are some types of people who have a higher tendency to win the game, regardless of how they played.

# Collecting and Cleaning Data

We began our study by gathering several datasets from online that held information about the Survivor show and its contestants. Among these datasets, we found physical information on each contestant (gender, age, home state, etc.), as well as personality types (described on the Myers-Briggs Type Indicator Scale), and the ranking and achievements of each contestant in various games and challenges within the show. These datasets were formatted specifically for use in the R language, so we exported them as .csv files, and then pulled them into Jupyter Notebook for use in Python.

We then clean the data, filling in missing data where possible, or removing rows with missing values. From there, we put together the data frame that will be used for our analysis. This includes only those details about a contestant that one could find at the start of a season, as well as whether the contestant won the show as the “Sole Survivor”.  This final variable, “win”, serves as our response in the study, while age, personality type, home state, and gender serve as our explanatory variables.

Following is our initial exploratory data analysis on the data that has been collected and cleaned.

# Exploratory Data Analysis

With some initial plots, we can see the relationship between the various explanatory variables and the ultimate result of winning the game. While these displays are not definitive, there is certainly something to be learned from them.

We see below the proportion of contestants from each state to have won the game in the past. Those states not shown have never had a contestant win the game before and are therefore proportioned at 0. It is shown that Rhode Island and Idaho both have a win proportion of .33. That is to say, of all the contestants from each of these states to have played the game, 33% have ended up winning.

![State Prop.](/stat426-fall2021/classproject-front-row/State_Wins1.png “Win Prop by State”)

Below we have a boxplot representation of the age range of winners and all other contestants on Survivor, split between men and women. We can see that the age range of winners for both men and women is smaller than the range of all contestants, however the median appears to be close to the same amongst both winning and losing groups.

![Age Ranges](/stat426-fall2021/classproject-front-row/Age_Range.png “Age Ranges of Men and Women”)

Additionally, we see below a plot of the proportion of winners amongst the different personality types, again split between men and women. It is interesting to note that ENFJ, INFJ, ESTP, and ISTP all seem to have seen success in past games amongst men and women.

![Personality Prop.](/stat426-fall2021/classproject-front-row/Personality_Gender_Rate.png “Win Prop by Personality and Gender”)

From our EDA, we can see some of the relationships that we might find after fitting our model. Moving forward, we will fit the data to a model and find the model that gives us the best accuracy. We will then interpret our results and make suggestions.

# Modeling

For this study, we tested our data on several different models and parameter types. These included a naïve bayes model, a logistic regression model, a decision tree model, a random forest model, and a gradient boosting model. We first encoded our categorical variables, and then split the data into training and testing sets. We created a function that would accept a model type, as well as the training and testing data values for both the dependent and independent variables. The function then fit the data to the given model, and returned accuracy scores, F1 scores, and AUC scores for both the training and testing datasets. An explanation of these scores is given below.

An accuracy assessment allows us to evaluate the ability of the model to correctly predict the results within a dataset. It is the percentage of predicted values that match the actual value. Using this form of assessment, we found that three models were tied with the greatest accuracy on the testing subset. Our models for logistic regression, decision tree, and random forest methods each resulted in an accuracy of about 93.6%.

The F1 score is used to measure the harmonic mean of the precision and recall of a model. Precision is the proportion of positive identifications that are correct. Recall is the proportion of actual positives that were correctly identified by the model.

# Results


