# assignment_rpcd_abebual
##Coursera Course: Getting and Cleaning Data Assignment Solutions 
## Enusre correct directory
> getwd()
[1] "C:/Users/zerihunassociates/Documents/Courses/Data Science Specialization/CleaningandPreparingData/run_analysis"

##download the zip file from the server 
> download.file(url="https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip", destfile = "wearable")
trying URL 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip'
Content type 'application/zip' length 62556944 bytes (59.7 MB)
downloaded 59.7 MB

> unzip("wearable", list = TRUE)

## load library 
> library(plyr)
> library(data.table)
> library(dplyr)


#loading the files into R
> Test_Y <- read.table(unzip("wearable", "UCI HAR Dataset/test/y_test.txt"))
> Test_X <- read.table(unzip("wearable", "UCI HAR Dataset/test/X_test.txt"))
> Test_Subject <- read.table(unzip("wearable", "UCI HAR Dataset/test/subject_test.txt"))
> Train_Y <- read.table(unzip("wearable", "UCI HAR Dataset/train/y_train.txt"))
> Train_X <- read.table(unzip("wearable", "UCI HAR Dataset/train/X_train.txt"))
> Train_Subject <- read.table(unzip("wearable", "UCI HAR Dataset/train/subject_train.txt"))
> Features <- read.table(unzip("wearable", "UCI HAR Dataset/features.txt"))
> unlink("wearables")

##fix column names
> colnames(Train_X)<- t(Features[2])
> colnames(Test_X)<- t(Features[2])
> Train_X$activities<-Train_Y[, 1]
> Train_X$participants<-Train_Subject[,1]
> Test_X$activities<-Test_Y[,1]
> Test_X$participants<-Test_Subject[,1]

##TASK 1 Merge the training and test datasets 
> Merged_Wearables<-rbind(Train_X, Test_X)
> duplicated(colnames(Merged_Wearables))
> Merged_Wearables<-Merged_Wearables[, !duplicated(colnames(Merged_Wearables))]

##Task2: Extracts only the measurements on the mean and standard deviation for each measurement
  ##calculating mean and standard deviations 
> Mean_Wearables<-grep("mean()", names(Merged_Wearables), value=FALSE, fixed=TRUE)
> Mean_Wearables<- append(Mean_Wearables, 471:477)
> SD_Wearables<-grep("std()", names(Merged_Wearables), value=FALSE)
> Mean_Wearables<-Merged_Wearables[Mean_Wearables]
> SD_Wearables<-Merged_Wearables[SD_Wearables]

##Task3: Uses descriptive activity names to name the activities in the data set
> Merged_Wearables$activities <- as.character(Merged_Wearables$activities)
> Merged_Wearables$activities[Merged_Wearables$activities == 1] <- "Walking"
> Merged_Wearables$activities[Merged_Wearables$activities == 2] <- "Walking Upstairs"
> Merged_Wearables$activities[Merged_Wearables$activities == 3] <- "Walking Downstairs"
> Merged_Wearables$activities[Merged_Wearables$activities == 4] <- "Sitting"
> Merged_Wearables$activities[Merged_Wearables$activities == 5] <- "Standing"
> Merged_Wearables$activities[Merged_Wearables$activities == 6] <- "Laying"
> Merged_Wearables$activities <- as.factor(Merged_Wearables$activities)

##Task 4: Appropriately labels the data set with descriptive variable names.
> names(Merged_Wearables) <- gsub("Acc", "Accelerator", names(Merged_Wearables))
> names(Merged_Wearables) <- gsub("Mag", "Magnitude", names(Merged_Wearables))
> names(Merged_Wearables) <- gsub("Gyro", "Gyroscope", names(Merged_Wearables))
> names(Merged_Wearables) <- gsub("^t", "time", names(Merged_Wearables))
> names(Merged_Wearables) <- gsub("^f", "frequency", names(Merged_Wearables))
> Merged_Wearables$participants <- as.character(Merged_Wearables$participants)
> Merged_Wearables$participants[Merged_Wearables$participants == 1] <- "Participant 1"
> Merged_Wearables$participants[Merged_Wearables$participants == 2] <- "Participant 2"
> Merged_Wearables$participants[Merged_Wearables$participants == 3] <- "Participant 3"
> Merged_Wearables$participants[Merged_Wearables$participants == 4] <- "Participant 4"
> Merged_Wearables$participants[Merged_Wearables$participants == 5] <- "Participant 5"
> Merged_Wearables$participants[Merged_Wearables$participants == 6] <- "Participant 6"
> Merged_Wearables$participants[Merged_Wearables$participants == 7] <- "Participant 7"
> Merged_Wearables$participants[Merged_Wearables$participants == 8] <- "Participant 8"
> Merged_Wearables$participants[Merged_Wearables$participants == 9] <- "Participant 9"
> Merged_Wearables$participants[Merged_Wearables$participants == 10] <- "Participant 10"
> Merged_Wearables$participants[Merged_Wearables$participants == 11] <- "Participant 11"
> Merged_Wearables$participants[Merged_Wearables$participants == 12] <- "Participant 12"
> Merged_Wearables$participants[Merged_Wearables$participants == 13] <- "Participant 13"
> Merged_Wearables$participants[Merged_Wearables$participants == 14] <- "Participant 14"
> Merged_Wearables$participants[Merged_Wearables$participants == 15] <- "Participant 15"
> Merged_Wearables$participants[Merged_Wearables$participants == 16] <- "Participant 16"
> Merged_Wearables$participants[Merged_Wearables$participants == 17] <- "Participant 17"
> Merged_Wearables$participants[Merged_Wearables$participants == 18] <- "Participant 18"
> Merged_Wearables$participants[Merged_Wearables$participants == 19] <- "Participant 19"
> Merged_Wearables$participants[Merged_Wearables$participants == 20] <- "Participant 20"
> Merged_Wearables$participants[Merged_Wearables$participants == 21] <- "Participant 21"
> Merged_Wearables$participants[Merged_Wearables$participants == 22] <- "Participant 22"
> Merged_Wearables$participants[Merged_Wearables$participants == 23] <- "Participant 23"
> Merged_Wearables$participants[Merged_Wearables$participants == 24] <- "Participant 24"
> Merged_Wearables$participants[Merged_Wearables$participants == 25] <- "Participant 25"
> Merged_Wearables$participants[Merged_Wearables$participants == 26] <- "Participant 26"
> Merged_Wearables$participants[Merged_Wearables$participants == 27] <- "Participant 27"
> Merged_Wearables$participants[Merged_Wearables$participants == 28] <- "Participant 28"
> Merged_Wearables$participants[Merged_Wearables$participants == 29] <- "Participant 29"
> Merged_Wearables$participants[Merged_Wearables$participants == 30] <- "Participant 30"
> Merged_Wearables$participants <- as.factor(Merged_Wearables$participants)


##Task5: From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
> Merged_Wearables.dt <- data.table(Merged_Wearables)

##Creating final tidy dataset 
> FinalTidyData <- Merged_Wearables.dt[, lapply(.SD, mean), by = 'participants,activities']
> write.table(FinalTidyData, file = "FinalTidyData.txt", row.names = FALSE)
