# DataWrangling_Project

## WeRateDogs Wrangling_Project 

### WRANGLING EFFORTS


Data Wrangling process used in my analysis includes the

Gathering
Assess
Clean
Gathering
The first step as mentioned above is the GATHERING stage where i got to assemble all the data i needed for this project, First of all the The WeRateDogs Twitter archive was gathered by Downloading manually. Once it was downloaded, i uploaded it and read the data into a pandas DataFrame in the wrangle_act jupyter notebook.

Secondly,The tweet image predictions file (image_predictions.tsv) i got was also provided via a link on Udacity's classroom and was downloaded programmatically using the Requests library and the URL below: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv.

I had to access the Weratedogs twitter page with twitter Api(tweepy) to gather other information like retweet count and favorite count missing in the original Weratedogs twitter archive downloaded manually initially, after Twitter granted me elevated access.I read the Json objects from the tweet-json.txt file into pandas and all the json objects were pushed in a list of dictionaries which was appended and that list converted to a Dataframe.

At this time, i had my 3 datasets gathered and ready.

Assess
This was where i made an effort to be somewhat like an investigator, searching for where the data had issues and what exact kind of issues it has.I had to read the image_predictions.tsv file here so i can assess the datasets as well. pandas function like .tail(), .describe(), .value_counts(), .info() helped me find out various issues with the gathered data i had .

I broke down the assessed problems gotten from Assessing the datasets into Quality issues and Tidyness issues which are listed below

Quality
tweet_id column name not consistent for the other tables
all (retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp columns) rows have values in the dataframe but we dont want retweet info based on the fact that most users retweet their own tweets.
name column in the we_rate_dogs table have some unusual names as a,not,one,his etc,and this non-dog names all comes in small letters. also name as column title not descriptive enough.
Erroneous datatypes (timestamp, retweeted_status_timestamp columns)
retweeted_status_id, retweeted_status_user_id, in_reply_to_status_id,in_reply_to_user_id,retweeted_status_timestamp columns are not needed in this analysis for data integrity, esp with Validity data conerns with float datatype
source column has some irrelevant words attached to the main source type
header/column names for p1,p1_conf,p1_dog,p2,p2_conf,p2_dog,p3,p3_conf,p3_dog are not descriptive enough
p1,p2,p3 columns begin with small letters sometimes, capital letters other times
Tidiness
df table and image_predictions table should be part of we_rate_dogs table
Four columns containing one variable-dog stages
Clean
In this section, First i created copy of all dataframes to enable me access the main dataframe/dataset should incase i want to in the future.All cleaning method or processes were carried out on this copied dataframes which were

we_rate_dogs_clean
image_predictions_clean
df_clean
and all were made to pass through the "Define":"Code":"Test" formula for Cleaning data.

Cleaning steps i took for the assessed problems were that I

Renamed the tweet_id column to tweet_ID column with pandas rename method so we can have a common column for easy joining of tables later while cleaning
Merged the df_table and the image_predictions table to the we_rate_dogs table using their common column tweet_ID
Melted the doggo floofer pupper and puppo columns to dog stages.Drop the intermediate dogs column and also resulting duplicate entries as a result of the melt method.
selected the rows in these columns (retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp columns) that have null values,we only need purely dog ratings and null values for these columns signify no retweets from original user tweets.
Renamed the name column to a descriptive column name and convert all unusual names like 'a','not','one','his' etc to nan(np.nan) values since those with lower case cant be a name of a dog and we cant input/fill any random name.
Converted timestamp, retweeted_status_timestamp columns to datetime datatype.
Dropped these columns(retweeted_status_id,retweeted_status_user_id,in_reply_to_status_id,in_reply_to_user_id,retweeted_status_timestamp) and also normal schema doesnt allow Unique IDs to be a float datatype.
Got the exact description of the source by creating a function that will remove the unnneccessary details in the source * column and return just the exact source type and then using .apply method to apply the function into the main dataframe
Rename the p1,p1_conf,p1_dog,p2,p2_conf,p2_dog,p3,p3_conf,p3_dog columns to a descriptive column name using .rename method in pandas
capitalize all first letters of the p1,p2,p3 columns to avoid inconsistency in those columns that might affect our analysis later on. The .capitalize method in pandas was useful for this.
 
 Insights
Labrador retriever is one of the most commonly occurring dog breed based on this Twitter data followed closely by Golden retriever. As seen also in the mean of 66% on the First prediction,down to 14% on the Second prediction for the Labrador retriever dog breed compared to the mean of 72% on the First prediction,down to 11% on the Second prediction for the Golden_retriever.So close!!!

The favorite count, retweet count and tweet_IDs gave us more insight that there are tweets that have more favorite counts and retweet counts than other tweet_IDs regardless if the dog stage posted with the various tweets are the same.like in our vizzes of favorite column and retweet counts compared with tweet_IDs, observe that the highest liked(favorite) dog stage,puppo had a different tweet_ID and was not the highest_retweeted dog_stage; instead it was the tweet_ID 744234799360020481 with dog stage,doggo that had the most retweet count aand also the second highest favorite count.

As mentioned earlier,Tweet source provides information about the Tweet and its author.Hence why we needed to know where most tweets on the weratedogs twitter archive come from. It helps understand how a tweet was posted.Twitter for iphone is really a source where most authors posted from,liked and retweeted from. Safe to say our Users are majorly IPHONE users.
