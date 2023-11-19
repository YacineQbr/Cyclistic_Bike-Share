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
In this project, we will be using a public historical trip data provided by the company itself has been made available by Motivate International Inc. under this [licence](https://divvybikes.com/data-license-agreement). The data has been made available by Motivate International Inc. The statistics are orgnized as long data in CSV files  which gives information from 2013 to 2023, and it was retreived from [Data](https://divvy-tripdata.s3.amazonaws.com/index.html) and it has been safely stored in a local drive. 
The data is a good fit for this analysis as it accomplish the required conditions for the credibility and fullfill the ROCCC approach: **Reliable**, **Original**, **Comprehensive**, **Current** and **Cited**.

**2. Sort and filter the data**

For this examination I am going to focus on the period between November 2022 and October 2023 as it is the more recent and relevant period of the business task. 

### Phase 3: Process

In this phase, we will clean the data and make it free of errors or mistake which could affect the credibility or the conclusions. To achieve this gool, we will be using couple tools which will be cited as follow. 

**1. Tools**
* **Excel:** Data cleaning
* **RStudio:** Data Cleaning and analysis
* **Tableau Public:** Data visualisation and reports creation

**1.1. Excel:** 

First I opened the CSV files into Ms Excel to clean the data. during the process I used Power Query Editor which is a useful method for time-saving.  The cleaning steps include:


* Removal of columns I won't needing for my analysis like start and end station names, station ids, latitudes, and longitudes.
* Creation of ride_length column which is the time diference between the trip start time and the end time substracting the column "started at" and "ended at".
* Creation of day_of_week column which is the day of the week the trip started using the function WEEKDAY.
* Removal of rows with negative and zero ride lengths.
* Duplicates: Rows with identical data.
* Empty Cells: Cells with no data.
* Inconsistent Formatting: Different formats for the same type of data.
* Errors and Typos: Incorrect or misspelled entries.
* Non-printable Characters: Hidden characters that may cause issues
  
### Phase 4: Analyze

There were over 5 million records, making the use of spreadsheets impractical for data cleaning. Faced with two choices, SQL and R, I was a little familir with both of them. Given my penchant for learning new programming languages as a new Data Analyst, I saw this as a valuable chance to acquire R skills. Consequently, I opted for R.

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

Later, using **<-read.cvs** to load the 12 datasets for the 12 months from November 2022 untill October 2023 of my analysis and combine them into a single dataset. While pulling the dataset, I renamed each file to this format YYYY/MM.

* > `2022/11` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202211-divvy-tripdata.csv", sep=";")
  >   View(`2022/11`)
* > `2022/12` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202212-divvy-tripdata.csv", sep=";")
  >   View(`2022/12`)
* > `2023/01` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202301-divvy-tripdata.csv", sep=";")
  >   View(`2023/01`)
* > `2023/02` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202302-divvy-tripdata.csv", sep=";")
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
* > `2023/08` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202308-divvy-tripdata.csv", sep=";")
  >   View(`2023/08`)
* > `2023/09` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202309-divvy-tripdata.csv", sep=";")
  >   View(`2023/09`)
* > `2023/10` <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202310-divvy-tripdata.csv", sep=";")
  >   View(`2023/10`)

Now is to check column structures using str() to inspect the structure of each dataset and verify that the columns are in the same order and have compatible data types across datasets.
After running the function on all data, it appears that each dataset has seven variables (ride_id, rideable_type, started_at, ended_at, member_casual, ride_length, and day_of_week), but the column names might differ in some datasets. For instance, in 2023/08 and 2023/02, there's a typo in the column name day_of_.week and day_of_column compared to the other datasets where it's named day_of_week. This will require us to correct the typo using the command: 
* **colnames(`2023/08`)[colnames(`2023/08`) == "day_of_.week"] <- "day_of_week"** and
* **names(`2023/02`)[names(`2023/02`) == "day_of_column"] <- "day_of_week"** 

Now is to combine and merge all the dataset into one using the command: 
* **combined_data <- rbind(`2022/11`, `2022/12`, `2023/01`, `2023/02`, `2023/03`, `2023/04`, `2023/05`, `2023/06`, `2023/07`, `2023/08`, `2023/09`, `2023/10`)**

![combined-data](https://github.com/YacineQbr/Cyclistic_Bike-Share/assets/103572146/bca0f764-6866-4ec5-b1c3-2170124f1f03)

#### Data Cleaning: 
Ensuing that data is clean and ready for analysis is crucial for several reasons:

* Reliable Insights: Clean data ensures the accuracy and reliability of your analysis. It reduces the chances of errors, ensuring that the conclusions drawn from the data are trustworthy.
* Credibility: Clean data increases the credibility of your findings. Stakeholders, decision-makers, or clients are more likely to trust conclusions drawn from well-maintained, clean data.
* Informed Decision-Making: Clean data leads to accurate insights, aiding in informed decision-making. Organizations can make better strategic decisions based on reliable information.
* Avoiding Biased Results: Dirty data, with inconsistencies, errors, or missing values, can introduce bias into your analysis. Clean data minimizes this risk, providing a more accurate representation.
* Optimized Resource Utilization: Spending time cleaning and preparing data can be resource-intensive. Ensuring data cleanliness upfront saves time and resources in the long run.
* Better Models: Clean data contributes to the accuracy of predictive models. Models trained on clean data tend to perform better and offer more accurate predictions.
* Compliance: In regulated industries, adhering to data cleanliness standards is necessary for compliance with legal and industry-specific regulations.
* Effective Collaboration: Clean data facilitates collaboration among teams. It's easier for multiple stakeholders to understand and work with clean datasets.
* Clear Communication: Clean data simplifies the communication of findings and insights to diverse audiences, ensuring that everyone understands and interprets the results correctly.
* Iterative Process: Regularly cleaning and maintaining data promotes a culture of continuous improvement, enhancing data quality over time.

To achieve that, I will be running couple command and functions on RStudio:

1. Checking Structure and Summary
2. Missing Values
3. Check for Duplicates
4. Data Transformation

Click here to view the R script for these stpes.

### Phase 4: Analyze
















