# Predicting Subreddits using NLP and ML Models

### Problem Statement
Fantasy vs Sci Fi Subreddits: 
Which model will accurately differentiate between these two subreddits ?

The definition of  a successful model is described by looking at two metrics of evaluation. The first metric is the variance between the training and testing accuracy scores, in other words whether overfitting occurs. The second metric is looking at the testing score, looking at models with the highest testing score.

### Background Information

Reddit is a social news website and forum where content is socially curated and promoted by site members through voting. The site name is a play on the words "I read it."

Reddit member registration is free, and it is required to use the website's basic features.

The site is composed of hundreds of subcommunities, known as subreddits. Each subreddit has a specific topic, such as technology, politics or music. Reddit's homepage, or the front page, as it is often called, is composed of the most popular posts from each default subreddit. The default list is predetermined and includes subreddits such as "pics," "funny," "videos," "news" and "gaming."
https://searchcio.techtarget.com/definition/Reddit

r/Fantasy:
"r/Fantasy is the internet's largest discussion forum for the greater Speculative Fiction genre."
https://www.reddit.com/r/Fantasy/

r/AskScienceFiction:
"It's like Ask Science, but all questions and answers are written with answers gleaned from the universe itself.Use in-universe knowledge, rules, and common sense to answer the questions."
"A suitable question for /r/asksciencefiction: Pertains to one or more specific fictional universes (of any genre)."
https://www.reddit.com/r/AskScienceFiction/

### Data Dictionary
| Feature  | Type  |  Description |
|---|---|---|
| subreddit      |  int64 |  1 for Fantasy, 0 for AskScienceFiction|
|  title  | string  | Title of the subreddit post|
|  selftext    |  string | Main body of the subreddit post  |
|status_word_count |int64|Word count for selftext|

### Analysis and Recommendations

In order to effectively answer: what model will best classify the subreddits as Fantasy or Science Fiction I divided this task into two notebooks. The first notebook collected data by scraping a subreddit API. Because I was only able to scrape 100 posts at a time, I effectively made a while loop that would scrape 10,000 posts for each subreddits. The loop dropped any posts that contained 'deleted' or 'removed'. Finally the posts were combined into a data frame and exported as a csv. The second notebook is where the modelling took place. The first step taken to answer the question was to further clean the data by removing outliers and any unwanted punctuations. EDA was then performed on the data in order to effectively understand patterns. The last step was to make various models using both count vectorizer and TFIDF vectorizer. Once all these models fitted, all that was left was to compare them together in order to find the best one.

Looking at all 6 of the models, the model that best classifies the subreddits into either Fantasy or Science Fiction is the Random Forests using TFIDF Vectorizer. This was chosen as the best model for the following reasons. Taking training scores into consideration, the model did not score the highest. The highest scoring model after tuning was the XG Boost using TFIDF vectorizer. It scored a training score of 0.976. With that said the TFIDF Random Forest model had a slightly lower training score of 0.971. What makes the difference between these two models is the testing score. The Random Forest model is the model that scored the highest in terms of testing score,0.94, and that is one of the metrics by which I evaluated these models. Scoring high on unseen data shows how well a model really does. The other metric by which I chose this model was the low variance between training and testing, it is equivalent to approximately 0.03. Although it is slightly overfit, the variance is low enough to accept the model. With that said although it only scored as the second highest for training score, TFIDF Random Forest model scored the highest in testing score and was therefore chosen as the best model.

Now that we have chosen our best model, we can evaluate how good it is at classification. Plotting a confusion matrix we can see that our model does pretty well at classifying our subreddits. This can be further justified by looking at the precision and specificity score. Precision outlines how well did the model predict Fantasy classes, it scored 94.3%. While specificity outline how well did the model predict Sci Fi classes, it scored about 94.3% as well.What this means is that the model does an equivalent job at classifying a Fantasy and a Science Fiction subreddit. This can be further explained by reminding our audience that the data was well balanced. Next looking at the accuracy of the model, we can see that the model is able to successfully predict 94% of the observations. This remains a high scoring model and is accepted  as the model that best answers the problem statement. Overall, it is concluded that this investigation has successfully addressed and answered the problem statement of finding the best model at classifying posts into  Fantasy or Science Fiction subreddits. 

After choosing the best model for my specific problem statement, this can be taken a step further. A model that takes in all the subreddits would be used to make recommendations to users on what subreddits they could posts their thread. For instance, if a user posts a thread in the AskScienceFiction subreddit, the model incorporated  would classify if the posts is best suited for that subreddit in particular. The model would take the post and predict in which subreddit it falls best. If the post is not suited for that subreddit, the model will make recommendations on where the user should post their thread, for instance on the Fantasy subreddit. Doing so will increase user commitment, engagement and satisfaction. As well as further accommodate users (to better respond to their needs).
