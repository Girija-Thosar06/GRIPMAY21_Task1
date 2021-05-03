---
title: "GRIPMAY21_TASK1"
output: 
  html_document:
    keep_md: true
---



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:
* * *

GRIPMAY21 : TASK1 : Prediction using supervised ML

BY GIRIJA THOSAR

* * *


```r
# loading the libraries
library(ggplot2)
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(statsr)
```

```
## Loading required package: BayesFactor
```

```
## Loading required package: coda
```

```
## Loading required package: Matrix
```

```
## ************
## Welcome to BayesFactor 0.9.12-4.2. If you have questions, please contact Richard Morey (richarddmorey@gmail.com).
## 
## Type BFManual() to open the manual.
## ************
```


```r
# loading the dataset from the url provided
data = read.csv(url("http://bit.ly/w-data"))
```


Now lets check the dataset



```r
head(data)
```

```
##   Hours Scores
## 1   2.5     21
## 2   5.1     47
## 3   3.2     27
## 4   8.5     75
## 5   3.5     30
## 6   1.5     20
```

Using 'geom_point' function to create the scatter plot of the response variable (scores) and the explanatory variable (hours)


```r
ggplot(data = data, aes(x = Hours, y = Scores)) +
  geom_point()
```

![](GRIPMAY21_TASK1_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

From the graph we can see that there is a linear relationship between the response variable and explanatory variable. Also the direction of association seems positive.




```r
# Checking the correlation between the two variables.
cor(data$Scores,data$Hours)
```

```
## [1] 0.9761907
```


We see a highly positive correlation between scores and hours.



```r
# Writing the model where Scores (response variable) is a function of Hours (explanatory variable)
model = lm(Scores ~ Hours, data = data)
summary(model)
```

```
## 
## Call:
## lm(formula = Scores ~ Hours, data = data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -10.578  -5.340   1.839   4.593   7.265 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   2.4837     2.5317   0.981    0.337    
## Hours         9.7758     0.4529  21.583   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.603 on 23 degrees of freedom
## Multiple R-squared:  0.9529,	Adjusted R-squared:  0.9509 
## F-statistic: 465.8 on 1 and 23 DF,  p-value: < 2.2e-16
```


The model can be interpreted as :
Predicted Scores = 9.7758 * Hours + 2.4837.
Here $R^2$ = 0.9529. It is the strength of the fit of a linear model.



```r
# adding the regression line
plot(data$Hours,data$Scores)
abline(model)
```

![](GRIPMAY21_TASK1_files/figure-html/unnamed-chunk-7-1.png)<!-- -->



Checking actual score values of top 3 observations


```r
head(data,n=3)
```

```
##   Hours Scores
## 1   2.5     21
## 2   5.1     47
## 3   3.2     27
```


Now checking the predicted scores for the above mentioned observations


```r
test1 = data.frame(Hours = c(2.5,5.1,3.2))

predict(model, test1)
```

```
##        1        2        3 
## 26.92318 52.34027 33.76624
```

Now when the hours = 9.25, what is the predicted score

```r
# Now when the hours = 9.25, what is the predicted score
test2 = data.frame(Hours = 9.25)

predict(model, test2)
```

```
##        1 
## 92.90985
```
SO the predicted score is 92.90











