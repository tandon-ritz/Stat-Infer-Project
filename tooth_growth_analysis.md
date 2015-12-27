---
title: "Impact of different supplement types and vitamin C dose levels on tooth lengths"
author: "Ritesh Tandon"
date: "December 27, 2015"
output: pdf_document
---



## Overiew

In this report we will analyze the TootGrowth data of the R data set package which describes the effect of different doses of vitamin C supplement on tooth growth.

The ToothGrowth data set consists of 60 observations of 3 variables:

* len: Tooth length in millimeters (numeric variable)
* supp: Supplement type (factor variable with levels VC and OJ)
* dose: Dose in milligrams (numeric variable)


## Exploratory data analysis


The average tooth length is 18.8133333 and standard deviation of 7.6493152.

Following graph shows the effect in tooth length depending on different doses for both the types of supplement ( OJ and VC ).


<img src="figure/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />


## Hypothesis tests


We want to statistically prove that different supplement ( OJ or VC ) or different doses ( 0.5, 1.0, 2.0 ) or combination of both effects tooth growth. Our null hypothesis is that there is no effect on tooth growth even after giving supplement/doses. We either has to accept or reject this null hypothesis by statistical evidence.

Although the total number of observation in datasets is 60 but it is less than 30 within each group ( supplement or doses ) , hence we will perform t test on the data.

### Differences in supplement types

We will verify if the difference in tooth length means between pigs who received their dose using OJ and those who received their dose via VC is statistically different from 0.



```
##   estimate estimate1 estimate2 statistic    p.value parameter   conf.low
## 1      3.7  20.66333  16.96333  1.915268 0.06063451  55.30943 -0.1710156
##   conf.high
## 1  7.571016
```

We notice that p value is 0.06 which is greater than significant value 0.05 , indicating that based on given data we are not 95% confident that supplement effect the tooth growth. 

Also, 95% t confidence interval is between -0.1710156 and 7.571016 that contains 0 in the range.This, we are not sure if supplement effect the tooth growth. Hence, we can not reject our null hypothesis.

### Differences in dose levels

There are three different types of doses ( 2, 1 and 0.5 ) given to the subjects in order to study its impact on tooth length. We will do group by comparison between these doses and perform t test between the groups in order to analyze its impact on tooth length


1. comparison of Impact on tooth length betwenn dose 2 and 1


```
##   estimate estimate1 estimate2 statistic     p.value parameter conf.low
## 1    6.365      26.1    19.735  4.900484 1.90643e-05  37.10109 3.733519
##   conf.high
## 1  8.996481
```


We notice that p-value ( 1.9e-05 ) is much smaller than significant level (0.05) for us to be 95% confident.Also, 0 does not lie between t interval ( 3.73 to 8.99 ) Hence, we reject null hypothesis.

This means that we are 95% confident that the average tooth length of pigs who received a 2mg dose is on average 3.73 to 9 millimeters higher than those who received a 1mg dose.

2. comparison of Impact on tooth length betwenn dose 2 and 0.5


```
##   estimate estimate1 estimate2 statistic      p.value parameter conf.low
## 1   15.495      26.1    10.605  11.79905 4.397525e-14  36.88259 12.83383
##   conf.high
## 1  18.15617
```

We notice that p-value ( 4.3e-14 ) is much smaller than significant level (0.05) for us to be 95% confident.Also, 0 does not lie between t interval ( 12.83 to 18.15 ) Hence, we reject null hypothesis. 


This means that we are 95% confident that the average tooth length of pigs who received a 2mg dose is on average 12.83 to 18.16 millimeters higher than those who received a 0.5 mg dose.

3. comparison of Impact on tooth length betwenn dose 1 and 0.5


```
##   estimate estimate1 estimate2 statistic      p.value parameter conf.low
## 1     9.13    19.735    10.605  6.476648 1.268301e-07  37.98641 6.276219
##   conf.high
## 1  11.98378
```


We notice that p-value ( 1.26e-07 ) is smaller than significant level (0.05) for us to be 95% confident.Also, 0 does not lie between t interval ( 6.27 to 11.98 ) Hence, we reject null hypothesis. 


This means that we are 95% confident that the average tooth length of pigs who received a 1mg dose is on average 6.28 to 11.98 millimeters higher than those who received a 0.5 mg dose.


# Conclusions

1. There is no impact on tooth length mean across supplement types.

2. dose level does impact the tooth length mean 



## Appendix (Source Code)

Following source code which was used for generating the results of the analysis. 
Complete source code and pdf files are also avilable on [GitHub](https://github.com/tandon-ritz/Stat-Infer-Project).


```r
library(ggplot2)
library(dplyr)
library(broom)
library(wesanderson)
library(grid)


# Exploratory Graph

require(graphics)
coplot(len ~ dose | supp, data = ToothGrowth, panel = panel.smooth,
       xlab = "ToothGrowth data: length vs dose, given type of supplement")




# T-test for difference in tooth length means across supplement types

t_test_supp <- t.test(len ~ supp, ToothGrowth, var.equal = FALSE)
t_test_supp<-tidy(t_test_supp)
t_test_supp

# t-tests for differences in tooth lengths means across dose 


# between doses 2 and 1

t_test_dose_2_and_1 <- t.test(ToothGrowth$len[ToothGrowth$dose == 2],
                           ToothGrowth$len[ToothGrowth$dose == 1])
t_test_dose_2_and_1<-tidy(t_test_dose_2_and_1)
t_test_dose_2_and_1


# between doses 2 and 0.5
  
t_test_dose_2_and_0.5 <- t.test(ToothGrowth$len[ToothGrowth$dose == 2],
                           ToothGrowth$len[ToothGrowth$dose == 0.5])
t_test_dose_2_and_0.5<-tidy(t_test_dose_2_and_0.5)
t_test_dose_2_and_0.5


# between doses 1 and 0.5

t_test_dose_1_and_0.5 <- t.test(ToothGrowth$len[ToothGrowth$dose == 1],
                           ToothGrowth$len[ToothGrowth$dose == 0.5])
t_test_dose_1_and_0.5<-tidy(t_test_dose_1_and_0.5)
t_test_dose_1_and_0.5
```

