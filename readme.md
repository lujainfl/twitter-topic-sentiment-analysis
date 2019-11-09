Note 1: This project description is to be read with the attached Capstone Presentation PDF AND 10 Jupyter Notebooks as directed per each section. 

# Twitter Sentiment Analysis by Topic for a Select Group
#### Data Science Immersive Captsone
### Author: Lujain Felemban


## Problem Overview 

Audience, Followers, Users, Customers, all are different names for the same idea. A population that shares a common  aspect who are provided a service of some kind, whether it is a product, an idea (talk), a policy(governance). One thing remains constant, this population's specific behavior is important to the service provider. That could be in how they use the service (eg. products), how they perceive the service (eg. talks), how they feel about the service (eg. policies), and so on. 

Many studies and business analytics research focus on this population behavior (eg. UX design), opinion (eg. elections polls), and identity (market/customer segmentation). Personally, when it comes to prediction, as it is the theme of a Data Science capstone project, I have always wished I could predict a person's reaction, opinion, or sentiment in contrast to my own towards a certain issue, topic, or anything. While important to me, the impact of such predictive product lies in how it can be applied elsewhere beyond the personal level. For example:

1- A politician cares about his/her governed body's opinion towards a hypothetical policy before implementing or even proposing it. 

2- An educator would cares about the students reaction towards a certain new implementation in the school system.

In the era of PR (Both Political Correctness and Public Relations), any player has to strategically position itself in today's current polarized millennial consumers. Wouldn't it be nice to predict and understand the specific audience reaction to a campaign/decision (eg. Gillet's latest "Don't Let Boys be Boys" ad) before investing a great amount of money in it? 

## Translate to Data Science Problem 

Now that I have the problem defined, the next step would be to translate to a data science problem, thinking about what the y (target variable to predict) and the correlated X (features/predictors) would be. After careful thought, I hypothesize that a person's opinion and sentiment towards certain issues, domain, or topics can be understood from their words. I definitly can do that myself after talking to someone for a long time. So, I set up the X to be a person's words.

Luckily it is 2019, a lot of people have access to the internet. Writing opinions or just thoughts on personal blogs, websites, pages, or social media accounts is pretty common. I chose twitter to go data mining for a number of reasons: 

1- Most accounts are completely public (unlike FB, Linkedin,or Instagram)

2- Easy to find a specifc population of interest to the service provided, I assume their followers represent their respective users or a true random sample of them. 

3- Many Data Science projects have been done on Twitter, which makes it easy to find refernces / packages for successful NLP and collection techniques on twitter Data. 


## Data Collection and Cleaning

There are two ways to collect data from twitter, either use an API OR scrape. As previously mentioned, many Data Science projects have been done on Twitter so much that there is an open -ource written library that makes scraping twitter data very easy. TWINT!

Now that I have tool to collect the data, next step would be to choose an appropriate exmaple account to work on. I have chosen the Public Investment Fund (PIF).

What is PIF!

- The Public Investment Fund

The Public Investment Fund seeks to become one of the largest sovereign wealth funds in the world. To achieve this, the Fund is building a world-class, diversified portfolio through investments in attractive, long-term opportunities at both the domestic and international level.

- PIF and Saudi Vision 2030

With the guidance of God Almighty , we have embarked on a new era of growth and leadership toward comprehensive economic and social development, with the launch of Saudi Arabia’s Vision 2030 : “Saudi Arabia… the heart of the Arab and Islamic worlds, the investment powerhouse, and the hub connecting three continents”. The Vision revolves around three pillars: a vibrant society, a thriving economy, and an ambitious nation.

The Public Investment Fund (PIF) Program (2018-2020) is one of twelve vision realization programs. The Program outlines our objectives in local and international investments that enable the diversification of the Kingdom’s sources of development and growth. The Program crystalizes PIF’s role as the engine behind economic diversity in the Kingdom by developing strategic sectors. It also seeks to grow PIF into one of the largest sovereign wealth funds in the world, as well as to build strong economic partnerships to deepen and strengthen the impact and role of Saudi Arabia on the regional and global stages.

Why choose PIF for this project:

1- Their account is relatively new, they have only started tweeting continoulsy since Jan 26th of 2019.

2- They have over 40K followers already.

3- I beleive the pubic, whether it be international investors, large businesses, or the Saudi population are interested.



- Please refer to the following Jupyter Notebooks in the order below for the code.
    - 0_data_collection
(Note that actual scraping code was run on an AWS cloude-based instance and took 5+ hours)
    - 1_en_users_extract
    - 2_data_filtering
After a lengthy filtering effort, a 300K long dataframe of english tweets of 430 different pif followers were collected. Columns include date, time stamp, text of tweet, hashtags, and mentions. 

## NLP Pre-Processing
- Please refer to the following Jupyter Notebooks/sections in the order below for the code.:
    - 3_data_munging
            - Pre Processing
Only the username, text, date-time columns were used. Basic NLP pre-processing were done on the text of the tweets to prepare for topic modelling

## Feature Extraction and Machine Learning Set Up 
- Please refer to the following Jupyter Notebooks/sections in the order below for the code.:
    - 3_data_munging
The collected tweets were combined to train an LDA topic model from gensim (a clustering algorithm) for (10 topics) after which a similarity metric for each tweet and each topic were assigned to create 10 new columns t represent how similar the tweet is to each topic, to act as the X.

Since our dataframe is relativaly small, the best LDA topic coherence score achieved is 0.3. The workflow was continue dto show future application. However, results and modelling metric would improve greatly or be more relaiable after LDA topic modelling is optimized. 

For each tweet string, a sentiment polarity for each tweet were extracted, assuming subjectivity is 1.0, by TextBlob pre-trained algorithm to be our Y.


## Exploratory Data Analysis
- Please refer to the following Jupyter Notebooks/sections in the order below for the code:
    - 4_data_eda
Some basic EDA work is done on the new dataframe containing topic similarity, username, and year, day, month for each tweet. Overall, I could not find an apparent correlation of X and y, which could mean that data are truly uncorrelated or that the correlation can not be simply visualized. In general, most tweets have a neutral sentiment polarity. Avg sentiment of topics in time showed some change that could correlate to time and topic, however the variance of 0.2 in sentiment (from a range of -1 to 1) is negligble. 

## Modeling 
- Please refer to the following Jupyter Notebooks/sections in the order below for the code:
    - 5_data_basic_modeling
    - 6_data_heavy_modeling (Powered by external GPU machine)
Modelling was difficult since there was no apparent correlation between X and y, however after choosing to classify the y into (positive or 1: 1 to 0.2, neutral or 0: 0.2 to -0.2, -1 or negative -0.2 to -1) and trying out a simple Multi Layer Perceptron Neural Network model, I was able to achieve an accuracy score higher than the baseline by a small but not negligible value. 

## Sample Case Use Result
- Please refer to the following Jupyter Notebooks/sections in the order below for the code:
    - 7_case_data
    - 8_case_predict
    - 9_case_results
A dataframe of a processed tweet written by PIF (we assume they have not published it yet) to creat a dataframe of the tweet models columns, date-time and usernames possiblities. For each tweet, the best performing model above predicted the sentiment (here by users OR preceived sentiment). A simple dashboard is created to visualize the predicted preceived sentiment distribution of users, as well as the averege sentiment change in day, month, and hour. 

## Conclusion

### Challanges


#####    - Data Collection : 

While Twint is a very powerful tool, it still takes time to collect the data. For the size of this project 75 - 1500 tweets for 429 users took ~5 hours, not including the time it took to filter the usernames. However, to productionalize such work, we would be working with thousands of users which takes time and need to clear Twitter terms of agreement for business use of public data. 

#####    - No Defined Metric

The Translated data science problem of this project assumes that the perceived sentiment of users about certain topics is the same as the sentiment of users on those same topics regardless of who;s talking about them. It's hard to measure the success of the data science work when we do not have a defined metric we can use to measure the preceived the sentiment vs predicted preceievd sentiment of each user.

#####    - Time

There was a very little time to ideate and work on this project (3 weeks) that some steps were done hastly, which affecte dthe overall results. Given more time, better results or at least understand of the data and problem can be achieved. 
    
#####    - Modelling based on features with no appearent correlation to y

There are no appearnt correlation between a tweets topic and the sentiemnt for each user.
#####    - Data Size

For a relativaely small number of users (429) the data is big (~300K observations) and at the same time not big enough for LDA modelling and EDA.
 

### Future Work 

####    - Hashtags 
There were no analysis done on hashtags due to timing, it would be interesting to analyze certain repating hashtags and the sentiment in respect to them (eg. Vision2030)
    
####    - Pre-trained LDA topic model
For the small size of data, it might yield better results to use a pre-trained LDA model to extract the topic from each tweets. Whith time and as the dataset grows bigger, a persnalized LDA model would then be appropriate.

####    - Time-Series based Sentiment Analysis
A time-series based user topic sentiment analysis of tweets can be a whole project on it's own. Specifically for account with a longer history (5 years), it would be inetersting to analyze the staionarity of sentiment or observe any seasonality.

####    - Modelling  
With more time and better machinary, perhaps some deep learning algorithms would perform better on the collected dataset, or a grid-searched optimized paramaters for more models. 

####    - Define a Metric (likes, RT)
We can define a metric of perceived sentiment such as number of likes or retweets or measured popularity of some sort.

####    - Tweet’s sentiment (by head account)
Consider the proposed tweet's sentiment in addition to the excatracted topics to forecast/predict approval of users (i.e. if the sentiments match, then a user approves)

####    - Resampling   
As the data mostly contain neutral tweets, we coould consider resamplling to solve the imbalnce problem and better predict more polarized tweets. 

####    - Wait for more followers to get bigger data
For such a new account, we might consider waiting a few weeks for the number followers togrwo from the thousands to millions and hopefully be able to use tweets from over 5K followers and get better results without overfitting.

### Resources

- Twint Link: https://github.com/twintproject/twint
- Gensim LDA Topic Modelling
- Textblob Library : https://textblob.readthedocs.io/en/dev/quickstart.html

### Collaborators and Enablers

Thank You to General Assembly, MiSK Academy, and AWS for providing resources, of which without this project would not exist.


Please reach out to me on Linkedin OR github if you have any questions or interested in collaboration
https://www.linkedin.com/in/lujainfelemban/
