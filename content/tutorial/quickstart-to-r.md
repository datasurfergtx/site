---
date: "2018-09-09T00:00:00-04:00"
draft: true
linktitle: Quick Start to Data Analysis in Transportation
menu:
  tutorial:
    parent: Transportation
    weight: 1
title: Example Page
toc: true
type: docs
---

```r
library(tidyverse)
library(data.table)
options(scipen =999)
setwd("/Users/Jacky/Downloads/uber-pickups-in-new-york-city")
# Download link: https://www.kaggle.com/fivethirtyeight/uber-pickups-in-new-york-city/data

uber = read.csv("uber-raw-data-sep14.csv")
str(uber)
sum(is.na(uber))
```

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |


|Date.Time        |Lat     |Lon      |Base   |
|-----------------|--------|---------|-------|
| 9/1/2014 0:01:00| 40.2201| -74.0021| B02512|
| 9/1/2014 0:01:00| 40.7500| -74.0027| B02512|
| 9/1/2014 0:03:00| 40.7559| -73.9864| B02512|
| 9/1/2014 0:06:00| 40.7450| -73.9889| B02512|
| 9/1/2014 0:11:00| 40.8145| -73.9444| B02512|
| 9/1/2014 0:12:00| 40.6735| -73.9918| B02512|


## Datetime

library(tidyverse)
library(data.table)
options(scipen =999)
setwd("C:/Users/lamja/Documents/R/uber-pickups-in-new-york-city")

uber = read.csv("uber-raw-data-sep14.csv")
str(uber)
sum(is.na(uber))
#Date.Time is not in a readable time format for r. Let's convert it.

#I like to use datetime as 2/20/2019 8:15:55PM but my friend from Latvia uses datetime in 20-02-2019 20:15:55, which one is correct?

#r says neither!

#what is the ISO 8601 standard?
#https://en.wikipedia.org/wiki/ISO_8601
#R likes to use POSIXct when working with dates. This follows the ISO 8601 standard.


#NEVER convert factors directly into time. Convert it to a character first.
uber$Date.Time = as.character(uber$Date.Time)
str(uber)
#we need to use strptime
#https://stat.ethz.ch/R-manual/R-devel/library/base/html/strptime.html
uber$Date.Time = strptime(uber$Date.Time, "%m/%d/%Y %H:%M:%S") #fast
parse_date_time(uber$Date.Time, order = 'mdy HMS') #slow but forgiving
uber$Date.Time = as.POSIXct(uber$Date.Time) #fastest! But data needs to be in the format already or it won't work.


## lets play around with the data!

trip_times = as.data.frame(table(uber$Date.Time, uber$Base))
#so this aggregation sucks.

#let's see what the trip volume is per day.

uber1 = uber
uber1$Date.Time = substr(uber1$Date.Time, 1,10)
str(uber1)
#it's a character again.
uber1$Date.Time = strptime(uber1$Date.Time, "%Y-%m-%d")
uber1$Date.Time = as.POSIXct(uber1$Date.Time)
trip_times = as.data.frame(table(uber1$Date.Time,uber1$Base))
table(uber1$Base)

#notice that the bases are in one column, let's reshape this to make it look cleaner
#https://www.rstudio.com/resources/cheatsheets/
trip_times = spread(trip_times, Var2, Freq)

#nice! Let's rename the column, Var1 is not that descriptive, anyway.
colnames(trip_times)[1] <- "Date"

names(trip_times)
graph = gather(trip_times, 'B02512','B02598', 'B02682', 'B02764', 'B02617', key = "Base", value = "Trips")
head(graph)
#let's make sure we have proper datetimes
str(graph)
#we don't! Let's convert this quickly.
graph$Date = as.POSIXct(as.character(graph$Date))
str(graph)

ggplot(graph, aes(x = Date, y = Trips, color = as.factor(Base))) + geom_line()
