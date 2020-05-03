
## Course Description

Storing, managing, and processing datasets are foundational processes in data
science. This course introduces the fundamental knowledge and skills of data
engineering that are required to be effective as a data scientist. This course
focuses on the basics of data pipelines, data pipeline flows and associated
business use cases, and how organizations derive value from data and data
engineering.  As these fundamentals of data engineering are introduced,
learners will interact with data and data processes at various stages in the
pipeline, understand key data engineering tools and platforms, and use and
connect critical technologies through which one can construct storage and
processing architectures that underpin data science applications.

## Course Format

The course is organized as an online inverted classroom. During each week, students first
work through a set of asynchronous materials, including video lectures, readings, and other
activities. Once a week, students meet for a 90-minute live session, in which they connect with
an instructor and other students in an online classroom. A functioning webcam and an audio
headset are required to participate in the live sessions. Students must complete all assigned
asynchronous material before the scheduled live session begins.

## Course Objectives

### Tools and Technologies

Students will:

- Build practical experience building data pipelines.
- Build practical experience cleaning, anonymizing, and plumbing data.
- Learn tooling for queries and query management (e.g., BigQuery, SQL).
- Learn tooling for analytics (jupyter, python, py-based-libs).
- Get exposure to advanced tooling for analytics (spark, kafka, etc).
- Learn how to leverage revision control.
- Learn how to use docker to assemble common tools for analysis.
- Build practical experience leveraging cloud-based resources for data analytics.
- Build practical experience consuming data and services from APIs.
- Get exposure to events and event-log based analytics.

### Concepts

Students will:

- Learn to keep their analysis grounded in business relevance.
- Get exposure to some basic distributed storage and compute concepts.
- Get exposure to some basic RDBMS concepts.
- Get exposure to RDB -vs- NoSQL tooling and approaches.
- Get exposure to some basic data warehousing concepts.
- Learn the basics of virtualization and containerization.
- Understand how analysis changes wrt scale / complexity of data.
- Learn about data partitioning.
- Learn about latency in data analysis.
- Get exposure to ETL -vs- NoETL.
- Learn the basic concepts of web-based applications.
- Understand how basic data privacy, security, and chain-of-custody works.


## Course Tools

In this class we will be using cloud instances on Google Cloud Platform (GCP)
for all class activities and projects. We will set these up in the first week
of class, but if you'd like to get a head start, here are some notes.

We'll have you
[create](https://cloud.google.com/ai-platform/notebooks/docs/create-new)
an
[AI Platform Notebook](https://cloud.google.com/ai-platform-notebooks/)
instance for class.
These are general instructions as well as a general
[video on AI Platform Notebooks](https://www.youtube.com/watch?v=Eu57QKNHaiY)
that goes into a little more depth.

The only differences to note for class are:

- Sign up with your UCB ISchool email address and you should get a fresh $300
  credit for GCP.  This should more than cover the instance expense for the
  semester

- Please create your instance from the TensorFlow-2.0 image when prompted

- We recommend you customize the AI Platform Notebook Instance to be smaller
  (cheaper) than the default.  A single cpu core with 4G RAM and no GPU should
  suffice for class.  You can always increase/add these later if you want to
  use this for other projects/classes


## Evaluation & Grading

### Projects

There are three projects:

- Query Project
- Tracking User Activity
- Understanding User Behavior

that collectively form the core of this course. Your work on them is one of the
best ways for you to learn, and they each count for a third of your grade in this
course.

### Due Dates for Projects

Please check with your section instructor for definitive due dates for your
projects.


## Readings

Most readings are available through a subscription to
https://www.safaribooksonline.com/. Other readings are blog posts and links.


## Prerequisites

- Previous experience with Python
- Basic knowledge of Unix/Linux commands and tools as well as concepts such as
  processes, file systems
- In addition we'll use Docker, Git, and SQL as well as other tools
- If you feel like you're not where you'd like to be with these
  technologies/tools, here are some resources to get up to speed. There are
  options, pick which one best suits your needs

#### SQL

    SQL Tutorial
    w3schools.com
    https://www.w3schools.com/sql/default.asp

    Learning SQL, 2nd Edition
    by Alan Beaulieu
    https://www.safaribooksonline.com/library/view/learning-sql-2nd/9780596801847/

#### The Command Line

	Learning the Shell
	by William E. Shotts, Jr.
	http://linuxcommand.org/lc3_learning_the_shell.php

#### Git

	Pro Git book
	by Scott Chacon and Ben Straub 
	https://git-scm.com/book/en/v2

#### Python

	Python for Data Analysis, 2nd Edition
	by William Wesley McKinney
	https://www.safaribooksonline.com/library/view/python-for-data/9781491957653/

#### Docker

	Getting Started with Docker
	https://docs.docker.com/get-started/

	Using Docker
	by Adrian Mouat
	https://www.safaribooksonline.com/library/view/using-docker/9781491915752/

## Course Outline

The course consists of 4 sections:

-   [Introduction](#introduction)
    -   [Week 01 - Introduction](#week-01---introduction)
    -   [Week 02 - Working with Data](#week-02---working-with-data)
    -   [Week 03 - Welcome to the Queryside](#week-03---welcome-to-the-queryside)
-   [The Basics](#the-basics)
    -   [Week 04 - Storing Data](#week-04---storing-data)
    -   [Week 05 - Storing Data II](#week-05---storing-data-ii)
    -   [Week 06 - Transforming Data](#week-06---transforming-data)
    -   [Week 07 - Sourcing Data](#week-07---sourcing-data)
    -   [Week 08 - Querying Data](#week-08---querying-data)
-   [Streaming](#streaming)
    -   [Week 09 - Ingesting Data](#week-09---ingesting-data)
    -   [Week 10 - Transforming Streaming Data](#week-10---transforming-streaming-data)
    -   [Week 11 - Storing Data III](#week-11---storing-data-iii)
    -   [Week 12 - Querying Data II](#week-12---querying-data-ii)
-   [Putting it All Together](#putting-it-all-together)
    -   [Week 13 - Understanding Data](#week-13---understanding-data)
    -   [Week 14 - Patterns for Data Pipelines](#week-14---patterns-for-data-pipelines)


A 3-week Introduction that covers the basics of storage and retrieval concepts
and tools; a 5-week Basics section that provides a deeper exploration of
working with data and data pipelines; a 4-week section that focuses on
Streaming Data; and a concluding section, Putting it All Together, that
integrates concepts and skills from the entire course into a cohesive model of
the data pipeline.

In addition to the sequenced material covered, the course also includes
Tutorial materials that focus on technical skills associated with data
engineering technologies, tools, and platforms. These tutorials also provide a
practical foundation for the discussions and activities that will take place in
the live classroom for specific weeks in the term.

