# We Rate Dog
This is a course project from Udacity. In the project, I gathered data from the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates), also known as WeRateDogs, which includes date and content of each tweet. I also query the Twitter API to get the number of favorite and retweet of each tweet.   
After conducting data wrangling and cleaning, I plotted the distribution of favorite and retweet and confirm that they have a linear relationship.  
  
The wrangling effort is summarized as below:

**1. Data Gathering**  
In this project, three sets of information were gathered.  

1) The WeRateDogs Twitter archive.   
This piece information was gathered by directly download the file provided at Udacity's project instruction page.  
  
2) The tweet image predictions.   
The breed of dogs are predicted by a neural network using the images and this file is hosted on Udacity's servers using the URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv. I download this information from Udacity server by using response=requests.get(url) command in the jupyter notebook.  
  
3) Each tweet's retweet count and favorite ("like") count.   
To gather this information, I first retrived tweet ID from WeRateDogs Twitter archive. Then I set up my Twitter developer account and with an app created. This process provide consumer_key, consumer_secret, access_token and access_secret that are needed in order to query twitter API. Next, I queried the Twitter API for each tweet's JSON data using Python's Tweepy library. This JSON data was store in a file called tweet_json.txt file.  
  
  
**2. Data Wrangling**  
In this step, data were assessed and 9 quality issues and 2 tidiness issues were identified.  
  
**Quality issues:**  
1) There're missing data in in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, and expanded_urls. This was identified by first visually inspect then programmatically assess using the info() function.  
  
2) There're 745 dogs that do not have name(“None”). None should be stored are NaN.  
  
3) There're 55 dogs name "a" and 7 dogs name "an". These do not seem to be name. These two quality issues were identified using the value_counts() command on name variable.  
  
4) Timestamp is not python datetime.  
  
5) NaN for doggo,floofer, pupper, puppo is none, not NaN.  
  
6) There are dogs with rating far more than 10 (for example 960 or 1776), and some with rating far smaller than 10 (like 0 or 1).  
  
7) Some data, for example ID=694925794720792577, have an expanded_urls other than twitter. This was identified by visually inspection of some urls of the dataset.  
  
8) Some tweet, for exsample ID=667550882905632768, starts with a "RT", this means that this tweet is a retweet.  
  
9) There are tweets with a denominator other than 10. Demoninator other than ten is suspicious  
  
**Tidiness issues:**  
1) Doggo,floofer, pupper, puppo can be combined to a single variable: dogstage.  
  
2) These data can be combined into a single spreadsheet.  
  
**3. Data Cleaning**  
In this step, data were programmatically cleaned. First, the three dataset were combined using the common column "tweet_id". Next, doggo,floofer, pupper, puppo were combined into a single variable: dogstage. Then, for the variable name and dogstage, "none" were replaced with NaN. Next, timestamp variable were changed to python datetime. Then, entries with several characteristics were deleted: 1) Expanded_urls other than twitter were deleted; 2) Retweets were deleted; 3) Tweets with denominator other than 10 were deleted.  
  
The cleaned data were saved as twitter_archive_master.csv.
