# Project 1: Query Project

- In the Query Project, you will get practice with SQL while learning about
  Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven
  questions using public datasets housed in GCP. To give you experience with
  different ways to use those datasets, you will use the web UI (BiqQuery) and
  the command-line tools, and work with them in Jupyter Notebooks.

#### Problem Statement

- You're a data scientist at Lyft Bay Wheels (https://www.lyft.com/bikes/bay-wheels), formerly known as Ford GoBike, the
  company running Bay Area Bikeshare. You are trying to increase ridership, and
  you want to offer deals through the mobile app to do so. 
  
- What deals do you offer though? Currently, your company has several options which can change over time.  Please visit the website to see the current offers and other marketing information. Frequent offers include: 
  * Single Ride 
  * Monthly Membership
  * Annual Membership
  * Bike Share for All
  * Access Pass
  * Corporate Membership
  * etc.

- Through this project, you will answer these questions: 

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- Please note that there are no exact answers to the above questions, just like in the proverbial real world.  This is not a simple exercise where each question above will have a simple SQL query. It is an exercise in analytics over inexact and dirty data. 

- You won't find a column in a table labeled "commuter trip".  You will find you need to do quite a bit of data exploration using SQL queries to determine your own definition of a communter trip.  In data exploration process, you will find a lot of dirty data, that you will need to either clean or filter out. You will then write SQL queries to find the communter trips.

- Likewise to make your recommendations, you will need to do data exploration, cleaning or filtering dirty data, etc. to come up with the final queries that will give you the supporting data for your recommendations. You can make any recommendations regarding the offers, including, but not limited to: 
  * market offers differently to generate more revenue 
  * remove offers that are not working 
  * modify exising offers to generate more revenue
  * create new offers for hidden business opportunities you have found
  * etc. 

#### All Work MUST be done in the Google Cloud Platform (GCP) / The Majority of Work MUST be done using BigQuery SQL / Usage of Temporary Tables, Views, Pandas, Data Visualizations

A couple of the goals of w205 are for students to learn how to work in a cloud environment (such as GCP) and how to use SQL against a big data data platform (such as Google BigQuery).  In keeping with these goals, please do all of your work in GCP, and the majority of your analytics work using BigQuery SQL queries.

You can make intermediate temporary tables or views in your own dataset in BigQuery as you like.  Actually, this is a great way to work!  These make data exploration much easier.  It's much easier when you have made temporary tables or views with only clean data, filtered rows, filtered columns, new columns, summary data, etc.  If you use intermediate temporary tables or views, you should include the SQL used to create these, along with a brief note mentioning that you used the temporary table or view.

In the final Jupyter Notebook, the results of your BigQuery SQL will be read into Pandas, where you will use the skills you learned in the Python class to print formatted Pandas tables, simple data visualizations using Seaborn / Matplotlib, etc.  You can use Pandas for simple transformations, but please remember the bulk of work should be done using Google BigQuery SQL.

#### GitHub Procedures

In your Python class you used GitHub, with a single repo for all assignments, where you committed without doing a pull request.  In this class, we will try to mimic the real world more closely, so our procedures will be enhanced. 

Each project, including this one, will have it's own repo.

Important:  In w205, please never merge your assignment branch to the master branch. 

Using the git command line: clone down the repo, leave the master branch untouched, create an assignment branch, and move to that branch:
- Open a linux command line to your virtual machine and be sure you are logged in as jupyter.
- Create a ~/w205 directory if it does not already exist `mkdir ~/w205`
- Change directory into the ~/w205 directory `cd ~/w205`
- Clone down your repo `git clone <https url for your repo>`
- Change directory into the repo `cd <repo name>`
- Create an assignment branch `git branch assignment`
- Checkout the assignment branch `git checkout assignment`

The previous steps only need to be done once.  Once you your clone is on the assignment branch it will remain on that branch unless you checkout another branch.

The project workflow follows this pattern, which may be repeated as many times as needed.  In fact it's best to do this frequently as it saves your work into GitHub in case your virtual machine becomes corrupt:
- Make changes to existing files as needed.
- Add new files as needed
- Stage modified files `git add <filename>`
- Commit staged files `git commit -m "<meaningful comment about your changes>"`
- Push the commit on your assignment branch from your clone to GitHub `git push origin assignment`

Once you are done, go to the GitHub web interface and create a pull request comparing the assignment branch to the master branch.  Add your instructor, and only your instructor, as the reviewer.  The date and time stamp of the pull request is considered the submission time for late penalties. 

If you decide to make more changes after you have created a pull request, you can simply close the pull request (without merge!), make more changes, stage, commit, push, and create a final pull request when you are done.  Note that the last data and time stamp of the last pull request will be considered the submission time for late penalties.

---

## Parts 1, 2, 3

We have broken down this project into 3 parts, about 1 week's work each to help you stay on track.

**You will only turn in the project once  at the end of part 3!**

- In Part 1, we will query using the Google BigQuery GUI interface in the cloud.

- In Part 2, we will query using the Linux command line from our virtual machine in the cloud.

- In Part 3, we will query from a Jupyter Notebook in our virtual machine in the cloud, save the results into Pandas, and present a report enhanced by Pandas output tables and simple data visualizations using Seaborn / Matplotlib.

---

## Part 1 - Querying Data with BigQuery

### SQL Tutorial

Please go through this SQL tutorial to help you learn the basics of SQL to help you complete this project.

SQL tutorial: https://www.w3schools.com/sql/default.asp

### Google Cloud Helpful Links

Read: https://cloud.google.com/docs/overview/

BigQuery: https://cloud.google.com/bigquery/

Public Datasets: Bring up your Google BigQuery console, open the menu for the public datasets, and navigate to the the dataset san_francisco.

- The Bay Bike Share has two datasets: a static one and a dynamic one.  The static one covers an historic period of about 3 years.  The dynamic one updates every 10 minutes or so.  THE STATIC ONE IS THE ONE WE WILL USE IN CLASS AND IN THE PROJECT. The reason is that is much easier to learn SQL against a static target instead of a moving target.

- (USE THESE TABLES!) The static tables we will be using in this class are in the dataset **san_francisco** :

  * bikeshare_stations

  * bikeshare_status

  * bikeshare_trips

- The dynamic tables are found in the dataset **san_francisco_bikeshare**

### Some initial queries

Paste your SQL query and answer the question in a sentence.  Be sure you properly format your queries and results using markdown. 

- What's the size of this dataset? (i.e., how many trips)

`983648`

```sql
#standardSQL
SELECT count(*) FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```

- What is the earliest start date and time and latest end date and time for a trip?

`2013-08-29 09:08:00 UTC` 

`2016-08-31 23:48:00 UTC`

```sql
#standardSQL
SELECT min(start_date) 
FROM `bigquery-public-data.san_francisco.bikeshare_trips`

#standardSQL
SELECT max(end_date) 
FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```

- How many bikes are there?

`700`
``` sql
#standardSQL
SELECT count(distinct bike_number)
FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```



### Questions of your own
- Make up 3 questions and answer them using the Bay Area Bike Share Trips Data.  These questions MUST be different than any of the questions and queries you ran above.

- Question 1: Find out the longest rental time duration (in days) and maximum distance between rental stations (in miles) (Note: the maximum distance trip may not be the same as the maximum time duration trip)
  * Answer: 
  
      `max_distance_traveled	`  `42.42`
      `max_day_rented_duration	`  `199.89`
  
   
  
    For this problem, we first make a temporary/custom view using `bigquery-public-data.san_francisco.bikeshare_trips` and `bigquery-public-data.san_francisco.bikeshare_stations` tables and save the result as a view named: `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view` (we will utilize this view to extract further data in the subsequent sections)
  
  * SQL query:

    ``` sql
    #standardSQL
        select 
            a.trip_id, 
            round(a.duration_sec, 2) as duration_sec, 
          round(a.duration_sec/60, 3) as duration_min, 
          round(a.duration_sec/(60*60), 3) as duration_hour, 
          round(a.duration_sec/(60*60*24), 2) as duration_day, 
            a.start_date, 
            a.start_station_name, 
            a.start_station_id, 
            a.end_date, 
            a.end_station_name, 
            a.end_station_id, 
            abs(a.start_station_id - a.end_station_id)
            a.zip_code, 
            a.subscriber_type,
            EXTRACT(DAYOFWEEK FROM a.start_date) AS dow_int,
            CASE EXTRACT(DAYOFWEEK FROM a.start_date)
                   WHEN 1 THEN "Sunday"
                   WHEN 2 THEN "Monday"
                   WHEN 3 THEN "Tuesday"
                   WHEN 4 THEN "Wednesday"
                   WHEN 5 THEN "Thursday"
                   WHEN 6 THEN "Friday"
                   WHEN 7 THEN "Saturday"
                   END AS dow_str,
                   CASE 
                   WHEN EXTRACT(DAYOFWEEK FROM a.start_date) IN (1, 7) THEN "Weekend"
                   ELSE "Weekday"
                   END AS dow_weekday,
                   EXTRACT(HOUR FROM a.start_date) AS start_hour,
                   CASE 
                   WHEN EXTRACT(HOUR FROM a.start_date) <= 5  OR EXTRACT(HOUR FROM a.start_date) >= 23 THEN "Nightime"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 6 and EXTRACT(HOUR FROM a.start_date) <= 8 THEN "Morning"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 9 and EXTRACT(HOUR FROM a.start_date) <= 10 THEN "Mid Morning"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 11 and EXTRACT(HOUR FROM a.start_date) <= 13 THEN "Mid Day"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 14 and EXTRACT(HOUR FROM a.start_date) <= 16 THEN "Early Afternoon"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 17 and EXTRACT(HOUR FROM a.start_date) <= 19 THEN "Afternoon"
                   WHEN EXTRACT(HOUR FROM a.start_date) >= 20 and EXTRACT(HOUR FROM a.start_date) <= 22 THEN "Evening"
                   END AS start_hour_str,
            b.latitude as start_station_lat, 
            b.longitude as start_station_long , 
            b.dockcount as start_station_dockcount, 
            b.landmark as start_station_landmark, 
            b.installation_date as start_station_install_date, 
            c.latitude as end_station_lat, 
            c.longitude as end_station_long, 
            ROUND(ST_Distance(ST_GeogPoint(b.longitude, b.latitude), ST_GeogPoint(c.longitude, c.latitude)) * 0.00062137, 2) as distance_between_stations

        FROM 
            `bigquery-public-data.san_francisco.bikeshare_trips` a, 
            `bigquery-public-data.san_francisco.bikeshare_stations` b, 
            `bigquery-public-data.san_francisco.bikeshare_stations` c
        where 
            a.start_station_id = b.station_id and 
            a.end_station_id = c.station_id
        ORDER BY 
            distance_between_stations desc, duration_sec desc
    ```

    Once done, we now use the following query to extract the results: 

    ```sql
    #standardSQL
    select 
      max(distance_between_stations) as max_distance_traveled,  
      max(duration_day) max_day_rented_duration
    from `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`
    ```

- Question 2: How many distinct bike stations are there in the San Francisco bikeshare?
  * Answer: `74`
  * SQL query:
    ```sql
    #standardSQL
    SELECT count(distinct station_id) FROM `bigquery-public-data.san_francisco.bikeshare_stations`  
    ```
  
  
- Question 3: After the year 2000, show the top-5 stations (along with their zipcodes) that originated the most bike trips (i.e busiest top-5 biketrip originating stations by zip code after the year 2000)?
  * Answer: 
    `num_trips    start_station_id     start_station_name                              zip_code`
    
    `13521         73                  Grant Avenue at Columbus Avenue                 94133`
    
    `11220         61                  2nd at Townsend                                 94107`
    
    `9969          54                  Embarcadero at Bryant                           94105`
    
    `9876          69                  San Francisco Caltrain 2 (330 Townsend)         94107`
    
    `9789          65                  Townsend at 7th                                 94107`

    ``` sql
    #standardSQL
    SELECT count(*) as num_trips, start_station_id, start_station_name, zip_code
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE EXTRACT(YEAR from start_date) > 2000
    group by start_station_id, start_station_name, zip_code
    order by 1 desc
    limit 5
    ```


### Bonus activity queries (optional - not graded - just this section is optional, all other sections are required)

The bike share dynamic dataset offers multiple tables that can be joined to learn more interesting facts about the bike share business across all regions. These advanced queries are designed to challenge you to explore the other tables, using only the available metadata to create views that give you a broader understanding of the overall volumes across the regions(each region has multiple stations)

We can create a temporary table or view against the dynamic dataset to join to our static dataset.

Here is some SQL to pull the region_id and station_id from the dynamic dataset.  You can save the results of this query to a temporary table or view.  You can then join the static tables to this table or view to find the region:
```sql
#standardSQL
select distinct region_id, station_id
from `bigquery-public-data.san_francisco_bikeshare.bikeshare_station_info`
```

- Top 5 popular station pairs in each region

- Top 3 most popular regions(stations belong within 1 region)

- Total trips for each short station name in each region

- What are the top 10 used bikes in each of the top 3 region. these bikes could be in need of more frequent maintenance.

---

## Part 2 - Querying data from the BigQuery CLI 

- Use BQ from the Linux command line:

  * General query structure

    ```
    bq query --use_legacy_sql=false '
        SELECT count(*)
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
    ```

### Queries

1. Rerun the first 3 queries from Part 1 using bq command line tool (Paste your bq
   queries and results here, using properly formatted markdown):

  * What's the size of this dataset? (i.e., how many trips)
    ```sql
    #standardSQL
      $ bq query --use_legacy_sql=false "SELECT count(*) FROM \`bigquery-public-data.
        san_francisco.bikeshare_trips\`"
        Waiting on bqjob_r13dc1b57a7ebd6e_000001702c6fbeae_1 ... (0s) Current status: DONE   
        +--------+
        |  f0_   |
        +--------+
        | 983648 |
        +--------+
    ```
  

  * What is the earliest start time and latest end time for a trip?

    ```sql
    #standardSQL
    $ bq query --use_legacy_sql=false "SELECT min(start_date) FROM \`bigquery-publi
    c-data.san_francisco.bikeshare_trips\`"
    Waiting on bqjob_r5e0072daae2940ed_000001702ecee094_1 ... (0s) Current status: DONE   
    +---------------------+
    |         f0_         |
    +---------------------+
    | 2013-08-29 09:08:00 |
    +---------------------+
    
    $ bq query --use_legacy_sql=false "SELECT max(end_date) FROM \`bigquery-public-
    data.san_francisco.bikeshare_trips\`"
    Waiting on bqjob_r5303dfc623e3744e_000001702ecdaccf_1 ... (0s) Current status: DONE   
    +---------------------+
    |         f0_         |
    +---------------------+
    | 2016-08-31 23:48:00 |
    +---------------------+
    ```

  * How many bikes are there?
    ```sql
    #standardSQL
    $ bq query --use_legacy_sql=false "SELECT count(distinct bike_number) FROM \`bigquery-public-data.san_francisco.bikeshare_trips\`"
    Waiting on bqjob_r4dc6923437c9c561_000001702ed3a799_1 ... (0s) Current status: DONE   
    +-----+
    | f0_ |
    +-----+
    | 700 |
    +-----+
    ```

2. New Query (Run using bq and paste your SQL query and answer the question in a sentence, using properly formatted markdown):

  * How many trips are in the morning vs in the afternoon?
    ```sql
    #standardSQL
     select
     CASE 
         WHEN EXTRACT(HOUR FROM start_date) >= 6 and EXTRACT(HOUR FROM start_date) <= 10 THEN "Morning"
         WHEN EXTRACT(HOUR FROM start_date) >= 14 and EXTRACT(HOUR FROM start_date) <= 19 THEN "Afternoon"
         END AS start_hour_str,
     count(*)
     from `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`
     group by start_hour_str
     having start_hour_str in ('Morning', 'Afternoon')
    ```

    `Row	start_hour_str	f0_	`
    
    `1	    Afternoon       426175`
    
    `2	    Morning         359414`



### Project Questions
Identify the main questions you'll need to answer to make recommendations (list
below, add as many questions as you need).

- Question 1: Rank the busiest days of the week by total percentage of use.   

- Question 2: Rank the months of year by total percentage of use.

- Question 3: Rank trips in buckets of trip times (e.g. trip less than 5 minutes, greater than 5 minutes and less than 10 minutes). Identify which trips are most frequent as percentage of total.

- Question 4: Rank trips in buckets of trip durations (e.g. trip less than 2 miles long, greater than 5 miles and less than 10 miles). Identify which trips are most frequent as percentage of total.

- Question 5: What percentage of trips started and ended in the same stations?

- Question 6: What are the 5 most frequently used stations in the mornings? 

- Question 7: What are the 5 most frequently used stations in the evenings? 

- Question 8: Rank top-10 busiest rush-hour times by weekday as percentage of total trips. 

- Question 9: Break down Bike usage by customer type (ratio of total trips by annual subscribers and daily customers)

Identify bike availability at stations during rush hour commute (i.e. calculate the station utilization during rush hour times in mornings and evenings)


- ...

- Question n: 

### Answers

Answer at least 4 of the questions you identified above You can use either
BigQuery or the bq command line tool.  Paste your questions, queries and
answers below.

- Question 1: Rank the busiest days of the week by total percentage of use.   
  * Answer:
    ```sql
    #standardSQL
    +-----------+--------------+
    |  dow_str  | Pct_To_Total |
    +-----------+--------------+
    | Tuesday   | 0.187471     |
    | Wednesday | 0.183772     |
    | Thursday  | 0.179849     |
    | Monday    | 0.172762     |
    | Friday    | 0.162636     |
    | Saturday  | 0.061281     |
    | Sunday    | 0.052229     |
    +-----------+--------------+
    ```
    
  * SQL query: 
      ```sql
    #standardSQL
               $ bq query --use_legacy_sql=false "SELECT a1.dow_str, FORMAT(\"%f\", (count(*) /
                 (SELECT count(*) FROM \`profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view\`))) AS Pct_To
                _Total FROM \`profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view\` a1 group by a1.dow_str 
                order by Pct_To_Total desc"
      ```

- Question 2: Rank the months of year by total percentage of use.
  * Answer:
    ```sql
    #standardSQL  
    +------------+--------------+
    | trip_month | Pct_To_Total |
    +------------+--------------+
    |          8 | 0.097165     |
    |         10 | 0.095947     |
    |          6 | 0.093196     |
    |          7 | 0.091027     |
    |          9 | 0.088773     |
    |          5 | 0.087800     |
    |          4 | 0.085596     |
    |          3 | 0.083136     |
    |         11 | 0.074306     |
    |          1 | 0.072981     |
    |          2 | 0.071148     |
    |         12 | 0.058925     |
    +------------+--------------+
    ```
  * SQL query: 
    ```sql
    #standardSQL
              $ bq query --use_legacy_sql=false  "SELECT  EXTRACT(MONTH FROM a.start_date) as 
                trip_month, FORMAT(\"%f\", (count(*) / (SELECT count(*) FROM \`profound-surf-264703.bike_trip_data.bike_trip_distanc
                e_duration_station_view\`))) AS Pct_To_Total FROM \`profound-surf-264703.bike_trip_data.bike_trip_distance_duration_
                station_view\` a  group by trip_month  order by Pct_To_Total desc"
    ```
- Question 3: Break down Bike usage by customer type (ratio of total trips by annual subscribers and daily customers)
  * Answer:
    ```sql
    #standardSQL  
    +-----------+--------------+-----------------+
    | num_trips | Pct_To_Total | subscriber_type |
    +-----------+--------------+-----------------+
    | 846839    | 0.860917     | Subscriber      |
    +-----------+--------------+-----------------+
    | 136809    | 0.139083     | Customer        |
    +-----------+--------------+-----------------+    
    ```
  * SQL query:
    ```sql
    #standardSQL  
      select
      count(*) as num_trips, 
      FORMAT("%f", (count(*) / (SELECT count(*) FROM `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`))) AS Pct_To_Total,
      subscriber_type
    from 
        `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`
      group by
        subscriber_type
      order by Pct_To_Total desc
   ```
  
- Question 4: Rank trips in descending order buckets of trip times (e.g. trip less than 5 minutes, greater than 5 minutes and less than 10 minutes). Identify which trips are most frequent as percentage of total.
  * Answer:
    ```sql
    #standardSQL   
    +------------------------+--------------+
    | duration_min_slots     | Pct_To_Total |
    +------------------------+--------------+
    | 5 < duration <=10 min  | 0.420255     |
    +------------------------+--------------+
    | 10 < duration <=20 min | 0.302875     |
    +------------------------+--------------+
    | 3 < duration <=5 min   | 0.147016     |
    +------------------------+--------------+
    | 20 < duration <=30 min | 0.034393     |
    +------------------------+--------------+
    | 3 min or less          | 0.031651     |
    +------------------------+--------------+
    | >30 min                | 0.031231     |
    +------------------------+--------------+
  ```
  * SQL query:
    ```sql
    #standardSQL        
        select            	
         CASE 	
                   WHEN duration_min <= 3 THEN "3 min or less"	
                   WHEN duration_min > 3  and  duration_min <= 5 THEN "3 minutes < duration <= 5 minutes"	
                   WHEN duration_min > 5  and  duration_min <= 10 THEN "5 minutes < duration <= 10 minutes"	
                   WHEN duration_min > 10  and  duration_min <= 20 THEN "10 minutes < duration <= 20 minutes"	
                   WHEN duration_min > 20  and  duration_min <= 30 THEN "20 minutes < duration <= 30 minutes"	
                   WHEN duration_min > 30 THEN "> 30 min"	
                   END AS duration_min_slots,	
        FORMAT("%f", (count(*) / (SELECT count(*) FROM `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`))) AS Pct_To_Total                   	
        FROM 	
            `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view` a	
        where 	
              start_station_name <> end_station_name	
        group by duration_min_slots	
        ORDER BY Pct_To_Total desc	  
      ```
  

- Question 5: Rank trips in buckets of trip durations (e.g. trip less than 2 miles long, greater than 5 miles and less than 10 miles). Identify which trips are most frequent as percentage of total.
  * Answer:
    ```sql
    #standardSQL 
    +---------------------------------+--------------+
    | trip_distance                   | Pct_To_Total |
    +---------------------------------+--------------+
    | less than 2 miles               | 0.962615     |
    +---------------------------------+--------------+
    | 2 miles < distance <= 5 miles   | 0.004580     |
    +---------------------------------+--------------+
    | 5 miles < distance <= 10 miles  | 0.000116     |
    +---------------------------------+--------------+
    | 20 miles < distance <= 30 miles | 0.000049     |
    +---------------------------------+--------------+
    | 10 miles < distance <= 20 miles | 0.000035     |
    +---------------------------------+--------------+
    | > 30 miles                      | 0.000026     |
    +---------------------------------+--------------+    
    ```
  * SQL query:
    ```sql
    #standardSQL   
        select            	
         CASE 	
                   WHEN distance_between_stations <= 2 THEN "less than 2 miles"	
                   WHEN distance_between_stations > 2  and  distance_between_stations <= 5 THEN "2 miles < distance <= 5 miles"	
                   WHEN distance_between_stations > 5  and  distance_between_stations <= 10 THEN "5 miles < distance <= 10 miles"	
                   WHEN distance_between_stations > 10  and  distance_between_stations <= 20 THEN "10 miles < distance <= 20 miles"	
                   WHEN distance_between_stations > 20  and  distance_between_stations <= 30 THEN "20 miles < distance <= 30 miles"	
                   WHEN distance_between_stations > 30 THEN "> 30 miles"	
                   END AS trip_distance,	
        FORMAT("%f", (count(*) / (SELECT count(*) FROM `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view`))) AS Pct_To_Total                   	
        FROM 	
            `profound-surf-264703.bike_trip_data.bike_trip_distance_duration_station_view` a	
        where 	
              start_station_name <> end_station_name	
              and distance_between_stations <> 0
        group by trip_distance	
        ORDER BY Pct_To_Total desc	  
    ```
- ...

- Question n:
  * Answer:
  * SQL query:

---

## Part 3 - Employ notebooks to synthesize query project results

### Get Going

Create a Jupyter Notebook against a Python 3 kernel named Project_1.ipynb in the assignment branch of your repo.

#### Run queries in the notebook 

At the end of this document is an example Jupyter Notebook you can take a look at and run.  

You can run queries using the "bang" command to shell out, such as this:

```
! bq query --use_legacy_sql=FALSE '<your-query-here>'
```

- NOTE: 
- Queries that return over 16K rows will not run this way, 
- Run groupbys etc in the bq web interface and save that as a table in BQ. 
- Max rows is defaulted to 100, use the command line parameter `--max_rows=1000000` to make it larger
- Query those tables the same way as in `example.ipynb`

Or you can use the magic commands, such as this:

```sql
%%bigquery my_panda_data_frame

select start_station_name, end_station_name
from `bigquery-public-data.san_francisco.bikeshare_trips`
where start_station_name <> end_station_name
limit 10
```

```python
my_panda_data_frame
```

#### Report in the form of the Jupter Notebook named Project_1.ipynb

- Using markdown cells, MUST definitively state and answer the two project questions:

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- For any temporary tables (or views) that you created, include the SQL in markdown cells

- Use code cells for SQL you ran to load into Pandas, either using the !bq or the magic commands

- Use code cells to create Pandas formatted output tables (at least 3) to present or support your findings

- Use code cells to create simple data visualizations using Seaborn / Matplotlib (at least 2) to present or support your findings

### Resource: see example .ipynb file 

[Example Notebook](example.ipynb)

