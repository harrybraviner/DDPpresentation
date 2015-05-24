---
title       : Car Fuel Efficiency Predictor
subtitle    : Helping car designers predict before they build
author      : Harry Braviner
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## The Motivation

* Building a car is expensive.
* Designers would like to be able to predict the fuel efficiency of a car before building a prototype.
* Customers would like a prediction of fuel efficiency if no measurement is available.

There is a wide range of fuel efficencies in our dataset:

```r
data(mtcars)
summary(mtcars$mpg)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   10.40   15.42   19.20   20.09   22.80   33.90
```

--- .class #id 

## The Data


We will use the `mtcars` dataset to build our model.

### Pros

* The `mtcars` dataset is available in standard R installations and contains data for 32 cars.
* It contains data on fuel efficiency, weight, and number of gears (amongst other variables) for each car.

### Cons

* It is from 1974.
* I wasn't born in 1974.

--- .

## The Model

We will build a linear regression model predicting mpg from weight, conditioned on the number of gears the car has.
To illustrate why this conditioning matters, observe the differing coefficients in the following two linear models:

```r
carsG3 <- mtcars[mtcars$gear == 3,]; carsG4 <- mtcars[mtcars$gear == 4,]
LM3 <- lm(mpg ~ wt, data = carsG3); LM4 <- lm(mpg ~ wt, data = carsG4)
LM3$coefficients
```

```
## (Intercept)          wt 
##   28.395036   -3.156854
```

```r
LM4$coefficients
```

```
## (Intercept)          wt 
##   42.492769   -6.863478
```

--- .

## The App

* We build the app using the R package *shiny*, and deployed it at [http://harrybraviner.shinyapps.io/project/](http://harrybraviner.shinyapps.io/project/).
* The app provides a graphical display of the linear model to help the user assess whether the predictor is badly out of sample.

![Screengrab of the app](assets/img/appProject.png)

* The app has been tested in the Chromium browser, including a mobile version.
