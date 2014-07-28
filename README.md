Project-Getting-and-Cleaning-Data
=================================

# 1. Merges the training and the test sets to create one data set.

# Bring the data into R
# Unzip the data for the project and save the extracted folder "UCI HAR Dataset" in the working directory 

training_data  <- read.table("UCI HAR Dataset/train/X_train.txt")
training_labels  <-  read.table("UCI HAR Dataset/train/y_train.txt")
training_subject  <- read.table("UCI HAR Dataset/train/subject_train.txt")
test_data  <- read.table("UCI HAR Dataset/test/X_test.txt")
test_labels  <- read.table("UCI HAR Dataset/test/y_test.txt")
test_subject  <- read.table("UCI HAR Dataset/test/subject_test.txt")
features  <- read.table("UCI HAR Dataset/features.txt")


# Merge the two data frames "training_data" and "test_data"
merged_data  <- rbind(training_data,test_data)
colnames(merged_data)  <- features[,2]

merged_subject  <- rbind(training_subject,test_subject)
colnames(merged_subject)  <- "Subject"
merged_labels  <- rbind(training_labels,test_labels)
colnames(merged_labels)  <- "Activity_Label"

merged_data2  <- cbind(merged_subject,merged_labels,merged_data)

####################################################################################
# 2. Extracts only the measurements on the mean and standard deviation for each measurement.

mean_extract  <- grep("mean",names(merged_data2),value=T)
std_extract  <- grep("std",names(merged_data2),value=T)

# select the variables "Subject", "Activity_Label" and variables containing the mean and standard deviation
merged_data3  <- merged_data2[,c("Subject","Activity_Label",mean_extract,std_extract)]

####################################################################################
# 3. Uses descriptive activity names to name the activities in the data set

activity_labels  <- read.table("UCI HAR Dataset/activity_labels.txt")
merged_data3$"Activity_Label"  <- factor(merged_data3$"Activity_Label",levels=activity_labels$V1,labels=activity_labels$V2)

####################################################################################
# 4. Appropriately labels the data set with descriptive variable names.

# Create Tidy Variable Names 

TidyVarNames  <- c("Subject","Activity_Label","TimeSignalsBodyAccelerationMeanValueXaxis","TimeSignalsBodyAccelerationMeanValueYaxis","TimeSignalsBodyAccelerationMeanValueZaxis","TimeSignalsGravityAccelerationMeanValueXaxis","TimeSignalsGravityAccelerationMeanValueYaxis","TimeSignalsGravityAccelerationMeanValueZaxis","TimeSignalsBodyAccelerationJerkMeanValueXaxis","TimeSignalsBodyAccelerationJerkMeanValueYaxis","TimeSignalsBodyAccelerationJerkMeanValueZaxis","TimeSignalsBodyGyroMeanValueXaxis","TimeSignalsBodyGyroMeanValueYaxis","TimeSignalsBodyGyroMeanValueZaxis","TimeSignalsBodyGyroJerkMeanValueXaxis","TimeSignalsBodyGyroJerkMeanValueYaxis","TimeSignalsBodyGyroJerkMeanValueZaxis","TimeSignalsBodyAccelerationMagnitudeMeanValue","TimeSignalsGravityAccelerationMagnitudeMeanValue","TimeSignalsBodyAccelerationJerkMagnitudeMeanValue","TimeSignalsBodyGyroMagnitudeMeanValue","TimeSignalsBodyGyroJerkMagnitudeMeanValue","FrequencySignalsBodyAccelerationMeanValueXaxis","FrequencySignalsBodyAccelerationMeanValueYaxis","FrequencySignalsBodyAccelerationMeanValueZaxis","FrequencySignalsBodyAccelerationMeanValueFrequencyXaxis","FrequencySignalsBodyAccelerationMeanValueFrequencyYaxis","FrequencySignalsBodyAccelerationMeanValueFrequencyZaxis","FrequencySignalsBodyAccelerationJerkMeanValueXaxis","FrequencySignalsBodyAccelerationJerkMeanValueYaxis","FrequencySignalsBodyAccelerationJerkMeanValueZaxis","FrequencySignalsBodyAccelerationJerkMeanValueFrequencyXaxis","FrequencySignalsBodyAccelerationJerkMeanValueFrequencyYaxis","FrequencySignalsBodyAccelerationJerkMeanValueFrequencyZaxis","FrequencySignalsBodyGyroMeanValueXaxis","FrequencySignalsBodyGyroMeanValueYaxis","FrequencySignalsBodyGyroMeanValueZaxis","FrequencySignalsBodyGyroMeanValueFrequencyXaxis","FrequencySignalsBodyGyroMeanValueFrequencyYaxis","FrequencySignalsBodyGyroMeanValueFrequencyZaxis","FrequencySignalsBodyAccelerationMagnitudeMeanValue","FrequencySignalsBodyAccelerationMagnitudeMeanValueFrequency","FrequencySignalsBodyAccelerationJerkMagnitudeMeanValue","FrequencySignalsBodyAccelerationJerkMagnitudeMeanValueFrequency","FrequencySignalsBodyGyroMagnitudeMeanValue","FrequencySignalsBodyGyroMagnitudeMeanValueFrequency","FrequencySignalsBodyGyroJerkMagnitudeMeanValue","FrequencySignalsBodyGyroJerkMagnitudeMeanValueFrequency", "TimeSignalsBodyAccelerationStandardDeviationXaxis","TimeSignalsBodyAccelerationStandardDeviationYaxis","TimeSignalsBodyAccelerationStandardDeviationZaxis","TimeSignalsGravityAccelerationStandardDeviationXaxis","TimeSignalsGravityAccelerationStandardDeviationYaxis","TimeSignalsGravityAccelerationStandardDeviationZaxis","TimeSignalsBodyAccelerationJerkStandardDeviationXaxis","TimeSignalsBodyAccelerationJerkStandardDeviationYaxis","TimeSignalsBodyAccelerationJerkStandardDeviationZaxis","TimeSignalsBodyGyroStandardDeviationXaxis","TimeSignalsBodyGyroStandardDeviationYaxis","TimeSignalsBodyGyroStandardDeviationZaxis","TimeSignalsBodyGyroJerkStandardDeviationXaxis","TimeSignalsBodyGyroJerkStandardDeviationYaxis","TimeSignalsBodyGyroJerkStandardDeviationZaxis","TimeSignalsBodyAccelerationMagnitudeStandardDeviation","TimeSignalsGravityAccelerationMagnitudeStandardDeviation","TimeSignalsBodyAccelerationJerkMagnitudeStandardDeviation","TimeSignalsBodyGyroMagnitudeStandardDeviation","TimeSignalsBodyGyroJerkMagnitudeStandardDeviation","FrequencySignalsBodyAccelerationStandardDeviationXaxis","FrequencySignalsBodyAccelerationStandardDeviationYaxis","FrequencySignalsBodyAccelerationStandardDeviationZaxis","FrequencySignalsBodyAccelerationStandardDeviationFrequencyXaxis","FrequencySignalsBodyAccelerationStandardDeviationFrequencyYaxis","FrequencySignalsBodyAccelerationStandardDeviationFrequencyZaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationXaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationYaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationZaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationFrequencyXaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationFrequencyYaxis","FrequencySignalsBodyAccelerationJerkStandardDeviationFrequencyZaxis","FrequencySignalsBodyGyroStandardDeviationXaxis","FrequencySignalsBodyGyroStandardDeviationYaxis","FrequencySignalsBodyGyroStandardDeviationZaxis","FrequencySignalsBodyGyroStandardDeviationFrequencyXaxis","FrequencySignalsBodyGyroStandardDeviationFrequencyYaxis","FrequencySignalsBodyGyroStandardDeviationFrequencyZaxis","FrequencySignalsBodyAccelerationMagnitudeStandardDeviation","FrequencySignalsBodyAccelerationMagnitudeStandardDeviationFrequency","FrequencySignalsBodyAccelerationJerkMagnitudeStandardDeviation","FrequencySignalsBodyAccelerationJerkMagnitudeStandardDeviationFrequency","FrequencySignalsBodyGyroMagnitudeStandardDeviation","FrequencySignalsBodyGyroMagnitudeStandardDeviationFrequency","FrequencySignalsBodyGyroJerkMagnitudeStandardDeviation","FrequencySignalsBodyGyroJerkMagnitudeStandardDeviationFrequency")



####################################################################################
# 5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

library(reshape2)

melt_data  <- melt(merged_data3,id=c("Subject","Activity_Label"),measure.vars=names(x[,-c(1,2)]))
merged_data4  <- dcast(melt_data,Subject + Activity_Label ~ variable,mean)
FinalTidy_Dataset <- merged_data4

# Export the final tidy dataset as a csv and txt file
write.table(FinalTidy_Dataset,"TidyDataset.txt",sep="\t")
write.csv(FinalTidy_Dataset,file="TidyDataset.csv")
