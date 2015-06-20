---
tags: ['study-notes', 'analytics-edge']
title: 'The Analytics Edge'
---
[https://www.edx.org/course/analytics-edge-mitx-15-071x-0](https://www.edx.org/course/analytics-edge-mitx-15-071x-0)

## Week 1 - Introduction to analytics

**Variables:**

- rm(WHO_Europe)

**Functions:**

- sqrt(2)
- abs(-65)
- ?sqrt

**Vectors:**

- c(2,3,5,8,13)
- Country = c("Brazil", "China", "India","Switzerland","USA")
- Country[1]

**Data frame:**

- CountryData = data.frame(Country, LifeExpectancy)
- AllCountryData = rbind(CountryData, NewCountryData)
- nrow(Outliers)

**CSV Files:**

- WHO = read.csv("WHO.csv")
- str(WHO)
- write.csv(WHO_Europe, "WHO_Europe.csv")
- Convert dates: IBM$Date = as.Date(IBM$Date, "%m/%d/%y")
- Loading mapping data for fields - CPS = merge(CPS, MetroAreaMap, by.x="MetroAreaCode", by.y="Code", all.x=TRUE). x and y are the two data sets.

** Subsetting: **

- WHO_Europe = subset(WHO, Region == "Europe")
- Outliers = subset(WHO, GNI > 10000 & FertilityRate > 2.5)
- Outliers[c("Country","GNI","FertilityRate")]
- table(WHO$Region)

** Data Analysis: **

- summary(WHO)
- mean(WHO$Under15)
- sd(WHO$Under15)
- which.min(WHO$Under15)
- WHO$Country[86]
- tapply(WHO$Over60, WHO$Region, mean)
- tapply(WHO$LiteracyRate, WHO$Region, min, na.rm=TRUE)
- Investigate if na are related to other variables: table(cps$Region, is.na(cps$Married))
- Using mean to assess proportion of TRUE/FALSE tapply(is.na(cps$MetroAreaCode), cps$State, mean)

** Plots: **

- plot(WHO$GNI, WHO$FertilityRate), plot(CocaCola$Date, CocaCola$StockPrice, type='l', col='red')
- add line to plot: lines(ProcterGamble$Date, ProcterGamble$StockPrice)
- add vertical line: abline(v=as.Date(c("2000-03-01")), lwd=2)
- hist(WHO$CellularSubscribers)
- boxplot(WHO$LifeExpectancy ~ WHO$Region, xlab = "", ylab = "Life Expectancy", main = "Life Expectancy of Countries by Region")
