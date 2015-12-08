# PML Assignment Report
David A York  
November 7, 2015  

## Executive Summary
This project assignment studies a model to control for the effect of proper activity teqhnique by constructing a model to predict the occurence deviation from technique. The data to be use to construct a prediction model is from the [Human Activity Recognition](http://groupware.les.inf.puc-rio.br/har). Selected analysis focuses on use of data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants.




## Model Requirements (Purpose)
Devices such as Jawbone Up, Nike FuelBand, and Fitbit are able to collect a large amount of data about personal activity (of individual whereing the devices) as part of the quantified self movement (QSM). 

People in the QSM regularly quantify how much of a particular activity they do, but they rarely quantify how well they do it. The effectiveness of such activities is assumed to be related to carrying it out with proper technique.

Data was collected from accelerometers on the belt, forearm, arm, and dumbell of 6 participants asked to perform barbell lifts correctly and incorrectly in 5 different ways. Using this data, a model is build to detect improper activity teqhnique in Human Activity Recognition (HAR) data by constructing a prediction model for the occurence of deviation from correct activity technique. 

## Data Cleaning 
The data to be used to construct the prediction model is from the [Human Activity  Recognition](http://groupware.les.inf.puc-rio.br/har). This was downloaded in edited form from a location specifically for this assignment (see Appendix II Assignment Criteria as set out by instructors, Leek et al.) Selected analysis focuses on use of data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. It should be noted that this subset of the datasets has missing data in the var_accel_ data for each body part.

## Data Exploration
See the structure on the training data selected for the model in Appendix Table 1.
See the paires plot in Appendix Figure 1

## Model Building


```
## Random Forest 
## 
## 19622 samples
##    52 predictor
##     5 classes: 'A', 'B', 'C', 'D', 'E' 
## 
## No pre-processing
## Resampling: Bootstrapped (25 reps) 
## Summary of sample sizes: 19622, 19622, 19622, 19622, 19622, 19622, ... 
## Resampling results across tuning parameters:
## 
##   mtry  Accuracy   Kappa      Accuracy SD  Kappa SD   
##    2    0.9926404  0.9906869  0.001358708  0.001717550
##   27    0.9924201  0.9904081  0.001082374  0.001370812
##   52    0.9854942  0.9816434  0.003023064  0.003825377
## 
## Accuracy was used to select the optimal model using  the largest value.
## The final value used for the model was mtry = 2.
```

![](PML_Assignment_Report_files/figure-html/model-1.png) 

## Model Validation
Model validation is inherent in the resampling of the train() function. The validity is determine through the metric(s) chosen to drive the resampling with the accuracy and error rate visualized below from the confusion matrix and the means of the resampling accuracy and kappa.  


### Expected Error
Predicting on the test data based on the model (without NAs)

```r
modelfit52
```

```
## Random Forest 
## 
## 19622 samples
##    52 predictor
##     5 classes: 'A', 'B', 'C', 'D', 'E' 
## 
## No pre-processing
## Resampling: Bootstrapped (25 reps) 
## Summary of sample sizes: 19622, 19622, 19622, 19622, 19622, 19622, ... 
## Resampling results across tuning parameters:
## 
##   mtry  Accuracy   Kappa      Accuracy SD  Kappa SD   
##    2    0.9926404  0.9906869  0.001358708  0.001717550
##   27    0.9924201  0.9904081  0.001082374  0.001370812
##   52    0.9854942  0.9816434  0.003023064  0.003825377
## 
## Accuracy was used to select the optimal model using  the largest value.
## The final value used for the model was mtry = 2.
```

```r
modelfit52$finalModel
```

```
## 
## Call:
##  randomForest(x = x, y = y, mtry = param$mtry) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 2
## 
##         OOB estimate of  error rate: 0.4%
## Confusion matrix:
##      A    B    C    D    E  class.error
## A 5577    2    0    0    1 0.0005376344
## B   11 3784    2    0    0 0.0034237556
## C    0   16 3404    2    0 0.0052600818
## D    0    0   39 3175    2 0.0127487562
## E    0    0    0    4 3603 0.0011089548
```

### Error Estimation

```
## [1] 0.7359601
```
From the confusion matrix it can be seen that 0.1% of B and C and 0.3% of D were miss-classified so the error rate is 0.7359601


## Appendices
### Apendix I: Report Figures

**Table 1 The Structure of Actual Training Data for the Model**

```
## 'data.frame':	19622 obs. of  60 variables:
##  $ X                   : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ user_name           : Factor w/ 6 levels "adelmo","carlitos",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ raw_timestamp_part_1: int  1323084231 1323084231 1323084231 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 ...
##  $ raw_timestamp_part_2: int  788290 808298 820366 120339 196328 304277 368296 440390 484323 484434 ...
##  $ cvtd_timestamp      : POSIXlt, format: "2011-12-05 11:23:00" "2011-12-05 11:23:00" ...
##  $ new_window          : Factor w/ 2 levels "no","yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ num_window          : num  11 11 11 12 12 12 12 12 12 12 ...
##  $ roll_belt           : num  1.41 1.41 1.42 1.48 1.48 1.45 1.42 1.42 1.43 1.45 ...
##  $ pitch_belt          : num  8.07 8.07 8.07 8.05 8.07 8.06 8.09 8.13 8.16 8.17 ...
##  $ yaw_belt            : num  -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 ...
##  $ total_accel_belt    : num  3 3 3 3 3 3 3 3 3 3 ...
##  $ gyros_belt_x        : num  0 0.02 0 0.02 0.02 0.02 0.02 0.02 0.02 0.03 ...
##  $ gyros_belt_y        : num  0 0 0 0 0.02 0 0 0 0 0 ...
##  $ gyros_belt_z        : num  -0.02 -0.02 -0.02 -0.03 -0.02 -0.02 -0.02 -0.02 -0.02 0 ...
##  $ accel_belt_x        : num  -21 -22 -20 -22 -21 -21 -22 -22 -20 -21 ...
##  $ accel_belt_y        : num  4 4 5 3 2 4 3 4 2 4 ...
##  $ accel_belt_z        : num  22 22 23 21 24 21 21 21 24 22 ...
##  $ magnet_belt_x       : num  -3 -7 -2 -6 -6 0 -4 -2 1 -3 ...
##  $ magnet_belt_y       : num  599 608 600 604 600 603 599 603 602 609 ...
##  $ magnet_belt_z       : num  -313 -311 -305 -310 -302 -312 -311 -313 -312 -308 ...
##  $ roll_arm            : num  -128 -128 -128 -128 -128 -128 -128 -128 -128 -128 ...
##  $ pitch_arm           : num  22.5 22.5 22.5 22.1 22.1 22 21.9 21.8 21.7 21.6 ...
##  $ yaw_arm             : num  -161 -161 -161 -161 -161 -161 -161 -161 -161 -161 ...
##  $ total_accel_arm     : num  34 34 34 34 34 34 34 34 34 34 ...
##  $ gyros_arm_x         : num  0 0.02 0.02 0.02 0 0.02 0 0.02 0.02 0.02 ...
##  $ gyros_arm_y         : num  0 -0.02 -0.02 -0.03 -0.03 -0.03 -0.03 -0.02 -0.03 -0.03 ...
##  $ gyros_arm_z         : num  -0.02 -0.02 -0.02 0.02 0 0 0 0 -0.02 -0.02 ...
##  $ accel_arm_x         : num  -288 -290 -289 -289 -289 -289 -289 -289 -288 -288 ...
##  $ accel_arm_y         : num  109 110 110 111 111 111 111 111 109 110 ...
##  $ accel_arm_z         : num  -123 -125 -126 -123 -123 -122 -125 -124 -122 -124 ...
##  $ magnet_arm_x        : num  -368 -369 -368 -372 -374 -369 -373 -372 -369 -376 ...
##  $ magnet_arm_y        : num  337 337 344 344 337 342 336 338 341 334 ...
##  $ magnet_arm_z        : num  516 513 513 512 506 513 509 510 518 516 ...
##  $ roll_dumbbell       : num  13.1 13.1 12.9 13.4 13.4 ...
##  $ pitch_dumbbell      : num  -70.5 -70.6 -70.3 -70.4 -70.4 ...
##  $ yaw_dumbbell        : num  -84.9 -84.7 -85.1 -84.9 -84.9 ...
##  $ total_accel_dumbbell: num  37 37 37 37 37 37 37 37 37 37 ...
##  $ gyros_dumbbell_x    : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ gyros_dumbbell_y    : num  -0.02 -0.02 -0.02 -0.02 -0.02 -0.02 -0.02 -0.02 -0.02 -0.02 ...
##  $ gyros_dumbbell_z    : num  0 0 0 -0.02 0 0 0 0 0 0 ...
##  $ accel_dumbbell_x    : num  -234 -233 -232 -232 -233 -234 -232 -234 -232 -235 ...
##  $ accel_dumbbell_y    : num  47 47 46 48 48 48 47 46 47 48 ...
##  $ accel_dumbbell_z    : num  -271 -269 -270 -269 -270 -269 -270 -272 -269 -270 ...
##  $ magnet_dumbbell_x   : num  -559 -555 -561 -552 -554 -558 -551 -555 -549 -558 ...
##  $ magnet_dumbbell_y   : num  293 296 298 303 292 294 295 300 292 291 ...
##  $ magnet_dumbbell_z   : num  -65 -64 -63 -60 -68 -66 -70 -74 -65 -69 ...
##  $ roll_forearm        : num  28.4 28.3 28.3 28.1 28 27.9 27.9 27.8 27.7 27.7 ...
##  $ pitch_forearm       : num  -63.9 -63.9 -63.9 -63.9 -63.9 -63.9 -63.9 -63.8 -63.8 -63.8 ...
##  $ yaw_forearm         : num  -153 -153 -152 -152 -152 -152 -152 -152 -152 -152 ...
##  $ total_accel_forearm : num  36 36 36 36 36 36 36 36 36 36 ...
##  $ gyros_forearm_x     : num  0.03 0.02 0.03 0.02 0.02 0.02 0.02 0.02 0.03 0.02 ...
##  $ gyros_forearm_y     : num  0 0 -0.02 -0.02 0 -0.02 0 -0.02 0 0 ...
##  $ gyros_forearm_z     : num  -0.02 -0.02 0 0 -0.02 -0.03 -0.02 0 -0.02 -0.02 ...
##  $ accel_forearm_x     : num  192 192 196 189 189 193 195 193 193 190 ...
##  $ accel_forearm_y     : num  203 203 204 206 206 203 205 205 204 205 ...
##  $ accel_forearm_z     : num  -215 -216 -213 -214 -214 -215 -215 -213 -214 -215 ...
##  $ magnet_forearm_x    : num  -17 -18 -18 -16 -17 -9 -18 -9 -16 -22 ...
##  $ magnet_forearm_y    : num  654 661 658 658 655 660 659 660 653 656 ...
##  $ magnet_forearm_z    : num  476 473 469 469 473 478 470 474 476 473 ...
##  $ classe              : Factor w/ 5 levels "A","B","C","D",..: 1 1 1 1 1 1 1 1 1 1 ...
```
**#Figure 1 Compare the 4 exercises and classe**
![](PML_Assignment_Report_files/figure-html/plot9-1.png) 


### Appendix II: Project [R] Code Listing

```r
## R Main Code Block
# figures and tables are call by small code blocks for printing at the appropriate 
#   places below.

# load required libraries and functions
library(caret)
library(randomForest)
library(ggplot2)
library(GGally)
library(lattice)
library(knitr)

##  GET and CLEAN data ##################

# fetch Training and Testing data (if necessary)
if(!file.exists("train.csv")){
  fileUrlTrain <- "https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv"
  download.file(fileUrlTrain, destfile = "train.csv")
  # save the download dates for reference
  dateTrainDownloaded <- date()
}
if(!file.exists("test.csv")){
  fileUrlTest <-"https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv"
  download.file(fileUrlTest, destfile = "test.csv")
  # save the download dates for reference
  dateTestDownloaded <- date()
}


## Read in (load) the data files for training and testing  ######
training <- read.csv("train.csv")
testing <- read.csv("test.csv")
## end of data aquision  ####################

## Clean and tidy data and subsetting  #############
#   remove and "#DIV/0" to make missing data
divfactorIDX <-training=="#DIV/0!"
training[divfactorIDX] = NA

# cvdt_timestamp, ie var# 5, correct to DATE type (POSIXlt)
#    var# 3 and 4 s/b ok as interger (esp. for now)
training$cvtd_timestamp <-strptime(as.character(training$cvtd_timestamp), "%d/%m/%Y %H:%M")
# make variables 7 to 159 all numeric
for(i in c(7:159))
  { 
    training[,i] <-as.numeric(as.character(training[,i]))
} 

for(i in c(7:159))
  { 
    testing[,i] <-as.numeric(as.character(testing[,i]))
}

#remove NA columns
# Routine to remove na values (Coursera, PML Discussion, Thread, "Error message when using train(), working on project", 11-22-20156 10:02AM,
    # see https://class.coursera.org/predmachlearn-034/forum/thread?thread_id=129&utm_medium=email&u     #   tm_source=other&utm_campaign=notifications.auto.V_7MppEiEeWqDRKfSaeX2Q#post-484
    # by ARJUN KV @ https://github.com/arj27083)

    # "You don't get the error if you remove variables with NA values. 
    #  Use the following code to remove it."
    # "Note: Must also remove zero variates for which need nearZeroVar() function."
    naVar <-function(df){
      na_var <- apply(!is.na(df),2,sum) #identifying the no of NAs in each column
      na_var <- na_var == nrow(df)  #Identifying columns that don't have complete data without NA
      df <- df[ , na_var]  #Filtering out variables with NA values
      return(df)
    }

# now clean the NA columns out of the dataframes
training <- naVar(training) # note last training column is now the classe factor variable
testing <- naVar(testing)   # note last column is redundant and classe is omitted for testing 
testing <- testing[,-60]    # remove redundant column

## end of data tidying


## Data exploration #################
## Plots
##  scatter plots
plot1 <- qplot(training$classe,training$accel_belt_y, main = "classe vs accel_belt_y")
plot2 <- qplot(training$classe,training$accel_dumbbell_y, main = "classe vs accel_dumbbell_x")
plot3 <- qplot(training$classe,training$accel_arm_z, main = "classe vs accel_arm_z")
plot4 <- qplot(training$classe,training$accel_forearm_z, main = "classe vs accel_forearm_z")
##  bar and whisker plots
plot5 <- function(){plot(training$classe,training$accel_belt_x, type="p",main = "classe vs accel_belt_x")}
plot6 <- function(){plot(training$classe,training$accel_dumbbell_y, type="p",main = "classe vs accel_dumbbell_y")}
plot7 <- function(){plot(training$classe,training$accel_arm_z, type="p",main = "classe vs accel_arm_z")}
plot8 <- function(){plot(training$classe,training$accel_forearm_x, type="p",main = "classe vs accel_forearm_x")}
##  pairs plot
plot9 <- ggpairs(training[,c(15,29,43,55,60)])
## end data exploration ##

## Build and Assess Model ####################
# built using numeric variables 8:59 as regressors and classe factor varibale (column 60) 
#  as the response variable
## model validation by the resampling method(s) inherent in the train() function
modelfit52 <- train(classe~.,data = training[,-c(1:7)], method="rf")


# plot groups in data, and their centers
##belt_arm_x <- classCenter(training[,c(15,28)], training$classe, training)
##belt_arm_x <- as.data.frame(belt_arm_x)
##belt_arm_x$classe <- rownames(belt_arm_x)

plot10 <- qplot(accel_belt_x,accel_arm_x, col="classe", data=training)
##plot10 <- plot10+geom_point(aes(accel_belt_x, accel_arm_x,col=classe), size=5, shape=4, data= training)

## Carry out predition using testing data with model fit from the training data
pred <- predict(modelfit52,testing[,-c(1:7)])
testing$predRight <- pred


## Files for 20 questions
answers = as.vector(as.character(pred))
  # Function to make files
  pml_write_files = function(x){
    n = length(x)
    for(i in 1:n){
      filename = paste0("problem_id_",i,".txt")
      write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
    }
  }

pml_write_files(answers)
modelfit52
print(plot10)
modelfit52
modelfit52$finalModel
cM <- confusionMatrix(modelfit52)
errRate <- 100 - sum(cM$table[1,1],cM$table[2,2],cM$table[3,3],cM$table[4,4],cM$table[5,5])
errRate
# display Training structure
str(training)
# display the pairs plot
plot9
## predict test set and assess model accuracy/error
pred <- predict(modelfit52,testing[,-c(1:7)])
## add the model predictions as a new column to the testing dataframe
testing$predRight <- pred
```

## Appendix III Assignment Criteria

### Background

Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it. In this project, your goal will be to use data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from [the HAR website](http://groupware.les.inf.puc-rio.br/har) (see the section on the Weight Lifting Exercise Dataset). 

### Data Source(s)

The data for this project come from the [source](http://groupware.les.inf.puc-rio.br/har). 

The training data for this project are available for download from  https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv

The test data are available for download from  https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv

### Purpose
Project goal is to predict the manner in which exercise is performed (technique). 

### Method
The response is the "classe" variable in the training set. Determine a set of variables which best predicts technique (classe). 

The Report describes how the model was built, how cross validation was used, the expected out of sample error, and why the choices were made. 

Finally, the prediction model is used to predict 20 different test cases to determine it's accuracy. 

### Requirements
1. Submit a link to a Github repo with the R markdown and compiled HTML file describing the analysis. The text of the writeup should be < 2000 words and the number of figures less than 5. Submitting a repo with a gh-pages branch is desirable so the HTML page can be viewed online.
2. The Machine Learning Algorithm will be applied to the 20 test cases available in the test data above. submitting the predictions, in appropriate format, to the programming assignment for automated grading. (See the [programming assignment](https://class.coursera.org/predmachlearn-034/human_grading/view/courses/975204/assessments/4/submissions) for additional details.

### Submitting the Predictions to the Questions
Apply the machine learning algorithm you built to each of the 20 test cases in the testing data set. See the prediction assignment writeup below on how model to be build. For each test case, submit a text file with a single capital letter (A, B, C, D, or E) corresponding to your prediction for the corresponding problem in the test data set. Score is 1 point for each correct answer. May be submitted up to 2 times for each problem. It is a lot of files to submit so it may be helpful to use the following function to create the files from a character vector with the 20 predictions in correct order for the 20 problems.  

```r
## predict test set and assess model accuracy/error
pred <- predict(modelfit52,testing[,-c(1:7)])
## add the model predictions as a new column to the testing dataframe
testing$predRight <- pred
```
Something like (note these are not the right answers!):
```
    answers = rep("A", 20)
```    
then load the following function by copying and pasting it into R: 
```
  pml_write_files = function(x){
    n = length(x)
    for(i in 1:n){
      filename = paste0("problem_id_",i,".txt")
      write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
    }
  }
```
create a folder where the files are to be written. Set that to be your working directory and run: 
```
    pml_write_files(answers)
```
to create one file for each submission. 

Note: using this script, make sure the files that get written out have one character each with the prediction for the corresponding problem ID. The script produces strange results if the answers variable is not a character vector. 



