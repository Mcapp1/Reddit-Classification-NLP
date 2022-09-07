# Project 3: Reddit


## Scenario

Scenario
You're fresh out of your Data Science bootcamp and looking to break through in the world of freelance data journalism. Nate Silver and co. at FiveThirtyEight have agreed to hear your pitch for a story in two weeks!

Your piece is going to be on how to create a Reddit post that will get the most engagement from Reddit users. Because this is FiveThirtyEight, you're going to have to get data and analyze it in order to make a compelling narrative.

## Problem Statement

What characteristics of a post on Reddit are most predictive of the overall interaction on a thread based on the number of comments? Which characteristics determine if a post rises above or falls below the median of scrapped posts? Once we have performing models, we can select ideal model based on scenario use

## Executive Summary

This project is split into two notebooks. The contents of the first notebook contains only scrapping Reddit posts and the contents of the second is the rest of the project (data cleaning, modeling etc)

This notebook scraps 16,900 Reddit posts all derived from the front page of Reddit. Most posts are from recently hot reddit posts however in order to get enough data, many posts are scrapped from the top reddit posts of all time. These posts are easily visualized when viewing the distribution of data. Additionally these posts are explained in detail and handled appropriately in the notebook.

The data consists of:
- **Subreddit**: Original page of post
- **Title**: Post’s title text, additionally this is going to be the main feature as this notebook vectorizes the title text
- **Title Length**: Length of Title
- **Score**: The number of 'upvotes' per post
- **Comments**: The number of comments the post has
- **Created**: Date and time of submission

After scrapping 16,900 reddit posts this notebook examines the data and cleans appropriately to bring the total posts down to 12,875. This is done by getting rid of any posts with no comments as we are only examining posts with comments. Posts may have no comments because the creator disallowed or the post is too new, regardless the performance of the post is not represented when the post has no comments. This notebook gets rid of any posts with duplicate titles: Posts may have been submitted on multiple subreddits. This notebook gets rid of non alphanumeric characters, emojis included. This notebook gets rid of non discernable titles, such as titles with very short lengths where a word is not comprised.

Once the data is cleaned this notebook runs several models consisting of logisitc regression, random forest and decision tree. The best performing models are in the table below. The table consists of the type of model, accuracy, precision, recall and whether or not the model is overfit.

|Model_Number|Model_Type|Accuracy|Precision|Recall|Overfit?|
|------------|----------|--------|---------|------|--------|
|Model_1|Log-Reg|60%|65%|58%|Yes|
|Model_2|Log-Reg|54%|80%|53%|No|
|Model_3|Log-Reg|57%|66%|56%|No|
|Model_4|Random-Forest|57%|64%|56%|Yes|
|Model_5|Log-Reg|64%|74%|64%|Yes|

With the data cleaned and models ran we can interpret several conclusions

## Data Dictionary
|Variable|Variable Type|Definition|Notebook|
|--------|-------------|----------|--------|
|r_all|csv|first scrape of reddits front page|1|
|reddit_3|csv|combined first and second scrape|1|
|reddit_4|csv|3rd reddit scrape|1|
|reddit_all|csv|combined 3rd scrape and reddit_3|1|
|reddit_complete|csv|legible complete dataframe of all reddit scrapes with converted utc time|1|
|df|DataFrame|cleaned reddit_complete notebook|2|
|sub|pd.series / column of df|subreddit for which the submission was originally posted|2|
|title|pd.series / column of df|text of title for each submission|2|
|title_length|pd.series / column of df|length characters for each title|2|
|score|pd.series / column of df|number of upvotes each submission has|2|
|comments|pd.series / column of df|number of comments on each submission|2|
|created|pd.series / column of df|time and date each submission was posted|2|
|df_trial_1|DataFrame|Features for first model which uses count vectorizer|2|
|df_trial_2|DataFrame|Features for second model which uses Tfidf vectorizer|2|
|top_subs|DataFrame|DataFrame consisting of top 5 scoring subreddits|2|
|misclass|DataFrame|Dataframe consisting of all misidentified predictions on only the top_subs dataframe|2|

## Conclusions
Our problem statement was to identify which characteristics of a post on Reddit are most predictive of the overall interaction on a thread as measured by the median number of comments.

After running several models we can conclude:
- Model 2 is best used if attempting to write a post which attracts attention
    - Utilizes Precision
- Model 3 is best used if trying to view or learn from submissions where comments are accurately predicted to rise above or fall below the median.
    - Utilizes Recall
- Logisitc regression models consistently performed best whereas Random Forest and Decision Trees were constantly overfit

## Recommendations
- Our last model which was run on the top subreddits runs the best. 
- Models on the top scoring subreddits indicate initial models are very good at predicting submissions with comments on the higher end of the distribution spectrum. 
- The issue is that the model isn't significantly better than any of the models ran with the entirety of the data and many features are the exact same. 
- However the model performing better indicates we could use similar methods to run a model on the entirety of the data that performs best.
- Given more time, incorporate title lengths as a feature and see what is found since our top scoring subreddit there is a significant impact of title length