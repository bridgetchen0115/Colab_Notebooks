# Big Data Report
## Description of the data
> *When it has been collected? Who did collect it?  What is the source? How large is your data? Do you have any links to the data? How many records does it have? How many features columns)? Structured or Unstructured?* 

The “Trending YouTube Video Statistics” dataset was collected by Kaggle user Mitchell J 6 months ago. The link to the data source is [here](https://www.kaggle.com/datasnaek/youtube-new). The dataset was collected using the YouTube API. It includes a list of the top trending videos of 10 different countries and regions, which is put into separate files. Each CSV file includes 16 columns including video id, trending dates, video titles, channel titles, category ids, publish time, tags, views, likes and dislikes, the number of comments, thumbnail link, whether the comments or ratings are disabled, or video removed, and video description. And in each CSV file, there are up to 200 trending videos pulled from YouTube each day. The dataset in CSV files is structured, however, unstructured in JSON files. Each structured CSV file includes a column named category_id, which is associated with categories stored in the unstructured JSON file. 

## Problem Statement
> *What are you trying to do? What is your aim? What are your research questions?*

1. What’s the list of the trending videos? (Yuki) 

2. Which video remained the most on the most trending-videos list?--3 countries （CA, USA, GB) (Bridget) 

3. What are the lengths of the most trending video titles? (Bridget) 

4. What are the most common words in the most trending video titles? (Qinxin) 

5. Which YouTube channels have the largest number of the most trending videos? (Qinxin)


6. Which video category (e.g. Entertainment, Gaming, Comedy, etc.) has the largest number of the most trending videos?
 
> *The data also includes a categoryid field, which varies between regions. To retrieve the categories for a specific video, find it in the associated JSON. One such file is included for each of the five regions in the dataset.*

7. When were the most trending videos published? 


## Why is this a big data?
> *What is the reason that you did select this data? Why is it a big data?*

This dataset contains information about top trending Youtube videos of 10 different countries. We selected this data set because the dataset about trending youtube videos is very interesting and we can extract a lot of meaningful insights from the dataset. It contains both structured data (CSV files) and unstructured data (JSON files). Also, the data set 


## Method & Results
> *What methods did you use? Are you using any Hadoop tools? What are your findings? Any plot? Graph?*


## Conclusion
> *Conclude your findings and let us know if you have any suggestions regarding the data.* 


## Code Section (Appendix)
### Question 1
```bash
## import csv files into hdfs in terminal
hdfs dfs -put Youtube 
hdfs dfs -chmod 777 Youtube
```
```sql
--list based on views--
select video_id,
max(views) as total_views,
max(likes) as total_likes,
max(comment_count) as total_comments,
comments_disabled,ratings_disabled
from usvideo 
where trending_date is not null
group by video_id,comments_disabled,ratings_disabled
order by total_views desc;
```
![total_views_limit_20](https://raw.githubusercontent.com/aoyingxue/Colab_Notebooks/master/big_data_final_results/total_views_limit_20.png)

```sql
--list based on likes--
select video_id,
max(views) as total_views,
max(likes) as total_likes,
max(comment_count) as total_comments,
comments_disabled,ratings_disabled
from usvideo 
where trending_date is not null
group by video_id,comments_disabled,ratings_disabled
order by total_likes desc;
```
![total_likes_limit_20](https://raw.githubusercontent.com/aoyingxue/Colab_Notebooks/master/big_data_final_results/total_likes_limit_20.png)

```sql
--list based on comments--
select video_id,
max(views) as total_views,
max(likes) as total_likes,
max(comment_count) as total_comments,
comments_disabled,ratings_disabled
from usvideo 
where trending_date is not null
group by video_id,comments_disabled,ratings_disabled
order by total_likes desc;
```
![total_comments_limit_20](https://raw.githubusercontent.com/aoyingxue/Colab_Notebooks/master/big_data_final_results/total_comments_limit_20.png)

```sql
--comments_disabled vs. ratings_disabled--
select distinct video_id,comments_disabled, ratings_disabled
from usvideo
where trending_date is not null;
```

## Questions: 
1. What’s the list of the trending videos? Is there any similarity or difference based on views, based on likes, and based on the number of comments? What’s the reason? (comments_disabled)
    1. How many views do our trending videos have? Do most of them have a large number of views? Is having a large number of views required for a video to become trending?
    2. likes
    3. comments
    4. comments disabled and ratings disabled are correlated

Filter the list, then:
 
2. Which video remained the most on the trending-videos list? (trending-date)

4. What are the lengths of trending video titles? Is this length related to the video becoming trendy? (barplot)

4. What are the most common words in trending video titles?

5. Which YouTube channels have the largest number of trending videos?

6. Which video category (e.g. Entertainment, Gaming, Comedy, etc.) has the largest number of trending videos? (category_id, JSON) Find a relation between the category id and how many videos getting uploaded on that category.

7. When were trending videos published? On which days of the week? at which times of the day?


## Reference: 
https://www.kaggle.com/ammar111/youtube-trending-videos-analysis
https://www.kaggle.com/tripatsu/youtube-trending-videos-data-analysis
