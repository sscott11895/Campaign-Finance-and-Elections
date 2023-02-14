# Where's the Money? Campaign Finance and Election Outcomes in the 2016 U.S. Congressional Races

During U.S. elections, voters, candidates, and news outlets spend huge amounts of time, money, and brainpower to determine which candidate will win an election. Commonly, people want to predict the secret sauce that leads to victory. In this project, I review campaign finance data from the 2016 US congressional races and train a binary classification model to predict whether a candidate won their race or not based on information about their campaign finances. 

## **Full jupyter notebook with feature engineering and model fitting can be found [here](https://github.com/sscott11895/Campaign-Finance-and-Elections/blob/main/Campaign_finance_elections.ipynb).** 

The raw data set contained all the candidates that ran for either the House of Representatives, the Senate, or for president. I started out with just over 1800 candidates, and each candidate was represented by 51 different features. There was a general mix of numeric data related to contributions, loans, disbursements, receipts, and expenditures, and then there was a fair amount of categorical data, from where the candidate’s office was to party affiliation and whether the candidate was an incumbent or not. Once I was done processing the data, I had 1656 candidates represented by 20 features. The loss of observations stemmed from my decision to not use presidential data, as there was only one winner and over 100 candidates that ran during the election cycle. I was concerned that including this information would have affected my model’s predictions for Congress, where the campaigns often are less expensive and the importance of various financial factors may differ between the two types of races. 

In my model, I wanted to highlight financial data like contributions from individuals, candidates, and super PACS, loans taken, and how expensive the campaign was. Because campaigns vary in duration, there were a lot of missing values for financial data. I mainly relied on information from the Federal Election Commission website to understand the policies around reporting. After processing my data, I had 1186 people who did not win their races, and 470 winners. 

I worked on two models: A decision tree classifier as well as a random forest classifier. 

## **Decision Tree Classifier** 
I used One-hot Encoder on my categorical variables (candidate status as a challenger, incumbent, or ran in an open race), candidate office features (i.e. House or Senate rate), and candidate party affiliation (Democrat, Republican, or Other). I then took 80% of my data as the training data, 20% as test data. My final dataset was unbalanced, with nearly 3x more losers than winners. While this is to be expected for elections, I had to weigh my data accordingly. I weighted winners at 2.5 (overweighted) and weighted losers at 1. 

The mean accuracy on the test data and labels was 94.3%. The top features that the model focused on in order to make predictions were other committee contributions (83%), which would include the amount of money received from PACs and Super PACs, as well as if the the candidate was an incumbent or not (10%). In looking at the 19 occurrences where the model made incorrect predictions on the test data, we see that the model mostly guessed that these people had won when they really lost their election. Most of these observations had really large values for "other committee contributions", or super PAC contributions, which makes me think the model may be overemphasizing the importance of super PAC contributions. 

## **Random Forest Classifier**
I prepped the data in the same way as when I ran the Decision Tree Classifier. The mean accuracy on the test data and labels was 0.9578, or 95.8% accurate. The top features that the model focused on in order to make predictions were other committee contributions (18.5%), which would include the amount of money received from PACs and Super PACs, whether candidate was an incumbent or not (12%), total contributions to the campaign (11%), and how much the candidate contributed to his/her campaign as a fraction of total contributions (10%).

In looking at the 14 occurrences where the model made incorrect predictions on the test data, I saw that the model mostly guessed that these candidates had won when they really lost their election. This shows that placing a more even importance on certain features leads to slightly better predictions in this situation.

In conclusion, my results confirmed what many people assume to be true: Super PACs do play a large role in if you’re able to win, generally because it means you will experience a large influx of money. Additionally, incumbents normally have the upper hand when it comes to elections. 

In terms of limitations, my model did not take into account geography when making predictions because to split the data among states and territories would leave extremely small sample sizes. I do, however, think that geography can play a huge role. A democrat running in a blue state is more likely to win than a republican running in a blue state. Additionally, election data can be very difficult to use because of unbalanced samples, as we saw with the proportion of winners to losers, so it's important to weight the data accordingly. 


