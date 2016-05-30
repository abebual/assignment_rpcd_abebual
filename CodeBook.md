# assignment_rpcd_abebual
Coursera Course: Getting and Cleaning Data Assignment Solutions 
> getwd()
[1] "C:/Users/zerihunassociates/Documents/Courses/Data Science Specialization/CleaningandPreparingData/run_analysis"
> ##download the zip file
> download.file(url="https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip", destfile = wearable)
Error in download.file(url = "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip",  : 
  object 'wearable' not found
> download.file(url="https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip", destfile = "wearable")
trying URL 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip'
Content type 'application/zip' length 62556944 bytes (59.7 MB)
downloaded 59.7 MB

> unzip("wearable", list = TRUE)
                                                           Name   Length                Date
1                           UCI HAR Dataset/activity_labels.txt       80 2012-10-10 15:55:00
2                                  UCI HAR Dataset/features.txt    15785 2012-10-11 13:41:00
3                             UCI HAR Dataset/features_info.txt     2809 2012-10-15 15:44:00
4                                    UCI HAR Dataset/README.txt     4453 2012-12-10 10:38:00
5                                         UCI HAR Dataset/test/        0 2012-11-29 17:01:00
6                        UCI HAR Dataset/test/Inertial Signals/        0 2012-11-29 17:01:00
7     UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt  6041350 2012-11-29 15:08:00
8     UCI HAR Dataset/test/Inertial Signals/body_acc_y_test.txt  6041350 2012-11-29 15:08:00
9     UCI HAR Dataset/test/Inertial Signals/body_acc_z_test.txt  6041350 2012-11-29 15:08:00
10   UCI HAR Dataset/test/Inertial Signals/body_gyro_x_test.txt  6041350 2012-11-29 15:09:00
11   UCI HAR Dataset/test/Inertial Signals/body_gyro_y_test.txt  6041350 2012-11-29 15:09:00
12   UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt  6041350 2012-11-29 15:09:00
13   UCI HAR Dataset/test/Inertial Signals/total_acc_x_test.txt  6041350 2012-11-29 15:08:00
14   UCI HAR Dataset/test/Inertial Signals/total_acc_y_test.txt  6041350 2012-11-29 15:09:00
15   UCI HAR Dataset/test/Inertial Signals/total_acc_z_test.txt  6041350 2012-11-29 15:09:00
16                        UCI HAR Dataset/test/subject_test.txt     7934 2012-11-29 15:09:00
17                              UCI HAR Dataset/test/X_test.txt 26458166 2012-11-29 15:25:00
18                              UCI HAR Dataset/test/y_test.txt     5894 2012-11-29 15:09:00
19                                       UCI HAR Dataset/train/        0 2012-11-29 17:01:00
20                      UCI HAR Dataset/train/Inertial Signals/        0 2012-11-29 17:01:00
21  UCI HAR Dataset/train/Inertial Signals/body_acc_x_train.txt 15071600 2012-11-29 15:08:00
22  UCI HAR Dataset/train/Inertial Signals/body_acc_y_train.txt 15071600 2012-11-29 15:08:00
23  UCI HAR Dataset/train/Inertial Signals/body_acc_z_train.txt 15071600 2012-11-29 15:08:00
24 UCI HAR Dataset/train/Inertial Signals/body_gyro_x_train.txt 15071600 2012-11-29 15:09:00
25 UCI HAR Dataset/train/Inertial Signals/body_gyro_y_train.txt 15071600 2012-11-29 15:09:00
26 UCI HAR Dataset/train/Inertial Signals/body_gyro_z_train.txt 15071600 2012-11-29 15:09:00
27 UCI HAR Dataset/train/Inertial Signals/total_acc_x_train.txt 15071600 2012-11-29 15:08:00
28 UCI HAR Dataset/train/Inertial Signals/total_acc_y_train.txt 15071600 2012-11-29 15:08:00
29 UCI HAR Dataset/train/Inertial Signals/total_acc_z_train.txt 15071600 2012-11-29 15:08:00
30                      UCI HAR Dataset/train/subject_train.txt    20152 2012-11-29 15:09:00
31                            UCI HAR Dataset/train/X_train.txt 66006256 2012-11-29 15:25:00
32                            UCI HAR Dataset/train/y_train.txt    14704 2012-11-29 15:09:00
> library(plyr)
> library(data.table)
data.table 1.9.6  For help type ?data.table or https://github.com/Rdatatable/data.table/wiki
The fastest way to learn (by data.table authors): https://www.datacamp.com/courses/data-analysis-the-data-table-way
> library(dplyr)

Attaching package: ‘dplyr’

The following objects are masked from ‘package:data.table’:

    between, last

The following objects are masked from ‘package:plyr’:

    arrange, count, desc, failwith, id, mutate, rename, summarise, summarize

The following objects are masked from ‘package:stats’:

    filter, lag

The following objects are masked from ‘package:base’:

    intersect, setdiff, setequal, union

> Test_Y <- read.table(unzip("wearable", "UCI HAR Dataset/test/y_test.txt"))
> Test_X <- read.table(unzip("wearable", "UCI HAR Dataset/test/X_test.txt"))
> Test_Subject <- read.table(unzip("wearable", "UCI HAR Dataset/test/subject_test.txt"))
> Train_Y <- read.table(unzip("wearable", "UCI HAR Dataset/train/y_train.txt"))
> Train_X <- read.table(unzip("wearable", "UCI HAR Dataset/train/X_train.txt"))
> Train_Subject <- read.table(unzip("wearable", "UCI HAR Dataset/train/subject_train.txt"))
> Features <- read.table(unzip("wearable", "UCI HAR Dataset/features.txt"))
> unlink("wearables")
> ##fix column names
> colnames(Train_X)<- t(Features[2])
> colnames(Test_X)<- t(Features[2])
> Train_X$activities<-Train_Y[, 1]
> Train_X$participants<-Train_Subject[,1]
> Test_X$activities<-Test_Y[,1]
> Test_X$participants<-Test_Subject[,1]
> ##TASK 1 Merge the training and test datasets 
> Merged_Wearables<-rbind(Train_X, Test_X)
> duplicated(colnames(Merged_Wearables))
  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [17] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [33] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [65] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [81] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
 [97] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[113] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[129] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[145] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[161] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[177] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[193] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[209] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[225] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[241] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[257] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[273] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[289] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[305] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
[321]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
[337]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[353] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[369] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[385] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
[401]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
[417]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[433] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[449] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[465] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
[481]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
[497]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[513] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[529] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[545] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[561] FALSE FALSE FALSE
> Merged_Wearables<-Merged_Wearables[, !duplicated(colnames(Merged_Wearables))]
> ##Task2: Extracts only the measurements on the mean and standard deviation for each measurement
> Mean_Wearables<-grep("mean()", names(Merged_Wearables), value=FALSE, fixed=TRUE)
> Mean_Wearables<- append(Mean_Wearables, 471:477)
> SD_Wearables<-grep("std()", names(Merged_Wearables), value=FALSE)
> Mean_Wearables<-Merged_Wearables[Mean_Wearables]
> SD_Wearables<-Merged_Wearables[SD_Wearables]
> ##Task3: Uses descriptive activity names to name the activities in the data set
> Merged_Wearables$activities <- as.character(Merged_Wearables$activities)
> Merged_Wearables$activities[Merged_Wearables$activities == 1] <- "Walking"
> Merged_Wearables$activities[Merged_Wearables$activities == 2] <- "Walking Upstairs"
> Merged_Wearables$activities[Merged_Wearables$activities == 3] <- "Walking Downstairs"
> Merged_Wearables$activities[Merged_Wearables$activities == 4] <- "Sitting"
> Merged_Wearables$activities[Merged_Wearables$activities == 5] <- "Standing"
> Merged_Wearables$activities[Merged_Wearables$activities == 6] <- "Laying"
> Merged_Wearables$activities <- as.factor(Merged_Wearables$activities)
> ##Task 4: Appropriately labels the data set with descriptive variable names.
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
> 
> 
> ##Task5: From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
> Merged_Wearables.dt <- data.table(Merged_Wearables)
> FinalTidyData <- Merged_Wearables.dt[, lapply(.SD, mean), by = 'participants,activities']
> write.table(FinalTidyData, file = "FinalTidyData.txt", row.names = FALSE)
