# Client Project

### Data Dictionary

|File Name|Description|
|---|---|
|[raw_df](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/datasets/raw_df.csv)|Unedited `raw` tweets pulled through Twitterscraper|
|[df.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/datasets/df.csv)|Cleaned tweets, ready for EDA and modeling|
|[tweets_lemmatized.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/tweets_lemmatized.csv)|Lemmatized Tweets|
|[tweets_stemmed.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/tweets_stemmed.csv)|Stemmed Tweets|
|[tweets_tokenized.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/tweets_tokenized.csv)|Tokenized Tweets|
|[df_urgent.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/datasets/df_urgent.csv)|`urgent` classified tweets with assigned coordinates|
|[df_nonrguent.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/datasets/df_nonurgent.csv)|`non_urgent` classified tweets with assigned coordinates|
|[disaster_response_messages_training.csv](https://git.generalassemb.ly/kshupe/Client-Project/blob/master/data/disaster_response_messages_training.csv)|Data the `Word2Vec` classifier model was trained on|

### Twitter: Data Collection and Cleaning

Due to logistical constraints of obtaining Twitter Developer API, the **[Twitterscraper](https://github.com/taspinar/twitterscraper)** web-scraping tool was used to collect tweets. The benefit of this particular tool was the ability to use a customizable `query` for filtering tweets relevant to location and timeline. Due to the importance of **location** for our project, location was particularly difficult aspect to account for. Location of tweet is not a possible output in the query. Instead, location, as an input, is only used to search for tweets by city, area, or geo-coordinates.

Although all tweets have the same limitation on size, tweets can vary in a number of ways, and have a wide range of characters they can contain. In measuring statistically relevant textual information within a given tweet, we removed non-alphabetical characters, removed `url`'s, and stripped away all columns except for `text`. This process was automated using a custom function for further use.

### Creating Coordinates for Mapping

Because of the limitations on acquiring tweet location from either the Twitter API or Twitterscraper tool, we opted to randomly generate geo-coordinates for simulating the mapping of tweet locations (by geo-coordinate location) for our proof of concept.

A random cluster of coordinate positions was created around the coordinates for Paradise, Ca. Any cluster can be created by entering into the function the `number of coordinates to generate`, the `center around which to cluster`, and the `radius of the cluster`. The `coords_dict` dictionary contains several latitude / longitude coordinates wihtin the area of the Camp Fire wildfire, of which can be updated to reflect a clustering in another location.

ArcGIS is a powerful visualization tool that works well with `geopandas`. Once the coordinates were generated and assigned to the dataframes containing the `urgent` and `non_urgent` classified tweets, the respective dataframes were passed into a `GeoDataFrame`. This transformed the randomly generated coordinates into a geopandas `geometry` compatible for layering in ArcGIS.
