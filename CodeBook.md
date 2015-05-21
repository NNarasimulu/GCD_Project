#CodeBook.md
This code book  describes the variables, the data, and any transformations or work that was performed to clean up the data.

--- Getting and Cleaning Data Project

setwd("C:/Users/NNarasim/OneDrive/Education/Coursera/03. Getting and Cleaning Data/Project")

----- UCI HAR Dataset column names
 features.txt contains the column names for the test and train data sets
 read in the columns names to apply to the test and train data sets
colNames <- read.table("./UCI HAR Dataset/features.txt")

##############################################################
#----- UCI HAR Dataset train data
 read in train data and store in train.data
train.data <- read.table("./UCI HAR Dataset/train/X_train.txt")
 apply column names to train data
names(train.data) <- colNames[[2]]

 read in train labels  and store in train.labels
train.labels <- read.table("./UCI HAR Dataset/train/y_train.txt")
 assign default column name to train.labels column
names(train.labels) <- "labelID"

 read in train subjects and store in train.subject
train.subject <- read.table("./UCI HAR Dataset/train/subject_train.txt")
 assign default column name to train.subject column
names(train.subject) <- "subject"

 - combine all 3 data sets into a single train data set.
train <- cbind(train.subject, train.labels, train.data, type = "train")


##############################################################
#----- UCI HAR Dataset test data
 read in train data and store in test.data
test.data <- read.table("./UCI HAR Dataset/test/X_test.txt")
 apply column names to test data
names(test.data) <- colNames[[2]]

 read in test labels  and store in test.labels
test.labels <- read.table("./UCI HAR Dataset/test/y_test.txt")
 assign default column name to test.labels column
names(test.labels) <- "labelID"

 read in test subjects and store in test.subject
test.subject <- read.table("./UCI HAR Dataset/test/subject_test.txt")
 assign default column name to test.subject column
names(test.subject) <- "subject"

 combine all 3 data sets into a single test data set.
test <- cbind(test.subject, test.labels, test.data, type = "test")


##############################################################
#----- 1. Merges the training and the test sets to create one data set.
data <- rbind(train, test)


##############################################################
#----- 2. Extracts only the measurements on the mean and standard deviation 
#-----    for each measurement. 
 Find mean or std in the column name of the data set, include the first two columns
data.mean_std <- data[,c(1:2,grep(paste("mean", "std",sep = "|"), names(data)))]


##############################################################
#----- 3. Uses descriptive activity names to name the activities in the data set
#         read in activity label data (id & activity) and store in activity
activity <- read.table("./UCI HAR Dataset/activity_labels.txt")
 assign  column names to activity data set
names(activity) <- c("id","activity")
 add the activity column to the data_mean_std dataset where the ID's match
data.mean_std <- merge(data.mean_std , activity, by.x = "labelID", by.y = "id")

##############################################################
#----- 4. Appropriately labels the data set with descriptive variable names. 
 *** Data set column variables was named earlier in the code.
 *** Line 15 and Line 36 

##############################################################
#----- 5. From the data set in step 4, creates a second, independent tidy data 
#-----    set with the average of each variable for each activity and each subject.
 Use reshape2 to transform data set to calculate mean of all columns
library(reshape2)
data.molten <- melt(data.mean_std, id = c("activity","subject"))
data.tidy <- dcast(data.molten, activity + subject ~ variable, mean)
str(data.tidy)

 # Output data.tidy to a text file.
write.table(data.tidy, file="UCIHAR_Tidy_Dataset.txt", sep = ",", row.name=FALSE)
