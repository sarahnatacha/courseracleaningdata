### Getting and Cleaning Data - Course Project

### Human Activity Recognition Using Smartphones Dataset

This repository hosts the code for the Getting and Cleaning Data Course project.

It is using the data from
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

### Files
1. CodeBook.md describes the variables, the data, and any transformations or work that was performed to clean up the data.
2. Output is a tidy data set called tidyMeans.txt
3. run_analysis.R contains all the code to perform the analysis requested. It can be run by executing the following:

* install.packages("data.table") if not already installed
* library(data.table) if not already loaded
* install.packages("plyr") if not already installed
* library(plyr)
* source("run_analysis.R") 
* runAnalysis() to create the tidy set
* checkData() to check the file that was produced
