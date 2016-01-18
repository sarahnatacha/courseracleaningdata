# Code Book for Getting and Cleaning Data Course Project

## Subject and Activity

These variables identify the unique subject/activity pair the variables relate to:

 - Subject: the integer subject ID.
 - Activity: the string activity name:
  - Walking
  - Walking Upstairs
  - Walking Downstairs
  - Sitting
  - Standing
  - Laying

## Measurement Means

All variables are the mean of a measurement for each subject and activity. This is indicated by the initial Mean in the variable name. All values are floating point numbers.

 - Time domain body acceleration mean along X, Y, and Z:
  - MeanTimeBodyAccMeanX
  - MeanTimeBodyAccMeanY
  - MeanTimeBodyAccMeanZ
 - Time domain body acceleration standard deviation along X, Y, and Z:
  - MeanTimeBodyAccStdDevX
  - MeanTimeBodyAccStdDevY
  - MeanTimeBodyAccStdDevZ
 - Time domain gravity acceleration mean along X, Y, and Z:
  - MeanTimeGravityAccMeanX
  - MeanTimeGravityAccMeanY
  - MeanTimeGravityAccMeanZ
 - Time domain gravity acceleration standard deviation along X, Y, and Z:
  - MeanTimeGravityAccStdDevX
  - MeanTimeGravityAccStdDevY
  - MeanTimeGravityAccStdDevZ
 - Time domain body jerk mean along X, Y, and Z:
  - MeanTimeBodyAccJerkMeanX
  - MeanTimeBodyAccJerkMeanY
  - MeanTimeBodyAccJerkMeanZ
 - Time domain body jerk standard deviation along X, Y, and Z:
  - MeanTimeBodyAccJerkStdDevX
  - MeanTimeBodyAccJerkStdDevY
  - MeanTimeBodyAccJerkStdDevZ
 - Time domain gyroscope mean along X, Y, and Z:
  - MeanTimeBodyGyroMeanX
  - MeanTimeBodyGyroMeanY
  - MeanTimeBodyGyroMeanZ
 - Time domain gyroscope standard deviation along X, Y, and Z:
  - MeanTimeBodyGyroStdDevX
  - MeanTimeBodyGyroStdDevY
  - MeanTimeBodyGyroStdDevZ
 - Time domain gyroscope jerk mean along X, Y, and Z:
  - MeanTimeBodyGyroJerkMeanX
  - MeanTimeBodyGyroJerkMeanY
  - MeanTimeBodyGyroJerkMeanZ
 - Time domain gyroscope jerk standard deviation along X, Y, and Z:
  - MeanTimeBodyGyroJerkStdDevX
  - MeanTimeBodyGyroJerkStdDevY
  - MeanTimeBodyGyroJerkStdDevZ
 - Time domain body acceleration magnitude mean:
  - MeanTimeBodyAccMagMean
 - Time domain body acceleration magnitude standard deviation:
  - MeanTimeBodyAccMagStdDev
 - Time domain gravity acceleration magnitude mean:
  - MeanTimeGravityAccMagMean
 - Time domain gravity acceleration magnitude standard deviation:
  - MeanTimeGravityAccMagStdDev
 - Time domain body jerk magnitude mean:
  - MeanTimeBodyAccJerkMagMean
 - Time domain body jerk magnitude standard deviation:
  - MeanTimeBodyAccJerkMagStdDev
 - Time domain gyroscope magnitude mean:
  - MeanTimeBodyGyroMagMean
 - Time domain gyroscope magnitude standard deviation:
  - MeanTimeBodyGyroMagStdDev
 - Time domain gyroscope jerk magnitude mean:
  - MeanTimeBodyGyroJerkMagMean
 - Time domain gyroscope jerk magnitude standard deviation:
  - MeanTimeBodyGyroJerkMagStdDev
 - Frequency domain body acceleration mean along X, Y, and Z:
  - MeanFrequencyBodyAccMeanX
  - MeanFrequencyBodyAccMeanY
  - MeanFrequencyBodyAccMeanZ
 - Frequency domain body acceleration standard deviation along X, Y, and Z:
  - MeanFrequencyBodyAccStdDevX
  - MeanFrequencyBodyAccStdDevY
  - MeanFrequencyBodyAccStdDevZ
 - Frequency domain body jerk mean along X, Y, and Z:
  - MeanFrequencyBodyAccJerkMeanX
  - MeanFrequencyBodyAccJerkMeanY
  - MeanFrequencyBodyAccJerkMeanZ
 - Frequency domain body jerk standard deviation along X, Y, and Z:
  - MeanFrequencyBodyAccJerkStdDevX
  - MeanFrequencyBodyAccJerkStdDevY
  - MeanFrequencyBodyAccJerkStdDevZ
 - Frequency domain gyroscope mean along X, Y, and Z:
  - MeanFrequencyBodyGyroMeanX
  - MeanFrequencyBodyGyroMeanY
  - MeanFrequencyBodyGyroMeanZ
 - Frequency domain gyroscope standard deviation along X, Y, and Z:
  - MeanFrequencyBodyGyroStdDevX
  - MeanFrequencyBodyGyroStdDevY
  - MeanFrequencyBodyGyroStdDevZ
 - Frequency domain body acceleration magnitude mean:
  - MeanFrequencyBodyAccMagMean
 - Frequency domain body acceleration magnitude standard deviation:
  - MeanFrequencyBodyAccMagStdDev
 - Frequency domain body jerk magnitude mean:
  - MeanFrequencyBodyAccJerkMagMean
 - Frequency domain body jerk magnitude standard deviation:
  - MeanFrequencyBodyAccJerkMagStdDev
 - Frequency domain gyroscope magnitude mean:
  - MeanFrequencyBodyGyroMagMean
 - Frequency domain gyroscope magnitude standard deviation:
  - MeanFrequencyBodyGyroMagStdDev
 - Frequency domain gyroscope jerk magnitude mean:
  - MeanFrequencyBodyGyroJerkMagMean
 - Frequency domain gyroscope jerk magnitude standard deviation:
  - MeanFrequencyBodyGyroJerkMagStdDev

## Code description

* Get and extract data
    
   ``` url <- \"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip\"```

    ```zipFile <- "dataset.zip"```
    ```if(!file.exists(zipFile)) { download.file(url, zipFile) }```
        
    ```dataDir <- "UCI HAR Dataset"```
    ```if(!file.exists(dataDir)) { unzip(zipFile, exdir = ".") } ```

    
    * Merges the training and the test sets to create one data set.
    
   ``` readData <- function(path) {
        read.table(filePath(dataDir, path))
    }```
    
    * Reads and caches XTrain and XTest data
    ```if(is.null(XTrain)) { XTrain <<- readData("train/X_train.txt") }```
    ```if(is.null(XTest))  { XTest  <<- readData("test/X_test.txt") }```
    ```merged <- rbind(XTrain, XTest)```
    
    ```featureNames <- readData("features.txt")[, 2]```
    ```names(merged) <- featureNames```
    
    * Extracts only the measurements on the mean and standard deviation for each measurement. Limit to columns with feature names matching mean() or std():
    ```matches <- grep("(mean|std)\\(\\)", names(merged))
    limited <- merged[, matches]```
    
    * Uses descriptive activity names to name the activities in the data set.Get the activity data and map to variable names:
    ```path <- getwd()```
    ```pathIn <- file.path(path, "UCI HAR Dataset")```
    
    ```yTrain <- fread(file.path(pathIn, "train", "y_train.txt"))```
   ``` yTest <- fread(file.path(pathIn, "test", "y_test.txt"))```
    ```yMerged <- rbind(yTrain, yTest)[, 1]```
    
    ```activityNames <-
        c("Walking", "Walking Upstairs", "Walking Downstairs", "Sitting", "Standing", "Laying")```
    ```activities <- activityNames[yMerged]```
    
    * Appropriately labels the data set with descriptive variable names.Change t to Time, f to Frequency, mean() to Mean and std() to StdDev. Remove extra dashes and BodyBody naming error from original feature names
    ```names(limited) <- gsub("^t", "Time", names(limited))
    names(limited) <- gsub("^f", "Frequency", names(limited))
    names(limited) <- gsub("-mean\\(\\)", "Mean", names(limited))
    names(limited) <- gsub("-std\\(\\)", "StdDev", names(limited))
    names(limited) <- gsub("-", "", names(limited))
    names(limited) <- gsub("BodyBody", "Body", names(limited))```
    
    * Add activities and subject with variable  names
    ```subjectTrain <- fread(file.path(pathIn, "train", "subject_train.txt"))```
    ```subjectTest <- fread(file.path(pathIn, "test", "subject_test.txt"))```
    ```subjects <- rbind(subjectTrain, subjectTest)[, 1]```
    
    ```tidy <- cbind(Subject = subjects, Activity = activities, limited)```
    
    * Creates a second, independent tidy data set with the average of each variable for each activity and each subject.
    ```library(plyr)```
    
    * Column means for all but the subject and activity columns
    ```limitedColMeans <- function(data) { colMeans(data[,-c(1,2)]) }
    tidyMeans <- ddply(tidy, .(Subject, Activity), limitedColMeans)
    names(tidyMeans)[-c(1,2)] <- paste0("Mean", names(tidyMeans)[-c(1,2)])```
    
    
    * Writes file
    ``` write.table(tidyMeans, "tidyMeans.txt", row.names = FALSE)```
    