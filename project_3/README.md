# Project 3: Web APIs & Classification

## Problem Statement

Using Reddit's API, posts from two subreddits (Basketball and Baseball) were collected. Using TFIDFVectorizer and Naive Bayes (Multinomial), posts were accurately differeniated and classified into basketball and baseball.  

### Context
We are working for SPORTS ILLUSTRATED, one of the biggest Sports magazine in the US. We have been receiving many commentaries from readers and these commentaries span from swimming to golf, including baseball and basketball. My company is having trouble sorting out all the commentaries according to their content and has engaged the data team to resolve this issue by developing an automated system to classify the commentaries according to their sports genre so that the respective editorial teams could process them on time. Our team has proposed to start with classifying Basketball and Baseball based on subreddit posts.

## Data Collection

1) Checked that the subreddit APIs were accessible.
2) For each request, Reddit only provided about 27 posts. A loop was created to hit Reddit about 40 times to extract at least 1,000 posts. While obtaining more posts was desirable, Reddit capped user at 1,000 posts for each subreddit. In hitting Reddit, 3-6s break time between requests were created to allow other people's requests. Beyond 40 times, posts were duplicated.
3) The raw posts were saved as csv files at the end of each loop to save time in running the loop.


## Data Cleaning 

1) The columns of interest were identified as "title" and "selftext". While there were no missing values in 'title', 'selftext' had 736 of missing values. 121 'selftext' missing in basketball and 615 'selftext' missing in baseball. 
2) There was consideration to drop 'selftext' as the missing values were unevenly distributed. However, the decision was to retain 'selftext' as it contained additional data and relevant words that were helpful in training and improving model accuracy. Therefore, the decision was to combine 'selftext' and 'title' to obtain a 'bigger' bag of words since they were both strings. 
3) The only outliers identified were duplicated posts that were dropped as they could skew the word counts.
4) Given Reddit's cap on 1,000 posts, Basketball and baseball had 932 and 924 unique posts respectively (1856 unique posts in total). 


## Preprocessing of text
1) Performed test-train split
2) A function was created to process the combined raw text ('title' and 'selftext') manually. The preprocessing consisted of the following steps:
    - Removed HTML
    - Removed non-letters
    - Converted to lower case, splitted into individual words
    - Removed stop words (included new words like 'http', 'www', 'com')
    - Lemmatized words
    - Joined the words back into one string separated by space

3) However, I was not sure if preprocessing indeed improves the accuracy of my classifier so I performed further EDA using simple CountVectorizer and Logistic Regression in the next step to check.

4) The baseline prediction for any post to be basketball was 0.5 as there were equal number of basketball and baseball posts. This is the worse prediction of probability that could be obtained.

## EDA using CountVectorizer

1) To check if preprocessing (previous step) aids in improving the model accuracy, using CountVectorizer and Logistic Regression:
    a) Without preprocessing, the results were:
    - Total features: 11598
    - Train ROC AUC: 0.9992
    - Test ROC AUC: 0.9181
    b) With preprocessing, the results were:
    - Total features: 8825
    - Train ROC AUC: 0.9992
    - Test ROC AUC: 0.9398
In short, preprocessing improved the accuracy of the model slightly and reduced the number of features given applied techniques like lemmatization and elimination of digits. Preprocessed data were used subsequently.

2) Based on the top 30 most common words, there seemed to be a clear distinction between baseball and basketball posts as most of these words were only seen in either baseball or basketball post. This explained the relatively high ROC AUC scores when performing simple CountVectorizer and Logistic Regression earlier. 


## Modelling

1) Pipeline function was created to perform grid search through 2 vectorizers (CountVectorizer and TfidfVectorizer) and 4 models (1. LogisticRegression; 2. BernoulliNB; 3. MultinomialNB; 4. KNeighborsClassifier). 8 combinations were explored and their respective ROC AUC test scores:
    1. CountVectorizer & Logistic Regression (0.9397)
    2. CountVectorizer & BernoulliNB (0.9332)
    3. CountVectorizer & MultinomialNB (0.9057)
    4. CountVectorizer & KNeighborsClassifier (0.8103)
    5. TfidfVectorizer & LogisticRegression (0.9397)
    6. TfidfVectorizer & BernoulliNB (0.9353)
    7. TfidfVectorizer & MultinomialNB (0.9418) - SELECTED
    8. TfidfVectorizer & KNeighborsClassifier (0.9246)

2) The scores of ROC AUC, f1, recall and precision were returned. The key evaluation metric selected was ROC AUC as it focuses equally on positive and negative results. Given that basketball and baseball have equal importance, ROC AUC score appeared to be the most suitable metric.

3) Fitting TFID and Multinomial with their optimised parameterson the data, the following ROC AUC scores are obtained. 
    -Train ROC AUC: 0.9827
    -Test ROC AUC: 0.9374

4) Given the difference in sensitivity and specificity scores, the selected model seemed to perform better at identifying baseball posts compared to basketball.
    -Sensitivity: 0.9657
    -Specificity: 0.9091


## Conclusion and Recommendations

### Conclusion
Using gridsearch, Multinomial classifier with TFIDVectorizer was most effective in  classifying posts into Basketball and Baseball posts. This could help my company, SPORTS ILLUSTRATED, to effectively direct relevant basketball and baseball commentaries to respective editorial teams.

In addition, based on my Logistic Regression coefficients, a set of words with high differentiating power was obtained. There were differences in the words used in the basketball and baseball Reddit communities.
    
   -Basketball: More discussions/sharing on techniques to improve basketball. Commenters are usually basketball players, who are interested in improving their skills. For example, words 'dunk', 'shoot', 'jump', 'vertical', 'form', 'improve', 'rim' etc. For those who are more interested in basketball games tend to comment in subreddit 'nba'.
    
   -Baseball: Discussion focused on baseball teams and games (more like a baseball fan community). Commenters are mostly likely fans who follow baseball games closely. For example, 'Mets', 'Astros', 'SOX', 'Red', 'Yankee', 'Angels' etc. The equivalent for basketball is 'nba' in subreddit.


### Recommendations

1) My selected subreddits - 'Basketball' and 'Baseball' were distinctively different so it was not much of a challenge to differentiate them. Most of the classifiers obtained high scores. Perhaps it will be more interesting to explore subreddits like 'nba' and 'basketball' as they may be harder to differentiate, yet there are some subtle differences (suspect 'nba' to be a fan community, while 'basketball' is for basketball enthusiast). 

2) With our current results, magazines or advertisers may want to better target their audience by producing content well aligned to the interest of the communities. For example, the basketball community maybe more interested in basketball related merchandise (e.g. balls, shoes, coaches, etc.) and information (e.g. techniques, skills), while baseball commenters maybe more interested in baseball games related merchandise (e.g. merchanise of teams) and information (e.g. news on baseball teams and players).

