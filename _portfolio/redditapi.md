---
caption:
  title: Subreddits r/Conservatives and r/democrats
  subtitle: Explore discussions in each subreddit and train models to classify posts into respective political leaning
  thumbnail: assets/img/portfolio/redditapi/demo-repub.png

title: Subreddits r/Conservatives and r/democrats
subtitle: Explore discussions in each subreddit and train classification models to classify posts to get insights into political leaning of a typical reddit post
image: assets/img/portfolio/redditapi/demo-repub.png

---

## Preamble

Public opinion towards political parties have a role to play in elecion outcomes. Different political parties have different views of public policies, and these public policies affect the general populace, businesses or even individuals. Businesses could benefit from preparing for any policy changes when during election where political leaders may change.

Reddit is a social media platform moderated by the community themselves and has a relatively large userbase, in large part due to anonymity of user (Squirell, 2018). Compared to other social media platforms, reddit is likely to have the least biased posts on political leaning, which is a relatively objective data to try and determine public sentiments.

A classification model that can accurately classify posts between `r/Conservative` and `r/democrats` could form a good foundation for further development like performing sentiment analysis and possibly predicting future election outcomes.

## Objective

The objective of this project is to build a classification model that can accurately classify a post into either `r/Conservative` or `r/democrats`.

## Analysis and Findings

#### Webscraping data using Reddit's API

I first scrape about 1,000 posts (maximum allowed from reddit) from the subreddits `r/Conservative` and `r/democrats` and use pandas profiling report for preliminary review.

For `r/Conservative`, I note the following:

1. 'selftext' column which contains the content of the reddit posts are empty in this subreddit. Looking through the subreddit `r/Conservative`, each post mostly usually contains title and a news link and rarely a text. While this would be most useful for modelling, there is no data. An alternative would be using comments data, which I will scrape later on.


2. 'title' column has no missing value. Apart from the content of the posts, the title is probably the closest identifier of the post to a particular subreddit. This would be my first option for modelling.


3. 'link_flair_text' column has 9 missing data (2.2% of dataset). Flair in reddit is used as a form of subcategorisation within the subreddit (Mathew, 2019). There are three types of flairs for posts : Flaired Users Only, Satire - Flaired Users Only and Misleading Title. These are not very useful for modelling later so we will not consider this.


4. 'domain' shows the source of the link eg. foxnews, dailywire, washingtonexaminer etc. There are no missing values under this column so this could be considered for modelling later on. This is especially since for instance, foxnews is well-known to be controlled by Republicans so we are likely to see more links in this subreddit from this news channel.


5. 'subreddit' column will be the label for our classification model later.

For `r/democrats`, I note the following :

1. 94% of the 'selftext' column is empty. Similar to the subreddit `r/Conservative`, each post mostly usually contains title and a news link and rarely a text. While this would be most useful for modelling, there is no data. An alternative would be using comments data, which I will scrape later on.


2. 'title' column has no missing value. Similar to `r/Conservative`, this would be the first option to use for modelling since it closely reflects the content of the post.


3. 'link_flair_text' column has 45.4% missing data which is pretty substantial. I would not consider this for modelling.


4. 'domain' shows the source of the link eg. self.democrats, twitter, youtube etc. There are no missing values under this column so this could be considered for modelling as well.


5. 'subreddit' column will be the label for our classification model later.

Based on above analysis, I decided to scrape just the comments and titles for this project, since the content for posts are lacking in these subreddits.

I used Python Reddit API Wrapper (PRAW) to extract, which turned out to be faster than json.

![](assets/img/portfolio/redditapi/praw-v-json.png)

`r/democrats` had more titles (possibly because there are duplicate titles under `r/Conservative` where several or the same user(s) share the same title and newslink to get more redditors' attention on the newslink). Conversely, there are much more comments on `r/Conservative` than for `r/democrats`. Also, praw was able to scrape all sub-comments, resulting in much more data available for comments.

Based on above, I will used praw-scraped datasets as overall it scraped much more data than using json.

#### Data Cleaning and Exploration

With the titles and comments, prior to modelling, I preprocessed it to expand contractions, remove punctuations and tokenizing. On top of that, I also created two separate files for each dataset (ie. titles and comments) where I did stemming on one, and lemmatized the other. This is to see which ones can work better in modelling later.

The target variable is also converted to a binary where `r/Conservatives` are labelled as 1 and `r/democrats` labelled as 0.

I visualise the most frequent words used in titles of both subreddits using a wordcloud.

![](assets/img/portfolio/redditapi/wordcloud-titles.JPG)

Most frequent word in titles is **Trump**, which is no surprise. At the time this project was done, it was days before the transition for Biden as President of the United States, and Trump (the current President) and his supporters did not make it easy. There was a riot at the US Capitol, innocent bystanders were killed, some policemen who were truly loyal to Trump failed to uphold their duty during the violence. Several articles came up on these on various news channels.

**Twitter** came up here because Trump's twitter acount was initally suspended for 6 hours but it has since been permanently suspended due to risk of further incitement of violence (in relation to the US Capital riots). (Twitter Inc. 2021)

**Elon Musk** came up here because several news channels reported that his net worth exceeded Jeff Bezos (Amazon CEO) to become the richest person in the world.

Looking at the words used in comments of both subreddits..

![](assets/img/portfolio/redditapi/wordcloud-comments.JPG)

**bail, parler, lawyers** are related to the same issue. Parler is a social network platform known for embracing people who are banned by Twitter, YouTube and other platforms. Parler's site is supported by Amazon Web Services (AWS). Amazon decided to effectively terminate Parler's account as it is deemed to be directly contributing to violence by Trump supporters. Parler has since filed a federal lawsuit against Amazon for removing supporting of its website. (Hayes, 2021)

Now let's look at the words for that come up in the respective subreddits.

**r/democrats**

![](assets/img/portfolio/redditapi/wordcloud-titles-dem.JPG)

In the democrats camp, we see **trump** being the most used, along with **impeachment**. The **14th amendment**, Section 3 which provided an alternative path for disqualification of a person from holding office, if they have engageed in "insurrection or rebellion" in the United States (which we saw in the US Capitol riots.(Wolfe, 2021)

This shows how democrats are discussion options to remove Trump from office for inciting a mob that stormed the Capital, days before Biden takes over the Presidency.

**r/Conservative**

![](assets/img/portfolio/redditapi/wordcloud-titles-con.JPG)

Over at the conservatives camp, **trump** is equally mentioned, along with **twitter**. Twitter had so much mentions probably because when Twitter banned Trump, the conservatives were livid and expressed their displeasure in this subreddit.  

#### Model Selection and Evaluation

In model selection, I first fit data into a few pipeline models, without changing the parameters. This will be the baseline model from which I will then score and select the best performing model to go forward with.

To evaluate which one is the best performing model, there a few metrics considered below (Vidhya, 2020) :

| Metric | Elaboration and Analysis |
| :-----: | :-------- |
| Accuracy | provides fraction of predictions that the model got right (ie. number of correct predictions / total number of predictions). This metric may not work well on imbalanced classes like the data I collected, but since I have balanced the classes with `RandomOverSampling`, I can rely on the accuracy metric.  |
| Precision | provides the fraction of correctly identified positives out of all predicted positives. [TP / (TP + FP)]. This indicates how much we can trust the algorithm when it predicts a class. |
| Recall/Sensitivity | provides the fraction of correctly identified as positive out of all positives. [TP / (TP + FN)] . This shows how many of the true labels of the class is predicted correctly. |
| F1-score | a harmonic mean of precision and recall. While we want to maximise precision and recall, it is a trade-off. Since I have no bias towards any classes (ie. predicting a post to be from `r/Conservative` is as good/bad as predicting a post to be from `r/democrats`), the F1 score may not as important as accuracy, for this project. |

Once selected the best performing model, I will then use that model and tune its hyperparameters.

I run the four datasets abovementioned into 5 different classfication models in a pipeline with count vectorizer or tf-idf vectorizer, with results below :

![](assets/img/portfolio/redditapi/baseline-model-score.JPG)

From here, there are several observations:

1. Comments always have a better score than titles, so I willl use the comments data to train in the final model. This is expected since there is more data available in comments than titles (ie. there can be several hundreds of comments on a particular post)  

2. Generally, stemmed words have a better score than lemmatized words. This is likely because words used in both `r/Conservative` and `r/democrats` are already very distinct from each other, such that a harsher truncation by stemming makes the model more effective.

3. Comparing scores on train set, the `RandomForestClassifier` and the `DecisionTreeClassifier` were the best performing model. However, when looking at the average `cross_val_score`, the `RandomForestClassifier` did better.

Based on this analysis, I will move forward with the `RandomForestClassifier` algorithm.

With the `RandomForestClassifier` algorithm, I then use gridsearchcv to tune its parameters to try and make it work even better. Looking at the best parameters, we observe some interesting insights below.

| Hyperparameter | Hyperparameter Value |
| :-----: | :--------: |
| cvec__stop_words | None |
| cvec__ngram_range | (1, 2) |


1. Surprisingly, not removing stop words improved the model. This suggests that stop words help in making sense of the data with respect to each subreddit. It is likely that stopwords help with the context in each of these subreddits.

2. ngram range is (1,2) which means both unigrams and bigrams (ie. single words or two words back-to-back) are considered together in training the model to help it perform better.

Now using the best parameters, I run the model again with the following scores :

![](assets/img/portfolio/redditapi/tuned-model-score.JPG)

The model did very well and is able to classify post correctly in the respective subreddits 97.9% of the time.

![](assets/img/portfolio/redditapi/roc-auc.JPG)

The ROC-AUC curve represents the degree or measure of separability between the subreddits. AUC score measure between 0 and 1 and a good score is one that is closest to 1, with one being the perfect model. With our well performing model, it is reasonable to expect an AUC score close to 1.

## Conclusion and Further development

Random Forest Classifier performed really well to classify a post between `r/Conservative` and `r/democrats`. This is expected as from the data exploration done earlier, we see pretty distinct words used in each of these subreddits. While we would expect similar topics to be discussed or similar mentions in both `r/Conservative` and  `r/democrats`, from our results, it appears that the content that is discussed in each subreddit goes in very different directions (ie. redditors use very distinct words for each subreddit).

**Further Development**

With this model, we can perform further sentiment analysis and from public sentiment, we could predict outcomes of future elections. Businesses would then be able to prepare for policy changes and if needed pivot the business in favour of any upcoming policy changes.

## References

"Reddit is the best social media site because it gets community right" (Squirrell, 2018)
https://qz.com/1309562/reddit-is-the-best-social-media-site-because-it-gets-community-right/

"Permanent suspension of @realDonaldTrump" (Twitter Inc. 2021)
https://blog.twitter.com/en_us/topics/company/2020/suspension.html

"Amazon Rips Parler Lawsuit, Calling Companies "Unable or Unwilling" to Police Its Site" (Hayes, 2021)
https://deadline.com/2021/01/parler-sues-amazon-trying-to-kill-site-donald-trump-1234671259/

"How to Choose Evaluation Metrics for Classification Models" (Vidhya, 2020) https://www.analyticsvidhya.com/blog/2020/10/how-to-choose-evaluation-metrics-for-classification-model/

{:.list-inline}
- Date: 14 Jan 2021
- Category: data exploration, logistic regression, miltunomial naive bayes, decision tree classifier, random forest classifier, support vector classifier, count vectorizer, tf-idf vectorizer, stemming, lemmatizing, random oversampling
