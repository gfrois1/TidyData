# TidyData
##Get and Clean data project
##  Read training data
TrainSubject  = read.table("UCI HAR Dataset/train/Subject_train.txt", header = FALSE)
TrainActivity = read.table("UCI HAR Dataset/train/y_train.txt", header = FALSE)
TrainFeature  = read.table("UCI HAR Dataset/train/X_train.txt", header = FALSE)

##  Read test data
TestSubject  = read.table("UCI HAR Dataset/test/Subject_test.txt", header = FALSE)
TestActivity = read.table("UCI HAR Dataset/test/y_test.txt", header = FALSE)
TestFeature  = read.table("UCI HAR Dataset/test/X_test.txt", header = FALSE)

##  1 - Merging train and Test data
Subject  = rbind(TrainSubject,  TestSubject)
Activity = rbind(TrainActivity, TestActivity)
Feature  = rbind(TrainFeature,  TestFeature)

FeatureNames       = read.table("UCI HAR Dataset/features.txt")	## from Supporting Metadata
colnames(Feature)  = t(FeatureNames[2])  ## naming the columns

##  Merging
colnames(Subject)  = "Subject"
colnames(Activity) = "Activity"
MergedData         = cbind(Feature,Activity,Subject)

##  2 - Extracts only the measurements on the mean and standard deviation for each measurement

##  Extract the column indices that have either mean or std in them.
MeanStdCols     = grep(".*Mean.*|.*Std.*", names(MergedData), ignore.case=TRUE)

##  Add Activity and Subject columns to the list and look at the dimension of MergedData
requiredColumns = c(MeanStdCols, 562, 563)
dim(MergedData)

ExtractedData   = MergedData[,requiredColumns]
dim(ExtractedData)

##  3 - Uses descriptive Activity names to name the activities in the data set

## change Activity field type in ExtractedData from numeric to character 
## to accept Activity names from metadata ActivityLabels

ActivityLabels = read.table("UCI HAR Dataset/activity_labels.txt", header = FALSE)	##Supporting Metadata
ExtractedData$Activity = as.character(ExtractedData$Activity)
for (i in 1:6){
    ExtractedData$Activity[ExtractedData$Activity == i] = as.character(ActivityLabels[i,2])
}

## factor the Activity variable in
ExtractedData$Activity = as.factor(ExtractedData$Activity)

##  4 - Appropriately labels the data set with descriptive variable names
names(ExtractedData)=gsub("Acc", "Accelerometer", names(ExtractedData))
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

##  5 - From the data set in step 4, creates a second, independent tidy data set 
##      with the average of each variable for each Activity and each Subject

## set Subject as a factor variable.
ExtractedData$Subject = as.factor(ExtractedData$Subject)
ExtractedData         = data.table(ExtractedData)

##  create TidyData as a data set with average for each Activity and Subject. 
TidyData = aggregate(. ~Subject + Activity, ExtractedData, mean)

##  order the entries in TidyData 
TidyData = TidyData[order(TidyData$Subject,TidyData$Activity),]

##  write data file
write.table(TidyData, file = "TidyDataSet.txt", row.names = FALSE)
