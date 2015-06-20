---
tags: ['study-notes', 'analytics-edge']
title: 'The Analytics Edge'
---
[https://www.edx.org/course/analytics-edge-mitx-15-071x-0](https://www.edx.org/course/analytics-edge-mitx-15-071x-0)

## Week 2 - Linear Regression

**Linear Regerssion:**

- model = lm(Price ~ AGST + HarvestRain, data=wine)
- Baseline prediction - a simple line of y=avg
- SST - square errors of the baseline
- SSE - square errors of the model - sum(model1.$residuals^2)
- RMSE - root of square errors = sqrt(SSE/nrow(NBA))
-
- R^2 = 1-(SSE/SST)
- Generate a new model that removes variables that don't add to R^2 = step(model)
- Refer to all variables using: lmScore = lm(readingScore ~ ., data = pisa)

**Correlation:**

- cor(wine$WinterRain, wine$Price) - how are two variables correlated? 0 <- no relation. -> 1/-1 - correlated
- remove any variables less than -0.7 or more than 0.7

**Test data:**

- predictTest = predict(model,  newdata=wineTest)
- SSE = sum((wineTest$Price - predictTest) ^ 2)
- SST = sum((wineTest$Price - mean(wine$Price))^2)
- out of sample R2 = 1 - SSE/SST
- SSE = sum((PointsPredicted - NBA_test$PTS)^2)
- SST = sum((mean(NBA$PTS) - NBA_test$PTS)^2)
- RMSE = sqrt(SSE / nrow(NBA_test))

**Other topics:**

- Factor variables. Set reference variable:
- pisaTrain$raceeth = relevel(pisaTrain$raceeth, "White")
- If there is a right skew (histogram shows most values are on the left and a long tail on the right) - using log might help with predictions.
