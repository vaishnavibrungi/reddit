# **Problem Statement**

* Imagine this scenario: A grumpy backend engineer working at Reddit mistakenly deleted the "subreddit" column in the database in Australia. None of the subreddit links will populate with posts until the subreddit column data is recovered. While Reddit's team is working on restoring the deleted column, they decide to hire outside consultants to build a classification model that will predict which subreddit a random post belongs to. For consultants bidding for the project, Reddit’s team is asking for a sample model focusing on only two subreddits rather than all of the subreddits hosted on the site.
* This analysis seeks to build  an accurate classification model to predict which subreddit a given post belongs to.
* This analysis also aims to list down top features of each subreddit that determine where a random post belongs to.

# **Summary**

## violinist Data Cleaning 
* Renamed the column names.
* Column order was changed.
* Converted unix/epoch time to regular time stamp in UTC.

## cello Data Cleaning 
* Renamed the column names.
* Column order was changed.
* Converted unix/epoch time to regular time stamp in UTC.

## reddit_data Data Cleaning 
* Binarized the subreddit_name column.
* Using Natural Language Processing in the post_title column special characters were removed, words were tokenized and stemmer was used to return the base form of the word.
* Row with missing values in post_title column was dropped

## **Data Visualization**

* Barcharts were used to analyze the data.
* ROC Curve was plotted to analyze the predictions.

## **Data Modeling**
We tested each model below under both CountVectorizer and TFI-DF Vectorizer and proceeded with the one that had the better score:
* Logistic Regression
* Multinomial Naive Bayes
* Decision Tree Classifier
* Bagging Classifier
* Random Forest Classifier
* Extra Trees Classifier
* GridSearchCV

# **Data**

## **Data Source**
The data was collected by reading from the push shift API on Thursday, June 17, 2021.1000 most recent submissions from each subreddit were taken to conduct the analysis.

## **Data Dictionary**

|      Feature     |       Type      |   Dataset   |                      Description                      |
|:----------------:|:---------------:|:-----------:|:-----------------------------------------------------:|
|     author_id    |      object     | reddit_data |          User Id of the author   of the post          |
|     posted_on    | datetime64[ns]  | reddit_data |                   post creation time                  |
|     author_tag   |      object     | reddit_data | Tags assigned by   author of the posts to themselves  |
|    post_title    |      object     | reddit_data |                   Title of the post                   |
| post_description |      object     | reddit_data |               Description of the   post               |
|  subreddit_name  |       int       | reddit_data |                 Name of the subreddit                 |

# **Conclusion**

* The Logistic Regression model under the CountVectorizer, can predict whether a given post comes from the Violinist or Cello subreddit with reasonably better accuracy.
* Baseline accuracy rate was 50.7% whereas on test data our model's accuracy rate was 71.4%  which was better than the baseline accuracy and  the error rate of our model was 28.5%.
* The subreddits shared common words like "cello", "violin", "string", "bow", "music" and many others.
* Model predictions got a roc_auc_score of  0.808 which shows that our model can detect more numbers of True positives and True negatives than False negatives and False positives.
* The top ten words that determine whether a post belonged to the Violinist or Cello subreddit according to our model  :

| Violinist 	|      Cello   	|
|:---------:	|:------------:	|
|   violin  	|     david    	|
| violinist 	|     band     	|
|  teacher  	|     often    	|
|    play   	|    weight    	|
|    long   	|    either    	|
|    rest   	| bought first 	|
|  shoulder 	|    hickey    	|
|    keep   	|     singl    	|
|   pleas   	|     talk     	|
|  vibrato  	|     camp     	| 

* The above words make intuitive sense to belong to their respective columns. For example, On the Violinist column, "rest", "shoulder" which stands for shoulder rest, attaches to the back of the violin and rests on the shoulder and collarbone. It makes the violin comfortable to play for long durations, enabling proper posture and preventing injury."vibrato" is a slight fluctuation in pitch that's used to create warmth or richness of tone. On the Cello column, "David" which stands for David Darling who is an American cellist and composer," hickey" is an instore and online music center that sells accessories, music software, and much other music-related stuff, and Cellos usually weigh between 5 and 7 pounds which "weight" is referring to.

# **Next Steps**
 Our model only worked with one vectorized feature, the title column, to predict whether a given post belonged to the Nike subreddit. To fine-tune the model we can:
* We can include the stemmerized and vectorized text column, the author_flair_text column to see which level of players like a beginner, adult, etc. post frequently in both the subreddits.
* Analyze created_utc to check which subreddit people post frequently.
* Collect more sample data, possibly include comments as well as score.
* Use sentiment analysis to analyze the post and comments section whether they are constructive or critical.
* Remove vectorized words that are in the title of the Subreddit.





