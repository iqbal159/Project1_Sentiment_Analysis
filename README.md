# Project1_Sentiment_Analysis
## (Twitter Sentiment Analysis Project_Data Engineering)

### Overview
Create a Spark Application to perform sentiment analysis on tweets, and populate the sentiment 
polarity in an output file. The sentiment polarity contains either “Positive”, “Negative”, or “Neutral”.

Populate all fields in the output file based on the following format: 
created_at, text, screen_name, source, location, followers_count, friends_count, retweet_count, language, sentiment polarity

### Dataset: blockchain.csv (tweets are in English) 
Fields in the dataset: created_at, text, screen_name, source, location, followers_count, friends_count, retweet_count, language 

## Tutorial<br>

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
label = read_csv("part-00000") 
#Label the column names according to the required output fields, below is the sample 
label.columns = ["created_at", "text", "screen_name", "source", "location", "followers_count", "friends_count", 
"retweet_count", "favourite_count", "language", "sentiment_polarity"] 
label.to_csv("part-00000headers1.csv",index = False) 

Step 12: Ingest the file with header into GIANT
