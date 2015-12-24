---
title: "CodeBook of Get and Clean Data Project"
author: "gfrois"
date: "24 December 2015"
output: html_document
---
CodeBook of Get and Clean Data Project

Source:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Full Description at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Process

The script run_analysis.R performs the following process to clean up the data and create tiny data sets:

    Merge the training and test sets to create one data set.

    Reads features.txt and uses only the measurements on the mean and standard deviation for each measurement.

    Reads activity_labels.txt and applies human readable activity names to name the activities in the data set.

    Labels the data set with descriptive names. 

    Merges the features with activity labels and subject IDs. 

Variables

##  Read training data
TrainSubject  contains "UCI HAR Dataset/train/Subject_train.txt"
TrainActivity contains "UCI HAR Dataset/train/y_train.txt"
TrainFeature  contains "UCI HAR Dataset/train/X_train.txt"

##  Read test data
TestSubject  contains "UCI HAR Dataset/test/Subject_test.txt"
TestActivity contains "UCI HAR Dataset/test/y_test.txt"
TestFeature  contains "UCI HAR Dataset/test/X_test.txt",

##  1 - Merging train and Test data
Subject  contains TrainSubject merged with TestSubject
Activity contains TrainActivity merged with TestActivity
Feature  contains TrainFeature merged with TestFeature
FeatureNames       contains "UCI HAR Dataset/features.txt from Supporting Metadata
colnames(Feature)  naming the columns

colnames(Subject)  = "Subject"
colnames(Activity) = "Activity"

##  Merging
MergedData         contains Feature,Activity,Subject merged together


MeanStdCols    Extract the column indices that have either mean or std in them.

##  Add Activity and Subject columns to the list and look at the dimension of MergedData
requiredColumns 
dim(MergedData)

ExtractedData   
dim(ExtractedData)

##  3 - Uses descriptive Activity names to name the activities in the data set

## change Activity field type in ExtractedData from numeric to character to accept Activity names from metadata 
##  ActivityLabels
ActivityLabels contains Supporting Metadata
ExtractedData$Activity 

## factor the Activity variable in
ExtractedData$Activity 

##  4 - Appropriately labels the data set with descriptive variable names
names(ExtractedData)=gsub("Acc", "Accelerometer", names(ExtractedData))  ## names variables from and to
names(ExtractedData)=gsub("Gyro", "Gyroscope", names(ExtractedData))
names(ExtractedData)=gsub("BodyBody", "Body", names(ExtractedData))
names(ExtractedData)=gsub("Mag", "Magnitude", names(ExtractedData))
names(ExtractedData)=gsub("^t", "Time", names(ExtractedData))
names(ExtractedData)=gsub("^f", "Frequency", names(ExtractedData))
names(ExtractedData)=gsub("tBody", "TimeBody", names(ExtractedData))
names(ExtractedData)=gsub("-mean()", "Mean", names(ExtractedData), ignore.case = TRUE)
names(ExtractedData)=gsub("-std()", "STD", names(ExtractedData), ignore.case = TRUE)
names(ExtractedData)=gsub("-freq()", "Frequency", names(ExtractedData), ignore.case = TRUE)

names(ExtractedData)

##  5 - From the data set in step 4, creates a second, independent tidy data set with the average of each 
##  variable for each Activity and each Subject

## set Subject as a factor variable.
ExtractedData$Subject = as.factor(ExtractedData$Subject)
ExtractedData         = data.table(ExtractedData)

##  create TidyData as a data set with average for each Activity and Subject. 
TidyData = aggregate(. ~Subject + Activity, ExtractedData, mean)

##  order the entries in TidyData 
TidyData = TidyData[order(TidyData$Subject,TidyData$Activity),]

##  write data file
write.table(TidyData, file = "TidyDataSet.txt", row.names = FALSE)



