---
title: Fundamentals of Data Engineering
author: Week 04 - sync session
...

---


#
## While we're getting started

- Review your Project Questions 
- Get ready to share

::: notes
Breakout at about 5 after the hour:
- Check in with each group on Project 1
- Answer questions as people have them on what they had trouble with
- Usually takes 10-20 minutes
:::

#
## Overview
- Intro Docker
- PRs from the command line

# 
## Project Review

# 

## Our Project Questions
- What is a trip?
- What are the most common trips?
- How does this differ based on trip type (commuter vs all)?
- What is a commuter trip?

::: notes
- What is a commuter trip?
  * A trip during rush hour
  * Write a query to determine if a trip happens from 7-9 am or 4-7 pm. (or how many trips do...)
:::

## Housekeeping

- Class flow

:::notes
- The following few slides review the flow of when things are due and what readings/videos go with which week.
:::

## Where are we in the Query Project?

- Answer your Project Questions
- Use Jupyter Notebook to do some visualizations and write up your reasoning for the recommendations you choose to make.

::: notes
use bigquery or bq cli for some of this
:::


#
## Docker: Where am I?

- Working with Docker
- Use it to explore cli ways to find out what's up with data
- How do we find our way around with Docker?

## Run the regular container

```
docker run -it --rm -v ~/w205:/w205 midsw205/base bash
```

::: notes
```
docker run -it --rm -v ~/w205:/w205 midsw205/base bash
```
:::

## What containers are running right now?

- New terminal window

- `docker ps`

## What containers exist?

- `docker ps -a`

## Container name

- `fervent_austin` is my running `midsw205/base:latest` container

## What images do I have?

- Images vs. containers

- `docker images`

## Image name 

- Need both repository & tag

- e.g., `midsw205/base:latest`

## Clean up containers

`docker rm -f <name-of-container>`

::: notes
:::

#
## Idiomatic docker

- start a `midsw205/base:latest` container
- run `pwd`
- exit container

-vs-

```
docker run -it --rm -v ~/w205:/w205 midsw205/base pwd
```
 
::: notes
I hope some of this simplifies when we start using the containers to _just_ run a command... i.e.,
`docker run [<opts>] <image> [<command>]`
... e.g., 
ME: check this query for backticks from bq cli sql
`docker run -it --rm midsw205/base bq query --use_legacy_sql=false 'select count(*) from mytable'`
in one go (edited)

then they're only "in" one place
:::


# 

## Git Branching

## Clone a repo from GitHub

```
git clone \
  https://github.com/mids-w205-martin-mims/signup-htmartin
```

    cd signtup-htmartin

## Create a branch to work from

    git branch my-cool-feature

## Switch to that branch

    git checkout my-cool-feature

## Make changes to code

    vi README.md

::: notes
- M: no vi in container?
:::

## Commit those changes

    git commit -m'updated README' README.md

## Push those up to GitHub

    git push origin my-cool-feature


## Note  
- If this is the first time you've pushed to the remote `my-cool-feature` branch, then this command will automatically _create_ that branch in your github repo and then push your changes to it.

## Pull Request from the GitHub Web-UI

- Select "New Pull-Request"

- Select branches so that you are "Requesting to merge changes from `my-cool-feature` branch _into_ `master`."

- Select your instructor(s) to review.

- Submit


#
## Summary
- git branching
- using docker

::: notes
docker-compose is for this
:::


## Week 4 videos 
- Relational Data Stores  
- NoSQL Data Stores
- Understand the RDB store we've been working with with big query
- Get ready to work with the nosql store redis next week as we start Project 2


##

![](images/pipeline-overall.svg)

::: notes
docker-compose is for this
:::


# 

## Extras


#

<img class="logo" src="images/berkeley-school-of-information-logo.png"/>

