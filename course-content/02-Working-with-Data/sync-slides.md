---
title: Fundamentals of Data Engineering
author: Week 02 - sync session
...

---

# 


## Your cloud instance set up

- repos cloned:
    - `course-content`

## How to create a new branch, commit to that and do a PR

- Process from commandline and giu this time

::: notes
we have gone through the gui last week, now let's how this works from the commandline. Note: you can't create a PR from the cli, PRs are github specific
:::


# 
## Some things about this class


## Pacing

- What you can do
- What you can understand

::: notes
We'll be reading/watching screencasts ahead of what we can do
:::


# 
## Where are we in the pipeline

![](images/pipeline-overall.svg)



## Main thing to pay attention to

- Pipeline is provided for this example
- We're _using_ it to answer business questions

::: notes
How would we build this ourselves?
:::


# 

## Business Decisions

- All about the business

- Data-Driven Business Decisions ...are queries

::: notes
in order for business decisions to be based on data, you have to be able to interact with the data.

business requirements get encoded as queries of data
:::

## Translation

- SQL queries are really pretty easy
- How to get to the queries from the questions, sometimes not so much


# 
## Query Project

- In the Query Project, you will get practice with SQL while learning about Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven questions using public datasets housed in GCP. To give you experience with different ways to use those datasets, you will use the web UI (BiqQuery) and the command-line tools, and work with them in jupyter notebooks.

- We will be using the Bay Area Bike Share Trips Data, follow the class walk through to find the data set. 

::: notes
Go over what the dataset is on the webpage
:::


## Problem Statement
- You're a data scientist at a company formerly known Ford GoBike, now Lyft bay wheels (<https://www.lyft.com/bikes/bay-wheels>). You are trying to increase ridership, and you want to offer deals through the mobile app to do so. What deals do you offer though? Currently, your company has three options: 

- a flat price for a single one-way trip, 
- a day pass that allows unlimited 30-minute rides for 24 hours, 
- and an annual membership. 

## Questions

- Through this project, you will answer these questions: 
  * What are the 5 most popular trips that you would call "commuter trips"?
  * What are your recommendations for offers (justify based on your findings)?

::: notes
:::


## Working with BQ gui

<https://console.cloud.google.com/bigquery>


#
## Some annoying specific stuff about BQ

## the `;`

    SELECT * 
    FROM Customers;

VS 

    SELECT * 
    FROM Customers

::: notes
- Nearly all other sql implementations (and what you will see in the tutorial), end statements with a `;`
- BQ doesn't
- btw, the CAPITALIZATION isn't necessary :)
:::

## Legacy vs Standard SQL


    SELECT *
    FROM [bigquery-public-data:san_francisco.bikeshare_trips]

VS 

    #standardSQL
    SELECT * 
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`

::: notes
- Google was going to create their own sql that worked different :)
- It's silly, but the way the table reference part, the "FROM" part, is written is different.
- So, now there's the `#standardSQL` flag
:::



## For this class

	#standardSQL
	SELECT * 
	FROM `bigquery-public-data.san_francisco.bikeshare_status`


- More similar to command line bq
- More like most other SQL implementations

::: notes
We're doing this one, but you can use either
:::
#
## Events

- What sort of events feed this pipeline?
- How were these events captured?

::: notes
Fed from device events:

- station kiosk (?)
- user app (?)
:::

#
## Querying Data

## How many events are there?

::: notes
For the following slides,
Wait on the question slide for a minute to give everyone a chance to try it.

Then reveal the next slide with query.

- Optional: you can do these in groups and ask people to 

  * report out
  * share issues, false starts they ran into 

[Obviously more useful on more complicated queries]
:::

##

	#standardSQL
	SELECT count(*)
	FROM `bigquery-public-data.san_francisco.bikeshare_status`


::: notes
107,501,619

The point: you can use `select *` to actually answer questions.
:::

## How many stations are there?

##

	#standardSQL
	SELECT count(distinct station_id)
	FROM `bigquery-public-data.san_francisco.bikeshare_status`

::: notes
The point: how to count unique
Answer: something like 75
:::


## How long a time period do these data cover?

##

	#standardSQL
	SELECT min(time), max(time)
	FROM `bigquery-public-data.san_francisco.bikeshare_status`


::: notes
- 2013-08-29 12:06:01.000 UTC	
- 2016-08-31 23:58:59.000 UTC	
:::

## How many bikes does station 90 have?


::: notes
Break into groups here.
Give them a few minutes, have someone from each group screen share and present their query.
If they don't tell you, ask why they made the choices they made.
I decided that a station's total bikes would `= docks_available + bikes_available`.
:::


##

	#standardSQL
	SELECT station_id, 
	(docks_available + bikes_available) as total_bikes
	FROM `bigquery-public-data.san_francisco.bikeshare_status`
	WHERE station_id = 90

::: notes
Stuff to explore:

- each station "has" different unique numbers of bikes [probably b/c e.g., docks are added to stations, etc, etc, etc]
- if you create a view, use these queries:


	#standardSQL
	SELECT distinct (station_id), total_bikes
	 FROM `ambient-cubist-185918.bike_trips_data.total_bikes`

	#standardSQL
	SELECT distinct station_id, total_bikes
	FROM `ambient-cubist-185918.bike_trips_data.total_bikes`
	WHERE station_id = 22


This shows that you get multiple entries for each `station_id` b/c diff values of total bikes
:::



## Independent Queries

<https://www.w3schools.com/sql/default.asp>

::: notes
If there's any time, break in groups to do whatever questions they come up with. 
Rotate between groups to see what folks are coming up with.
:::



# 
## Summary

- Business questions
- Answered using empirical data
- By running queries against (raw?) events
- Need a pipeline in place to capture these raw events

#

<img class="logo" src="images/berkeley-school-of-information-logo.png"/>

