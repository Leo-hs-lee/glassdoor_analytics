# Glassdoor Job Board Scraping & Analysis

## 🎞️ About the Project
The job market in data-related fields is rapidly evolving, with high demand for skilled professionals in various industries. 

This project aims to scrape job listings for Data Analyst, Data Scientist, and Data Engineer positions from Glassdoor in five major US cities: Seattle, Austin, Los Angeles, New York, and San Francisco. The collected data will be used for further analysis, visualization, and predicting trends in the job market.

### Tools Used
* [Python 3.8](https://www.python.org/downloads/release/python-3814/)
* [Sellenium](https://developers.google.com/youtube/v3)

## Problem Statment & 
Public Job data doesn't reflect current job market situation and our conditions.

## 📈 Result

> After collecting the data, you can analyze the job market trends, salary expectations, and skill requirements for each role using the provided Jupyter notebook:
<img src="https://user-images.githubusercontent.com/113565868/190591500-83b57aca-71f2-40c4-b94b-58e5b8d510e2.PNG" width="800" height="500" />
<img src="https://user-images.githubusercontent.com/113565868/190595693-6748471e-9d9e-4840-9f5e-f8ab056f0f4f.PNG" width="800" height="500" />



> Also, we can depict the viewership trend of high-performing channels.
<img src="https://user-images.githubusercontent.com/113565868/190593869-4e669cfa-c239-4f51-b319-ae61ef142e9a.PNG" width="800" height="300" />



## 🛠 Project Structure
![youtube_analysis4](https://user-images.githubusercontent.com/113565868/190601715-39a190fb-5c40-4f52-b2f5-faa5a9d72a89.PNG)
1. Input the list of *Youtube channel names* and *channel IDs* in the database(AWS RDS-MySQL)
2. Request corresponding youtube channel statistics from Youtube Data API v3
3. Store the Youtube channel information in the database automatically, once a day, using AWS Lambda serverless framework
4. data manipulation and visualization(Jupiter Notebook)


### Prerequisites
```
pip install google-api-python-client
pip install pandas
pip install pymysql
pip install sqlalchemy
pip install boto3
```
MUST INPUT YOUR OWN Youtube API key & Database credentials
```
api_key = 'Your API Key'
hostname="Host Address"
dbname="Database"
uname="User Name"
pwd="Your Password"
```


## 📊 Data 

* Job title
* Company name
* Location
* Salary range
* Job description
* Company rating
The data is saved in a CSV file in the data folder.

### Input data 
| Channel Name    | Channel ID               |
|-----------------|--------------------------|
| Example Channel | UCK9M3uZMNjbqCI3O80-eF1k |
| ...             | ...                      |

**Channel Name**: Name of the Youtube channel\
**Channel ID**: ID of the Youtube channel can be found ['here'](https://support.google.com/youtube/answer/3250431?hl=en)

### Output data
| channel_name    | published_date       | subscribers | views     | total_videos | playlist_id              | retrieved_date |
|-----------------|----------------------|-------------|-----------|--------------|--------------------------|----------------|
| Example Channel | 2015-12-27T21:31:03Z | 1690000     | 680087428 | 185          | UUJCx8aQrdx_ueXPmxTD2odQ | 2022/09/15     |
| ...             | ...                  | ...         | ...       | ...          | ...                      | ...            |

**published_date**: The date channel was published\
**subscribers**: Total subscriber count of the channel (Count in 1000)\
**views**: Total view count of public viddeos in the channel (Decreases if video is unlisted)\
**total_video**: Total number of public videos in the channel\
**playlist_id**: Channel's playlist ID for further analysis\
**retrieved_date**: The the data was retrieved

### Data Manipulation
| channel_name    | sub_diff | view_diff | upload_diff | viewperupload | sub_gain| veiw_gain | videoloads |
|-----------------|----------|-----------|-------------|---------------|---------|-----------|------------|
| Example Channel | 2000     | 310902    | 4           | 777025.5      | 1000    | 42407     | 1          |
| ...             | ...      | ...       | ...         | ...           | ...     | ...       | ...        |

**sub_diff**: How much subscriber has increased overtime (Count in 1000)\
**view_diff**: How much view has increased overtime \
**upload_diff**: How many video was uploaded (or unlisted) overtime\
**viewperupload**: Mean of view count affected per uploads, overtime: (*view_diff/upload_diff*)\
**sub_gain**: Subscriber gain to the day before\
**view_gain**: View gain to the day before

### Evaluation

**What we want to know:**
We want to know how much one video worth.

**How to evaluate:**
We need to evaluate the channels based on their expected view counts per one video upload.

**Evaluation index:**
view_game/upload_diff 

**Parameter Estimator:**
Ordinary least squares

## 🚀 What's Next?

* Conduct deeper channel analysis of top 3% youtube channels to identify which theme/concept of video is best performing
* Run the system with +1000 samples to develop more precise prediction model for well-performing youtube channels.



