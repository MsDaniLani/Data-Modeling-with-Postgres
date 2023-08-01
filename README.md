
# ***Data Modeling with Postgres - Sparkify***

This project is part of the Udacity Data Analyst Nanodegree program and involves designing a database schema and ETL pipeline for a music streaming startup called Sparkify.

## Table of Contents
- [Purpose and Analytical Goals](#purpose-and-analytical-goals)
- [Project Overview](#project-overview)
  - [Introduction](#introduction)
  - [Project Description](#project-description)
- [Project Datasets](#project-datasets)
  - [Song Dataset](#song-dataset)
  - [Database Schema](#database-schema)
  - [Schema for Song Play Analysis](#schema-for-song-play-analysis)
    - [Fact Table](#fact-table)
    - [Dimension Tables](#dimension-tables)
- [ETL Pipeline](#etl-pipeline)
- [Project Steps](#project-steps)
  - [Create Tables](#create-tables)
  - [Build ETL Processes](#build-etl-processes)
  - [Build ETL Pipeline](#build-etl-pipeline)
  - [Running the ETL Pipeline](#running-the-etl-pipeline)
- [Files](#files)
- [Software and Tools](#software-and-tools)
- [Queries](#queries)
- [Conclusion](#conclusion)


## Purpose and Analytical Goals

The purpose of the Sparkify database is to provide insight into user behavior on the startup music streaming platform. The database schema consists of a fact table and several dimension tables to make querying and summarizing data easy. The ETL process extracts and transforms JSON data into a format that can be loaded into the database using Python and SQL. The goal of this project is to create a database schema and ETL pipeline that will enable Sparkify to analyze user behavior and improve the overall user experience on their music streaming platform.

## Project Overview

### Introduction

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

### Project Description

In this project, you'll apply what you've learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, you will need todefine fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

## Project Datasets

### Song Dataset

The first dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID.

### Database Schema

The database schema is designed as a star schema with a fact table (`songplays`) and several dimension tables (`users`, `songs`, `artists`, and `time`). The fact table contains information about each song play, while the dimension tables contain information about the users, songs, artists, and time periods associated with each song play. This schema allows for easy querying and aggregation of data, as well as quick access to the most relevant information for analysis.

### Schema for Song Play Analysis

Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

#### Fact Table
- **songplays** - records in log data associated with song plays i.e. records with page `NextSong`
  - _songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent_

#### Dimension Tables

- **users** - users of the streaming platform
  - _user_id, first_name, last_name, gender, level_
- **songs** - songs in music database
  - _song_id, title, artist_id, year, duration_
- **artists** - artists in music database
  - _artist_id, name, location, latitude, longitude_
- **time** - timestamps of records in **songplays** broken down into specific units
  - _start_time, hour, day, week, month, year, weekday_

## ETL Pipeline

The ETL pipeline consists of two main functions: `process_song_file` and `process_log_file`. The process_song_file` function extracts data on songs and artists from the JSON files and inserts it into the `songs` and `artists` tables, while the `process_log_file` function extracts data on user activity and inserts it into the `songplays`,`users`, and `time` tables. The ETL pipeline is designed to extract data from JSON files, transform it into the appropriate format, and load it into the database using SQL queries. The pipeline is designed to be scalable and can handle large amounts of data.

## Project Steps

Below are steps you can follow to complete the project:

#### Create Tables

1. Write `CREATE` statements in `sql_queries.py` to create each table.
2. Write `DROP` statementsin `sql_queries.py` to drop each table if it exists.
3. Run `create_tables.py` to create the database and tables.

#### Build ETL Processes

1. Implement `process_song_file` function in `etl.py` to process song files.
2. Implement `process_log_file` function in `etl.py` to process log files.
3. Test `process_song_file` and `process_log_file` functions by running `etl.ipynb`.

#### Build ETL Pipeline

1. Implement `main` function in `etl.py` to perform ETL pipeline.
2. Run `etl.py` to extract data from JSON files, transform it, and load it into the database.

#### Document Process

Do the following steps in your  `README.md`  file.

1.  Discuss the purpose of this database in the context of the startup, Sparkify, and their analytical goals.
2.  State and justify your database schema design and ETL pipeline.
3.  [Optional] Provide example queries and results for song play analysis.

==**NOTE:**  You will not be able to run  `test.ipynb`,  `etl.ipynb`, or  `etl.py`  until you have run  `create_tables.py`  at least once to create the  `sparkifydb`  database, which these other files connect to.==

## Running the ETL Pipeline

To run the ETL pipeline, follow these steps:

1. Run `create_tables.py` to create the database and tables.
2. Run `etl.py` to extract data from JSON files, transform it, and load it into the database.

## Files

The project includes the following files:
| File Name | Description |
| :----------| :----------|
| `create_tables.py` | This script creates the database tables. It drops any existing tables and recreates them fresh. |
| `etl.ipynb` | This Jupyter notebook is used for prototyping the ETL pipeline. It allows testing extracting data from the  JSON files  and transforming it before loading into the database. |
| `test.ipynb` | This Jupyter notebook is used for testing the ETL pipeline. It connects to the database and runs queries to compare the results to expected values. |
| `etl.py` | This script contains the ETL pipeline that extracts data from the JSON files, transforms it, and loads it into the database. It contains the main functions to process the song and log JSON files. |
| `sql_queries.py`| This file contains the  SQL queries  used to create the  database tables  and insert data into them. The queries are imported and used in the  ETL  scripts. |
| `README.md`| This file provides an overview of the project,   instructions on how to run the ETL pipeline, and descriptions of the other files. |
| The song and log JSON files | These contain the  source data  that the ETL pipeline extracts from and loads into the database tables. |

## Software and Tools
In this project, the following software and tools were used:
- Python 3.6
- PyCharm 
- PostgreSQL 15.3
- Jupyter Notebook
- PGAdmin 4
- Anaconda
- `psycopg2` - PostgreSQL database adapter for Python
- `pandas` - data manipulation library
- `os` - operating system interface
- `glob` - filename pattern matching
- `json` - read and write JSON data

The project was completed on a local machine with the above software and libraries installed. However, the project can also be completed Udacity workspace, which has all the necessary software and tools pre-installed.

## Queries
1.  Find the top 10 users who have the most song plays:
>SELECT u.first_name || ' ' || u.last_name AS user_name,
    count(*) AS plays
    FROM 
    songplays sp
JOIN users u ON sp.user_id = u.user_id
GROUP BY 1
ORDER BY plays DESC
LIMIT 
    10;
![top 10 users.png](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/top%2010%20users.png)

2. View total song plays by day:
>SELECT time.start_time::date AS date, COUNT(songplays.songplay_id) AS num_songplays
FROM songplays
JOIN time ON songplays.start_time = time.start_time
GROUP BY date
ORDER BY date ASC;
![graph_visualiser-1685553656475.png](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/graph_visualiser-1685553656475.png)

3. Select the first 5 rows from the artists table. 
>SELECT * FROM artists LIMIT 5
![select-all-from-artists-limit-5.png](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/select-all-from-artists-limit-5.png)

4. Select the first 5 rows from the songs table. 
>SELECT * FROM songs LIMIT 5
![select-all-from-songs-limit-5.png](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/select-all-from-songs-limit-5.png)

5. Select the first 5 rows from the time table. 
>SELECT * FROM time LIMIT 5
![select-all-from-time-limit-5.png](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/select-all-from-time-limit-5.png)


6. Select the first 5 rows from the user table.
>SELECT * FROM users LIMIT 5
![Select-all-from-users-limit-5](https://github.com/MsDaniLani/Data-Modeling-with-Postgres/blob/main/select-all-from-users-limit-5.png)

## Conclusion

In this project, I have designed a database schema and implemented an ETL pipeline for a music streaming startup called Sparkify. I have created a star schema with a fact table and dimension tables, and used Python and SQL to extract, transform, and load data from JSON files into the database. The resulting database and ETL pipeline enable Sparkify to analyze user behavior and improve the overall user experience on their music streaming platform.
