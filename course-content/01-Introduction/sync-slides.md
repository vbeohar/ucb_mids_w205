---
title: Fundamentals of Data Engineering
author: Week 01 - sync session
...

---


# 
## Week 1 - Overview

- Introductions
- Set up your working environment for this class
- Review syllabus, course goals, processes & tools ...

::: notes
See ~/taylor-oreilly/data-engineering-course/solutions/setup.md
:::

## Introductions

::: notes
Introduce yourself :)
Student introductions
:::

## In this class, you will

- Gain exposure to basic problems associated with data and data-driven decision-making
- Develop a working knowledge of some tools/techniques used to solve these problems
- Learn where to go for help and more info

::: notes

:::

## Just enough

::: notes
You'll hear this over and over, but basics of worldview
...
:::

## { data-background="images/pipeline-overall.svg" } 

::: notes
This pipeline is your anchor, basically where are we and how does here relate to the rest of the class
:::

## Process/Procedures

- Good practices
- Appropriate tools
- Getting used to

::: notes
For your other classes, they may use a variety of ways to get content, turn in projects etc. 

Here, we're trying to follow good practices for data engineering and use appropriate tools. 

this will probably take some getting used to at first (unless you already use git all day every day, which is great, help your friends)
:::

#
## How this class works


## Syllabus

```
https://mids-w205-fund-of-data-eng.github.io/course-content/
```

::: notes
Prereqs
Video links
Readings
:::

## Asyncronous Content

```
https://github.com/mids-w205-martin-mims/course-content/ \
blob/master/01-Introduction/async-videos.md
```

- Same as in ISVC, but you can access it all in one place here.

## Readings

- No one textbook available for this course.
- Using subscription service to cover the range of topics.
- `https://www.safaribooksonline.com/pricing/`
- Individual option: $39/month (can stop whenever you want)
- Quick note: Get the mobile apps.

## Prerequisites

- Resources listed under prereqs
- Safari has tons of other materials you can help yourself with.


## Course Outline

- 4 sections:  
- 3-week Introduction
- 5-week Basics section 
- 4-week Streaming Data section
- Putting it All Together


::: notes
- 3-week Introduction covers the basics of storage and retrieval concepts and tools
- 5-week Basics section  provides a deeper exploration of working with data and data pipelines
- 4-week section that focuses on Streaming Data; and a 
- 1-week wrapup, Putting it All Together, integrates concepts and skills from the entire course into a cohesive model of the data pipeline.
:::


#
## Student Projects

## Student Projects

1. Querying Data
2. Tracking User Activity
3. Understanding User Behavior

## { data-background="images/pipeline-overall.svg" } 

::: notes
Back to the pipeline - What part are we in?
:::

## Querying Data

- Use existing tools/pipeline/dataset
- Answer basic business questions

::: notes
data-driven business decisions

prompt/reinforce the connection

validation/testing?  (how good are our results?)

(intro to model management?)
:::

## Tracking User Activity

- Use provided pipeline components
- Transform/store data
- Answer business questions
- Bonus:
    - Trigger notifications

::: notes
"Catching and Transforming Data using plumbing that's provided"

Catching Data

Classifying Events
Filtering/Sorting/Grouping
Transforming Data

Storing Data
:::

## Understanding User Behavior

- Assemble an end-to-end pipeline
- Ingest/transform/store data
- Answer comprehensive business questions
- Bonus:
    - Manage sessionization / state

::: notes
end-to-end pipeline for understanding behavior

you assemble the plumbing

baseline: queries to answer questions about the user activity

bonuses as above
:::

## Levels of Expertise
::: notes
- If you're brand new to something, you'll get it taken care of. 
- If you've nailed it, get creative
:::



## Async
-   To get ready for project 1, videos - how events are generated


#
## Activities

- Let's get going!

::: notes
With all of that in mind, let's get going!
:::


#
## Slack

::: notes
We're using slack for this class

Instructors specify each section's slack channel
:::


#
## Cloud Instances

::: notes
We'll be working from cloud instances in this class
:::


##

1. Sign up for GCP account
2. Create your instance
3. Access your instance

::: notes

- walk through this in class using cloud.google.com

- using ISchool email should get a fresh $300 credit which should more than
  cover the instance for the semester
:::

## Create your instance

::: notes

- AI Platform -> Notebooks -> Create
- Customize machine type
- Customize bookdisk to keep after deleting the instance
:::

## Access JupyterHub

AI Platform -> Notebooks -> "Open Jupyterlab"


## Access your instance

- Compute Engine -> VM Instances -> "SSH"
- Settings -> Change Linux Login -> "jupyter"

::: notes

- gcp creates/injects usernames when you first ssh into the instance

- We need to use the settings in the top right of the SSH terminal and change
  the login user to "jupyter" to see the same stuff as jupyterlab
:::


#
## Docker

::: notes
What is docker? Very brief version
:::

##

![](images/dontpanic.jpeg)

::: notes
These commands will look gnarly.

Don't worry about it, we will review....blah, blah,

For now, just follow along
:::

##

- pull the image:
  ```
  docker pull midsw205/base
  ```
- create your mids-w205 workspace:
  ```
  mkdir w205
  ```
- run (set _your_ home directory for "`-v`")
  ```
  docker run \
    -it \
    --rm \
    -v ~/w205:/w205 \
    midsw205/base:latest \
    bash
  ```
- `exit` (or `ctrl-d`)

::: notes
Like we said, we'll get into what all those options mean etc, just keep track for now

```
docker run -it --rm -v ~/w205:/w205 midsw205/base:latest bash
```
:::


#
## Git

::: notes
What is git?

go over set up of folders, show git hub...
:::

## Git set up

## Clone the `course-content` repo
- `cd w205`
- Clone the `course-content` repo into your mids-w205 workspace:
```
git clone https://github.com/mids-w205- \
  <instructor-last-name>/course-content
```

::: notes
```
git clone https://github.com/mids-w205-<instructor-last-name>/course-content
```

You can copy/paste complex commands from the markdown version of these lecture notes
in the course-content repo
:::


#
## Signup Assignment

## Clone the repo
- `cd w205`
- Clone the repo into your mids-w205 workspace:
```
git clone https://github.com/mids-w205- \
  <instructor-last-name>/ \
  signup-<git-user-name>
```

::: notes
```
git clone https://github.com/mids-w205-<instructor-last-name>/signup-<git-user-name>
```
:::

## Open, Change, Close  `README.md` 
- `nano README.md`
- change line
- `ctrl-o`
- return
- `ctrl-x`
- Now you're out of nano.

::: notes
Or just use whatever text editor you have, these are basically directions for doing this in the container.
:::

## Git: commit changes

- `git status`
- `git add README.md`
- `git commit -m 'my new readme'`
- The first time you commit, it doesn't know who you are.
  ```
  git config --global user.email "you@example.com"
  ```
  ```
  git config --global user.name "Your Name"
  ```
- `git commit -m 'my new readme'`
- `git push`


## Git: submit a PR
- All projects submitted as PRs
  ```
  https://github.com/mids-w205-martin-mims/signup-<user-name>
  ```
- Click on `README.md`
- Click on edit button (pencil icon)
- Make a change
- "Commit changes" section, select "Create a new branch for this commit..."
- Enter PR name & description
- Click "Propose file change" button
- Assign instructors as reviewers
- Click "Create pull request" button

::: notes
Do this in the gui
:::


#
![](images/berkeley-school-of-information-logo.png){.logo}
