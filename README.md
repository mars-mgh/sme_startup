# Identify Small Business Owners vs Startup Founders from their Reddit posts

by Marta Ghiglioni

### Executive Summary
To reach the best small companies where they need our financial insights the most we have to taget our blog towards the right industry subsect. This analysis uses natural language process and supervised machine learning to predict if a Reddit post was written in the Startups or Small Businesses subreddit.

The analysis resulted in a best model with an accuracy of 85%, and it is higly replicable result (proven by a 85% precision).

Also measuring the sentiment of these posts, they resulted to be overall positive for both categories, indicating that we should defenitly address these communities, dedicating both the support they need, where they look for it.

To do this with the language they use, the marketing team can use the presented model to gain insights on the most important features and verify through the model if the keywords for the articles they look forward to include in the online publication are predicted for the target they indend to address it towards.

---

### Data Source
Data are pulled from r/stratups and r/smallbusiness subreddits. Both are among the most activeon Finance & Business section on Reddit.

---

### Notebook Index
- [01 | Data Collection](./code/01_data_collection.ipynb)
- [02 | EDA & Cleaning](./code/02_eda.ipynb)
- [03 | Model](./code/03_model.ipynb)
- [04 | Sentiment Analysis](./code/04_sentiment_analysis.ipynb)

![Workflow](./presentation/workflow.png?raw=true "Workflow")

---

### EDA & Cleaning

I performed basic exploratory data analysis and consequential data cleaning.

In particular I started by handling nulls, deleted posts and in general and removed ones.

Then I decided to create a alltext feature, combining title and subtext.

Also, I investigated potential differences in engagement for the two subreddits, starting with comments and moving on to word count and post_lenght. If I wold have find any significant difference or peculiarity I would have engineered features describing it; unfortunately the two subreddits look extremely similar.

Then, to prepare my data for the modeling, I cleaned the text data using RegEx and lemmatize it.

I decided to store the entirety of my text in the same columns, to reduce the potential confusion of handling too many features and keep my code and data as clean and clear as possible.

---

### Models
First, I run a **Baseline Model** that predicts the majority class and results in a 62% Accuracy.

The I set a series of pipelines to run the following models using Count Vectorizer:

- **Random Forest** Manual
- **Random Forest** Grid Searched
- **Logistic Regression**
- **Multinomial Naive Bayes** 

Then I try using TF-TDIF and run a
- **Multinomial Naive Bayes** 


I choose Cvec over TFDIF to start with because in my data cleaning I removed all small size words and I want to take maxiumum advantage of "specific language" that might differenciate Startup and Small Business conversations.


#### Scores
Below a table summarizing the results from my models. Even thought the average scores for these models seem very similar, there is somewhat of a variation among them for different metrics and different classes.


|Model |precision | recall | f1|
| --- | --- | --- | --- |
|Baseline | 39% | 62% | 48% |
|Manual Random Forest| 85% | 85% | 85% |
|GridSearched Random Forest | 84% | 85% | 84%|
|Logistic Regression | 82% | 82% | 82% |
|MNBayes Count Vectorizer| 82% | 82% | 82%|
|MNBayes TF-IDF Vectorizer | 84% | 84% | 83 %|

These results show that the data is solid and the results consistent across different models.

#### Conclusion

The best model ends up being a Random Forest, having the more class balanced results.

Although a lot can be done in improving the performance of the model.

First of all pulling more data, then investigating further differences in engagement and feature weights.

---

### Sentiment Analysis

I perform I run a sentiment analysis model to identify if there is a difference between the two subreddits and if that could actually be a part of my predictive model. I end up realizing the sentiment is the same across the two subreddits.
This indicates that the subreddits are comparable and the tone is equally informative.

