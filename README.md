# Project1_Sentiment_Analysis
## Twitter Sentiment Analysis Project_Data Engineering (Fusionex Data Engineer Programme)

### Overview
Create a Spark Application to perform sentiment analysis on tweets, and populate the sentiment 
polarity in an output file. The sentiment polarity contains either “Positive”, “Negative”, or “Neutral”.

Populate all fields in the output file based on the following format: 
created_at, text, screen_name, source, location, followers_count, friends_count, retweet_count, language, sentiment polarity

### Dataset: blockchain.csv (tweets are in English) 
Fields in the dataset: created_at, text, screen_name, source, location, followers_count, friends_count, retweet_count, language 

## Tutorial_1 - Data Engineering<br>

  - Step 1: Move the dataset and spark_SA_assessment.py into ipython directory.  

  - Step 2: Move the dataset in ipython directory to hdfs.              
              
  - Step 3: Launch the spark service
    
  - Step 4: Use spark_SA_assessment.py as a start for Spark application. Define Spark Context in one thread  
             (.setMaster), and named the application (.setAppName)
    
  - Step 6: Prepare the pipeline for sentiment analysis.<br>
      a. Read the "text" column dataset in RDD(Resilient Distributed Dataset) named "RawData" <br>
      b. Identify the delimiter by using split(",").<br>
      c. Identify the length of fields using filter transformation; len() and == sign <br>
      d. Remove all empty lines using filter() transformation; len() index 0 > 1] <br>
      e. All tweets are in English. Do not need to perform translation. <br>
      f. Remove all the single (‘) and double(“)quotes <br>
      g. Use TextBlob package to identify the sentiment polarity by using code sentiment.polarity 

  - Step 7: Use .zip to combine two RDDs. Remove all single and double quotes.
  
  - Step 8: Save the output by using .saveAsTextFile()               

  - Step 9: Launch a new terminal, and run spark_SA_assessment.py 

  - Step 10: Now, little bit of pre-processing is needed on the generated output file (as in step 8), prior ingesting into GIANT 

  - Step 11: Move the generated output file (part-00000) from hdfs (/user/root/) to local drive (/root/ipython/).  

  - Step 11: In Jupyter, launch a Notebook 
             a) Run below code to label header for each field in part-00000 (in local drive) 

from pandas import read_csv 
label = read_csv("part-00000") <br>
#Label the column names according to the required output fields, below is the sample <br>
label.columns = ["created_at", "text", "screen_name", "source", "location", "followers_count", "friends_count", 
"retweet_count", "favourite_count", "language", "sentiment_polarity"] <br>
label.to_csv("part-00000headers1.csv",index = False) 

Step 12: Ingest the file with header into GIANT

## Tutorial_2 - Data Visualization using GIANT Dashboard<br>

  - Step 1: Edit the source and convert followers_count, friends_count to numeric data type
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/8351f8cd-a387-41d0-8312-802e124d6799)

  - Step 2:  Perform a “split column” on sentiment to remove the last bracket
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/6378b323-e7a3-41b6-b404-89276a84e163)

 - Step 3:  Hide the original sentiment and the bracket columns, then Save
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/cac6bfd7-9265-4416-a354-fad99bf207d2)

 - Step 4: Use Giant Smart Query to perform analysis and creating Dashboard based on the dataset
   
    1) Sentiment Polarity vs Followers Count - Positve and Neutral Tweets seemed to have more followers count than someone who has Negative tweets.
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/875b328d-1219-4ef5-8ba8-f3a81e326909)

    2) Sentiment Polarity by Locations - Most of the tweeted worldwide are from Positive and Neutral sentiment
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/2f9ed165-a0dc-4488-a790-ee95b142b195)

    3) Sentiment Polarity vs Retweeted Count - Others twitter users moslty retweeted on Positive and Neutral sentiment
![image](https://github.com/iqbal159/Project1_Sentiment_Analysis/assets/130142247/a901329f-1eac-419e-b95f-be80d1fba9d4)







