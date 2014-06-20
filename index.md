---
title       : Alzheimer Disease Prediction
subtitle    : based on the versions of the Apolipoprotein E gene
author      : 
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

---

## Introduction
This application aims to provide a simplified way of predicting Alzheimer's disease based on the versions of the Apolipoprotein E gene inherited from one's parents. The data set comes from 'AppliedPredictiveModeling' R package [1].

## Building a Model

```r
library(shiny)
library(caret)
library(e1071)
library(AppliedPredictiveModeling)
data(AlzheimerDisease)
set.seed("12345")
df = data.frame(diagnosis = diagnosis,Genotype = predictors[,"Genotype"])
inTrain = createDataPartition(df$diagnosis, p = 0.8)[[1]]
training = df[ inTrain,]
testing = df[-inTrain,]
modelFit<-train(diagnosis ~ Genotype, data = training, method = "glm")
```

---

## Model Summary 

```
## Generalized Linear Model 
## 
## 267 samples
##   1 predictors
##   2 classes: 'Impaired', 'Control' 
## 
## No pre-processing
## Resampling: Bootstrapped (25 reps) 
## 
## Summary of sample sizes: 267, 267, 267, 267, 267, 267, ... 
## 
## Resampling results
## 
##   Accuracy  Kappa  Accuracy SD  Kappa SD
##   0.7       0.05   0.03         0.05    
## 
## 
```

---

## Model Testing

```r
predict1 <- predict(modelFit, testing)
table(testing$diagnosis, predict1)
```

```
##           predict1
##            Impaired Control
##   Impaired        4      14
##   Control         4      44
```

---

## Using the Application 

This application is easy to use.  It provides an instant prediction based on selected Genotype.

To see the application in action, please complete the following steps:
* Go to https://natashadrozdova.shinyapps.io/Project/
* Select a predictor called Genotype from the dropdown box at the left side of the screen.
* Click Submit button to see the result in the gray box at the right side of the screen.




#### References 

1. Max Kuhn, Kjell Johnson, Package 'AppliedPredictiveModeling', http://cran.r-project.org/web/packages/AppliedPredictiveModeling/AppliedPredictiveModeling.pdf (February 3, 2014)





