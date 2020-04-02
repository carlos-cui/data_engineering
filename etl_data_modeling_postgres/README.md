# ETL process to ingest data into PostGres DB

## Goal
The goal of the ETL process is to give Sparktify, a startup music streaming company, the ability to analyse data on songs and user activty on their music streaming app.

## Process
In this project I will create a Postgres database with tables desgined to optimize queries on song play analyiss. The project will create a ETL process to create tables in a database (Sparktify) to ingest JSON data from two sources.

The ETL process will create a star schema database. The fact table will be a table called songplays with four dimension tables, users, songs, artists, time.

The star schema will be the best design for this need because it will give analysts a simple design to query song and user activity with few joins. This design also creates a table for our main dimensions and keeps the data to query in one fact table.

### Schema:

![Image description](https://github.com/carlos-cui/data_engineering/blob/master/etl_data_modeling_postgres/db_schema.jpg)

#### Fact Table
- songplays - records in log data associated with song plays i.e. records with page NextSong 
    - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### Dimension Tables
- users - users in the app
    - user_id, first_name, last_name, gender, level
- songs - songs in music database
    - song_id, title, artist_id, year, duration
- artists - artists in music database
    - artist_id, name, location, latitude, longitude
- time - timestamps of records in songplays broken down into specific units 
    - start_time, hour, day, week, month, year, weekday
    
    
## Process
The ETL process involves 3 python(.py) files, 'sql_queries.py', 'create_tables.py', and 'etl.py'.

There are also two notebook (.ipynb) files that were used to create the etl.py file and to test the results. This files aren't necessary for the ETL job.

#### sql.queries.py
This file has the sql queries needed to create the 5 tables and sql queries to insert records into those 5 tables. The file also has a sql query to match the song data with wiht log data.

#### create_tables.py
This file creates our database and runs the sql.queries.py file to create the tables.

#### etl.py
This file reads our two main json files, 'song data' and 'log data', and creates the etl process to ingest data into our 5 tables. This file runs the insert record queries from the sql.queries.py file.

## Conclusion
The end result is a database, 'sparktify', with 5 tables to form a star schema. The end result gives the company the ability to analyze data on songs and user activity.

Note regarding results: all files run successfully. However, the songplays table has mostly blank values in song_id and artist id. The sql query to do a match based on song, album title and duration doesn't seem to give the expected results. This has been noted in the user forums as a common issue.

