# Cyclistic_Bike-Share
A Case Study on how does a Bike-Share navigate speedy success:

This Case Study has been created as an essential component of the Google Data Analytics Professional Certificate Capstone.

## Senario and Projet Overview 
Cyclistic is a bike-share company in Chicago that was luanched in 2016. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. 
The director of marketing Lily Moreno, believes that the companys's future success depends on maximizing the number of memberships. Therefore, This data analysis aims to offer comprehensive insights into the distinct usage patterns of Cyclistic Bikes, encompassing both casual passengers and annual subscribers. Through a meticulous examination of various facets of the data, this analysis endeavors to discern prevalent trends, formulate data-driven recommendations, and deisgn a new markeing stratgey to convert casual passengers into annual subscribers. 

The project will follow the six phases of data analysis which includes: **Ask**, **Prepare**, **Process**, **Analyze**, **Share** and **Act**. 

## Phase 1: Ask 
There are couple questions that can guide the future marketing program and help the team achieve the needed results which are: 

1. How do annual members and casual riders use Cyclistic bikes differently?
2. why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

The director Moreno has assigned me the first question to answer which is: **How do annual members and casual riders use Cyclistic bikes differently ?**

### Key Tasks 
**1. The business task**

The task of this analysis is to pinpoint essential factors and detect patterns in Cyclistic Bike-Share usage among two user groups: casual riders and annual subscribers. This understanding will enable the company to enhance its profit share by developing a new marketing plan focused on converting casual riders into annual subscribers.

**2. Stakeholders**

Main stakeholder: 
* **Lily Moreno**: Team Manager, Marketing director
  
Subsidiary stakeholders: 
* **Marketing analytics team**
* **Executive team**

## Phase 2: Prepare

**1. Data Sources**
In this project, we will be using a public historical trip data provided by the company itself has been made available by Motivate International Inc. under this [licence](https://divvybikes.com/data-license-agreement). The data has been made available by Motivate International Inc. The statistics are orgnized as long data in CSV files  which gives information from 2013 to 2023, and it was retreived from [Data](https://divvy-tripdata.s3.amazonaws.com/index.html) and it has been safely stored in a local drive. 
The data is a good fit for this analysis as it accomplish the required conditions for the credibility and fullfill the ROCCC approach: **Reliable**, **Original**, **Comprehensive**, **Current** and **Cited**.

**2. Sort and filter the data**

For this examination I am going to focus on the period between November 2022 and October 2023 as it is the more recent and relevant period of the business task. 

## Phase 3: Process

In this phase, we will clean the data and make it free of errors or mistake which could affect the credibility or the conclusions. To achieve this gool, we will be using couple tools which will be cited as follow. 

**1. Tools**
* **Excel:** Data cleaning
* **RStudio:** Data Cleaning, analysis and visualization

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
  
## Phase 4: Analyze

There were over 5 million records, making the use of spreadsheets impractical for data cleaning. Faced with two choices, SQL and R, I was a little familir with both of them. Given my penchant for learning new programming languages as a new Data Analyst, I saw this as a valuable chance to acquire R skills. Consequently, I opted for R.

### **1.1. RStudio:** 

As part of the preparation of data, the following is done:

* the various datasets are imported to R
* the structure of the datasets are analyzed to ensure consistency

First I added all the packages and libraries necessary for my analysis: 

```install.packages("tidyverse")
install.packages("lubridate")
install.packages("ggplot2")
install.packages("dplyr")
install.packages("tidyr")
install.packages("readr")
install.packages("tibble")
install.packages("stringr")
install.packages("forcats")
install.packages("readxl")
```

```library(tidyverse)
library(lubridate)
library(ggplot2)
library(dplyr)
library(tidyr)
library(readr)
library(tibble)
library(stringr)
library(forcats)
library(readxl)
```

Then I donwloded the required packages needed for this libraries and analysis.

Later, using **<-read.cvs** to load the 12 datasets for the 12 months from November 2022 untill October 2023 of my analysis and combine them into a single dataset. While pulling the dataset, I renamed each file to this format data_YYYY_MM.

#Import data 

```data_2022_11 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202211-divvy-tripdata.csv") View(data_2022_11)
data_2022_12 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202212-divvy-tripdata.csv") View(data_2022_12)
data_2023_01 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202301-divvy-tripdata.csv") View(data_2023_01)
data_2023_02 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202302-divvy-tripdata.csv") View(data_2023_02)
data_2023_03 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202303-divvy-tripdata.csv") View(data_2023_03)
data_2023_04 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202304-divvy-tripdata.csv") View(data_2023_04)
data_2023_05 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202305-divvy-tripdata.csv") View(data_2023_05)
data_2023_06 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202306-divvy-tripdata.csv") View(data_2023_06)
data_2023_07 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202307-divvy-tripdata.csv") View(data_2023_07)
data_2023_08 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202308-divvy-tripdata.csv") View(data_2023_08)
data_2023_09 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202309-divvy-tripdata.csv") View(data_2023_09)
data_2023_10 <- read.csv("~/Desktop/Cyclistic data.CSV/edited CSV/202310-divvy-tripdata.csv") View(data_2023_10)
```

Now is to check column structures using str() to inspect the structure of each dataset and verify that the columns are in the same order and have compatible data types across datasets.
After running the function on all data, it appears that each dataset has seven variables (ride_id, rideable_type, started_at, ended_at, member_casual, ride_length, and day_of_week), but the column names might differ in some datasets. For instance, in 2023/08 and 2023/02, there's a typo in the column name day_of_.week and day_of_column compared to the other datasets where it's named day_of_week. This will require us to correct the typo using the command: 

```
colnames(`2023/08`)[colnames(`2023/08`) == "day_of_.week"] <- "day_of_week" 
colnames(`2023/02`)[names(`2023/02`) == "day_of_column"] <- "day_of_week"
```

Now is to combine and merge all the dataset into one using the command: 
```
Cyclistic_data <- rbind(`2022/11`,`2022/12`,`2023/01`,`2023/02`,`2023/03`,`2023/04`,`2023/05`,`2023/06`,`2023/07`,`2023/08`,`2023/09`,`2023/10`)

```
![Merged_data](https://github.com/YacineQbr/Cyclistic_Bike-Share/assets/103572146/d093372b-6cc5-4127-ba29-8e6e74f176ee)


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

##### 1. Checking Structure and Summary

```Structure for data_2022_11 :
# List of all dataset variables
data_variables <- c("data_2022_11", "data_2022_12", "data_2023_01", "data_2023_02", "data_2023_03",
                    "data_2023_04", "data_2023_05", "data_2023_06", "data_2023_07", "data_2023_08",
                    "data_2023_09", "data_2023_10")

# Loop to display column names for each dataset
for (data_var in data_variables) {
  cat("Column names for", data_var, ":\n")
  print(colnames(get(data_var)))
  cat("\n")
}
# Result: 
Column names for 2022/11 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2022/12 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/01 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/02 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/03 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/04 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/05 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/06 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/07 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/08 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/09 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  

Column names for 2023/10 :
[1] "X"             "ride_id"       "rideable_type" "started_at"    "ended_at"      "member_casual"
[7] "ride_length"   "day_of_week"  
```
#### 2. Missing Values

There are many options to check for missing values using functions like is.na() or summarise().
```
> # Count missing values in each column
> missing_count <- colSums(is.na(combined_data))
> missing_count
            X       ride_id rideable_type    started_at      ended_at member_casual   ride_length 
            0             0             0             0             0             0             0 
  day_of_week 
            0

# Check for empty cells (assuming empty cells are represented as "")
any(Cyclistic_data == "")
[1] FALSE
# Overall summary of data
summary(Cyclistic_data)
       X            ride_id          rideable_type       started_at          ended_at        
 Min.   :     1   Length:5144068     Length:5144068     Length:5144068     Length:5144068    
 1st Qu.:127524   Class :character   Class :character   Class :character   Class :character  
 Median :274547   Mode  :character   Mode  :character   Mode  :character   Mode  :character  
 Mean   :303499                                                                              
 3rd Qu.:463542                                                                              
 Max.   :771693                                                                              
 member_casual      ride_length         day_of_week   
 Length:5144068     Length:5144068     Min.   :0.000  
 Class :character   Class :character   1st Qu.:2.000  
 Mode  :character   Mode  :character   Median :4.000  
                                       Mean   :3.681  
                                       3rd Qu.:5.000  
                                       Max.   :7.000  
```
It appears that there is no missing values.

#### 3. Check for Duplicates
```
Cyclistic_data<- distinct(Cyclistic_data, .keep_all = TRUE)
```

#### 4. Identify trends and relationships:

The data is now clean and orgnized for further analysis, this will help the project to identify the behaviouor differences between annual members and casual riders. We will start conducting some calculations:

First, I created another column to convert the format HH:MM:SS in the ride_length column to a total seconds: 

```
#  'Cyclistic_data' has a column named 'ride_length' in "hh:mm:ss" format
combined_data$ride_length_seconds <- as.numeric(
  difftime(
    as.POSIXct(Cyclistic_data$ride_length, format = "%H:%M:%S"),
    as.POSIXct("00:00:00", format = "%H:%M:%S"),
    units = "secs"
  )
)
```

```
Cyclistic_data %>%
 summarise(
    mean_value = mean(ride_length, na.rm = TRUE),
    max_value = max(ride_length, na.rm = TRUE),
    min_value = min(ride_length, na.rm = TRUE),
    median_value = median(ride_length, na.rm = TRUE)
    )
  mean_value  max_value min_value median_value
1    1927533 9988946759 -34398148         1133
```

* **Creating pivot tables to quickly calculate and visualize the data:**
* Calculating the average ride_length for members and casual riders. Try rows = member_casual; Values = Average of ride_length.
* Calculating the average ride_length for users by day_of_week. Try columns = day_of_week; Rows = member_casual; Values = Average of ride_length.
* Calculating the number of rides for users by day_of_week by adding Count of trip_id to Values.

```
# Calculate the average ride_length for members and casual riders:      
     pivot_table <- Cyclistic_data %>%
       group_by(member_casual) %>%
       summarise(average_ride_length_seconds = mean(ride_length_seconds, na.rm = TRUE)) %>%
       mutate(average_ride_length_HMS = format(as.POSIXct(average_ride_length_seconds, origin = "1970-01-01"), format = "%H:%M:%S"))
     
View(pivot_table)
 # Display the pivot_table as markdown
  knitr::kable(pivot_table, format = "markdown")

| member_casual | average_ride_length_seconds | average_ride_length_HMS |
|---------------|-----------------------------|-------------------------|
| casual        | 1285.1855                   | 00:21:25                |
| member        | 730.0165                    | 00:12:10                |

  ggplot(pivot_table, aes(x = member_casual, y = average_ride_length_seconds, fill = member_casual)) +
    geom_bar(stat = "identity", position = "dodge") +
    labs(x = "Member Type", y = "Average Ride Length (Seconds)", title = "Average Ride Length by Member Type")
```

![image](https://github.com/YacineQbr/Cyclistic_Bike-Share/assets/103572146/e87f1e14-b18b-4213-b924-0c44b36054f4)


```# Calculate the average ride_lenght for users by day_of_week:
     
    pivot_table_2 <- combined_data %>%
    filter(day_of_week != 0) %>%
    group_by(member_casual, day_of_week) %>%
    summarise(average_ride_length_seconds = mean(ride_length_seconds, na.rm = TRUE)) %>%
    pivot_wider(names_from = member_casual, values_from = average_ride_length_seconds)
  
  pivot_table_2
  # Display the pivot_table_2 as markdown
  knitr::kable(pivot_table_2, format = "markdown")

| day_of_week|   casual|   member|
|-----------:|--------:|--------:|
|           1| 1427.262| 739.6665|
|           2| 1216.064| 703.6435|
|           3| 1130.007| 699.1341|
|           4| 1100.911| 693.9273|
|           5| 1150.257| 702.5000|
|           6| 1308.412| 761.3343|
|           7| 1494.176| 861.3595|

 # Creating a data frame from the table data
ride_length_data <- data.frame(
  day_of_week = 1:7,
  casual = c(1427.262, 1216.064, 1130.007, 1100.911, 1150.257, 1308.412, 1494.176),
  member = c(739.6665, 703.6435, 699.1341, 693.9273, 702.5, 761.3343, 861.3595)
)


library(tidyr)

ride_data_long <- pivot_longer(ride_length_data, cols = c(casual, member),
                               names_to = "Type", values_to = "Average_Ride_Length")



library(ggplot2)

ggplot(ride_data_long, aes(x = factor(day_of_week), y = Average_Ride_Length, fill = Type)) +
  geom_bar(position = "dodge", stat = "identity", alpha = 0.7) +
  labs(x = "Day of the Week", y = "Average Ride Length", title = "Average Ride Length for Casual and Member by Day of the Week") +
  scale_x_discrete(labels = c("1" = "Mon", "2" = "Tue", "3" = "Wed", "4" = "Thu", "5" = "Fri", "6" = "Sat", "7" = "Sun")) +
  theme_minimal()
 ```
![image](https://github.com/YacineQbr/Cyclistic_Bike-Share/assets/103572146/db369659-3f3b-4730-9d7a-b40adcf93c76)


```# Calculate the number of rides for users by day_of_week by adding Count of trip_id to values: 
     
     pivot_table_3 <- combined_data %>%
       group_by(member_casual, day_of_week) %>%
       summarise(ride_count = n()) %>%
       pivot_wider(names_from = day_of_week, values_from = ride_count)
     
     print(pivot_table_3)
     view(pivot_table_3)
  
  # Display the pivot_table_3 as markdown
  knitr::kable(pivot_table_3, format = "markdown")

| member_casual | 1      | 2      | 3      | 4      | 5      | 6      | 7      |
|---------------|--------|--------|--------|--------|--------|--------|--------|
| casual        | 277613 | 233330 | 226487 | 225057 | 248913 | 314638 | 264252 |
| member        | 408912 | 489298 | 501026 | 490356 | 479523 | 437803 | 250611 |

 

library(ggplot2)
library(scales)

# Data: 
ride_counts <- data.frame(
  member_casual = c("casual", "member"),
  `1` = c(277613, 408912),
  `2` = c(233330, 489298),
  `3` = c(226487, 501026),
  `4` = c(225057, 490356),
  `5` = c(248913, 479523),
  `6` = c(314638, 437803),
  `7` = c(264252, 250611)
)

# Reshape the data to longer format
ride_counts_long <- tidyr::pivot_longer(ride_counts, cols = -member_casual, names_to = "day_of_week", values_to = "ride_count")

# Plotting the bar chart with formatted Y-axis
ggplot(ride_counts_long, aes(x = factor(day_of_week), y = ride_count, fill = member_casual)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(x = "Day of the Week", y = "Count of Rides", title = "Number of Rides for Users by Day of Week") +
  scale_fill_manual(values = c("casual" = "skyblue", "member" = "pink"), name = "User Type") +
  scale_y_continuous(labels = comma) +  # Formatting the Y-axis with commas
  theme_minimal()

```
![image](https://github.com/YacineQbr/Cyclistic_Bike-Share/assets/103572146/7d3bf986-d667-4488-8cc6-3b5efb24d061)


### Analysis results and insights:
From the provided bar chartes and pivot tables, it's possible to extract several insights and observe differences in behavior between casual and member riders:

1. Average Ride Length:
   
Casual riders tend to have longer average ride lengths compared to members. The average ride length for casual riders ranges from around 21 to 23 minutes, while for members, it's between 12 to 14 minutes.

2. Ride Length by Day of the Week:
   
Both casual and member riders show fluctuation in ride lengths across the days of the week.
Casual riders seem to have slightly longer rides during weekdays, with a peak on days 1 and 7 (assuming day 1 is Sunday).
Member riders show a more consistent ride length pattern across the week, with shorter rides compared to casual riders.

3.Ride Count by Day of the Week:

Casual riders show higher ride counts during weekdays, with a notable decrease on day 7.
Member riders generally maintain a consistent number of rides across the week, with a slight decrease on day 7.

4. Behavior Patterns:

Casual riders might prefer longer rides, potentially using the service for leisure or longer commutes.
Member riders seem to utilize the service for shorter and possibly more routine trips, maintaining a consistent pattern both in ride length and ride count.

These insights suggest that casual riders tend to have longer rides and more variable ride counts across days, potentially using the service for leisure or occasional transportation. On the other hand, member riders show a more consistent pattern in both ride length and ride count, indicating a more routine usage, possibly for regular commuting or specific purposes. These observations could guide strategies for targeting different user groups, adjusting service offerings, or tailoring marketing efforts to attract and retain both casual and member riders

### Phase 5: Share 


















