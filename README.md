# Cyclistic_Bike-Share
A Case Study on how does a Bike-Share navigate speedy success:

This Case Study has been created as an essential component of the Google Data Analytics Professional Certificate Capstone.

## Senario and Projet Overview 
Cyclistic is a bike-share company in Chicago that was luanched in 2016. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. 
The director of marketing Lily Moreno, believes that the companys's future success depends on maximizing the number of memberships. Therefore, This data analysis aims to offer comprehensive insights into the distinct usage patterns of Cyclistic Bikes, encompassing both casual passengers and annual subscribers. Through a meticulous examination of various facets of the data, this analysis endeavors to discern prevalent trends, formulate data-driven recommendations, and deisgn a new markeing stratgey to convert casual passengers into annual subscribers. 

The project will follow the six phases of data analysis which includes: **Ask**, **Prepare**, **Process**, **Analyze**, **Share** and **Act**. 

### Phase 1: Ask 
There are couple questions that can guide the future marketing program and help the team achieve the needed results which are: 

1. How do annual members and casual riders use Cyclistic bikes differently?
2. why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

The director Moreno has assigned me the first question to answer which is: **How do annual members and casual riders use Cyclistic bikes differently ?**

#### Key Tasks 
**1. The business task**

The task of this analysis is to pinpoint essential factors and detect patterns in Cyclistic Bike-Share usage among two user groups: casual riders and annual subscribers. This understanding will enable the company to enhance its profit share by developing a new marketing plan focused on converting casual riders into annual subscribers.

**2. Stakeholders**

Main stakeholder: 
* **Lily Moreno**: Team Manager, Marketing director
  
Subsidiary stakeholders: 
* **Marketing analytics team**
* **Executive team**

### Phase 2: Prepare

**1. Data Sources**
In this project, we will be using a public historical trip data provided by the company itself under this [licence](https://divvybikes.com/data-license-agreement). The data has been made available by Motivate International Inc. The statistics are orgnized as long data in CSV files  which gives information from 2013 to 2023, and it was retreived from [Data](https://divvy-tripdata.s3.amazonaws.com/index.html) and it has been safely stored in a local drive. 
The data is a good fit for this analysis as it accomplish the required conditions for the credibility and fullfill the ROCCC approach: **Reliable**, **Original**, **Comprehensive**, **Current** and **Cited**.

**2. Sort and filter the data**

For this examination i am going to focus on the period between 2021 and 2023 as it is the more recent and relevant period of the business task. 

### Phase 3: Process

In this phase, we will clean the data and make it free of errors or mistake which could affect the credibility or the conclusions. To achieve this gool, we will be using couple tools which will be cited as follow. 

**1. Tools**
* **Excel:** Data cleaning
* **RStudio:** Data analysis
* **Tableau Public:** Data visualisation and reports creation

**1.1. Excel:** 

First I opened the CSV files into Ms Excel to clean the data. The cleaning steps taken include:

* Removal of columns I won't needing for my analysis like start and end station names, station ids, latitudes, and longitudes.
* Creation of ride_length column which is the time diference between the trip start time and the end time substracting the column "started at" and "ended at".
* Creation of day_of_week column which is the day of the week the trip started using the function WEEKDAY.
* Removal of rows with negative and zero ride lengths.
* Duplicates: Rows with identical data.
* Empty Cells: Cells with no data.
* Inconsistent Formatting: Different formats for the same type of data.
* Errors and Typos: Incorrect or misspelled entries.
* Non-printable Characters: Hidden characters that may cause issues
  
After cleaning and organizing data, I saved a copy for each CSV file as XLS under a subfolder named XLS.

### Phase 4: Analyze


**1.1. RStudio:** 

As part of the preparation of data, the following is done:

* the various datasets are imported to R
* the structure of the datasets are analyzed to ensure consistency

First I added all the libraries necessary for my analysis: 

* >library(tidyverse)
* >library(lubridate)
* >library(ggplot2)
* >library(dplyr)
* >library(tidyr)
* >library(readr)
* >library(tibble)
* >library(stringr)
* >library(forcats)
* >library(readxl)

Then I donwloded the required packages needed for this libraries and analysis.

Later, using **<-read.cvs** loading the 12 datasets for the 12 months from November 2022 untill October 2023 of my analysis and combine these datasets into a single dataset 

* >`2022/11` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202211-divvy-tripdata 2.csv", sep=";")
  >   View(`2022/11`)
* > `2022/12` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202212-divvy-tripdata.csv", sep=";")
  >   View(`2022/12`)
* > `2023/01` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202301-divvy-tripdata.csv", sep=";")
  >   View(`2023/01`)
* > `2023/02` <- read.csv2("~/Desktop/Cyclistic data.CSV/edited CSV/202302-divvy-tripdata.csv", sep=";")
  >   View(`2023/02`)
* > `2023/03` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202303-divvy-tripdata.csv", sep=";")
  >   View(`2023/03`)
* > `2023/04` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202304-divvy-tripdata.csv", sep=";")
  >   View(`2023/04`)
* > `2023/05` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202305-divvy-tripdata.csv", sep=";")
  >   View(`2023/05`)
* > `2023/06` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202306-divvy-tripdata.csv", sep=";")
  >   View(`2023/06`)
* > `2023/07` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202307-divvy-tripdata.csv", sep=";")
  >   View(`2023/07`)
* > `2023/08` <- read.csv2("~/Desktop/Cyclistic data.CSV/edited CSV/202308-divvy-tripdata.csv", sep=";")
  >   View(`2023/08`)
* > `2023/09` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202309-divvy-tripdata.csv", sep=";")
  >   View(`2023/09`)
* > `2023/10` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202310-divvy-tripdata.csv", sep=";")
  >   View(`2023/10`)

Now is to combine all the dataset into one: 















