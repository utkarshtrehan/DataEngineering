# DataEngineering
Data Engineering is the foundation for the new world of Big Data. Enroll now to build production-ready data infrastructure, an essential skill for advancing your data career.

[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/built-by-developers.svg)](https://forthebadge.com)  [![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)

---
## Learning 🧠

##### 1. SQL Database | Postgres | Python
##### 2. NoSQL Database | Cassandra | Python
##### 3. Creating Normalizaed Tables | Postgres | Python
##### 4. Creating Denormalized Tables | Postgres | Python
##### 5. Creating Fact and Dimension Tables with Star Schema | Postgres | Python
##### 6. 3NF to Star Schema
##### 7. Creating Redshift Cluster using the AWS python SDK
---
## Projects 🤖

### 1. Data Modeling with Postgres 🐘
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Our role is to create a database schema and ETL pipeline for this analysis. We will be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare our results with their expected results.

In this project, we build an ETL pipeline using Python. To complete the project, we will need to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

#### Prerequisites ⬇️

This project makes the folowing assumptions:

* Python 3 is available
* `pandas` and `psycopg2` are available
* A PosgreSQL database is available on localhost

#### Running the Python Scripts ▶️

At the terminal:

1. ```python create_tables.py```
2. ```python etl.py```

#### Database Schema 🦴

After examining the Log and Song JSON files, I created a Star schema (shown below) that include one Fact table (songplays) and 4 Dimension tables.

This design will offer flexibility with the queries being used for analysis.

#### ETL Process ⏩

##### Song Dataset 🎵

The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

```
{
    "num_songs": 1,
    "artist_id": "ARJIE2Y1187B994AB7",
    "artist_latitude": null,
    "artist_longitude": null,
    "artist_location": "",
    "artist_name": "Line Renaud",
    "song_id": "SOUPIRU12A6D4FA1E1",
    "title": "Der Kleine Dompfaff",
    "duration": 152.92036,
    "year": 0
}
```

This information is parsed to populate the Songs and Artists Dimension tables.

##### Log Dataset 🗃️

The log files in the dataset are partitioned by year and month. For example, here are filepaths to two files in this dataset.

```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```

<img src="images/image34.png" alt="Drawing" style="width: 600px;"/>

This data contains information of which songs Users listened to at a specific time. Information is parsed to provide data for the Songplays Fact table and the Users and Time Dimension tables. The ```songplays.artist_id``` and ```songplays.song_id``` columns are populated by a lookup based on the Song Title, Artist Name and song Duration.

##### Description of Files 

###### 📁Directory: data/log_data 

This directory contains a collection of JSON log files. These files are used to populate our Fact table - Song Plays - and to populate the Dimension tables for Users and Time.

###### 📁Directory: data/song_data 

This directory contains a collection of Song JSON files. These files are used to populate Dimension tables for Songs and Artists.

###### 📁create_tables.py 

This Python script recreates the database and tables used to storethe data.

###### 📁etl.ipynb 

A Python Jupyter Notebook that was used to initially explore the data and test the ETL process.
 
###### 📁etl.py 

This Python script reads in the Log and Song data files, processes and inserts data into the database.

###### 📁sql_queries.py 

A Python script that defines all the SQL statements used by this project.

###### 📁test.ipynb 

A Python Jupyter Notebook that was used to test that data was loaded properly.

---

### 2. Data Modeling with Apache Cassandra 👁️

---

### 3. Project: Data Warehouse

A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, we are tasked with building an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

In this project, you'll apply what you've learned on data warehouses and AWS to build an ETL pipeline for a database hosted on Redshift. To complete the project, we will need to load data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

#### Project Datasets
You'll be working with two datasets that reside in S3. Here are the S3 links for each:

- Song data: `s3://udacity-dend/song_data`
- Log data: `s3://udacity-dend/log_data`  
Log data json path: `s3://udacity-dend/log_json_path.json`

Song Dataset
The first dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
```{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}```

#### Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.

```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```
And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.

<img src="images/image33.png" alt="Drawing" style="width: 600px;"/>

#### Schema for Song Play Analysis
Using the song and event datasets, we created a star schema optimized for queries on song play analysis. This includes the following tables.

#### Fact Table
1. songplays - records in event data associated with song plays i.e. records with page NextSong
    - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location user_agent
#### Dimension Table
2. users - users in the app
    - user_id, first_name, last_name, gender, level
3. songs - songs in music database
    - song_id, title, artist_id, year, duration
4. artists - artists in music database
    - artist_id, name, location, lattitude, longitude
5. time - timestamps of records in songplays broken down into specific units
    - start_time, hour, day, week, month, year, weekday

#### Project Template

The project template includes four files:

- ```create_table.py``` is where you'll create your fact and dimension tables for the star schema in Redshift.
- ```etl.py``` is where you'll load data from S3 into staging tables on Redshift and then process that data into your analytics tables on Redshift.
- ```sql_queries.py``` is where you'll define you SQL statements, which will be imported into the two other files above.
- ```README.md``` is where you'll provide discussion on your process and decisions for this ETL pipeline.

#### Note
The SERIAL command in Postgres is not supported in Redshift. The equivalent in redshift is IDENTITY(0,1), which you can read more on in the Redshift Create Table Docs.

---

