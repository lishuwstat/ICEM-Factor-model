## R package 'ICTransCFA' version 1.0.3


## Factor Augmented Transformation Models for Interval-Censored Failure Time Data. 

This R package is used to implement a factor-augmented transformation modeling method to analyze interval-censored data with multiple correlated covariates introduced in the paper "Factor Augmented Transformation Models for Interval-Censored Failure Time Data by Li, H., Li, S., Sun, L., and Song, X. (2023+)".

The proposed joint model comprises a confirmatory factor analysis (CFA) model to group multiple observed variables into a few latent factors and a class of semiparametric transformation models to examine the effects of the latent factors and other observed covariates on the failure event.

This R package also contains an example data set.


####  Installation 
To install the ICTransCFA package, one can proceed with the following two steps:

1) Put the ICTransCFA_1.0.3.tar.gz file in the working directory, such as D:\wd.
2) Install the ICTransCFA package by running the following command in R:


# Please note that Rtools is required to install the ICTransCFA package on Windows.

setwd("D:/wd") ## set the working directory

install.packages("ICTransCFA_1.0.3.tar.gz", repos = NULL, type = "source")


#### An example

library(ICTransCFA)

# Use a simulated data set (100 observations and 16 variables) embedded in the INTransCFA package.

data("data_example")

L<-data_example[,1] ## left endpoint of the interval (n by 1) 
R<-data_example[,2] ## right endpoint of the interval (n by 1)
CensorIndMat<-as.matrix(data_example[,3:5]) ## the censoring indicator matrix (n by 3) 
X<-as.matrix(data_example[,6:10]) ## the observed covariate matrix (n by s)
V<-as.matrix(data_example[,11:16]) ## the observed covariate matrix used to form the latent factors
LoadingsInitial = matrix(c(rep(1, 4), rep(0, 6), rep(1,2)), ncol = 2) ## the initial value of the loading matrix in CFA model

# Fit the PH model (r=0) and get the standard error estimates with the profile Fisher score approach.

fit <- JointTransCFAreg(L, R, CensorIndMat, X, V, LoadingsInitial, seeMethod = "Profile", r = 0, ip = 15)
summary(fit)


For more details on the arguments of the package, please see the file "ICTransCFA_1.0.3.pdf".



