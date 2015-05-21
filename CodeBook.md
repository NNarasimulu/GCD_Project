#CodeBook.md
Author: N Narasimulu
This code book  describes the variables, the data, and any transformations or work that was performed to clean up the data.

#--- Getting and Cleaning Data Project
# Variables
colNames : features.txt contains the column names for the test and train data sets. Read in the columns names to apply to the test and train data sets
activity : activity_labels.txt contains the description of the different activities.  This data is stored in the activity variable.

train.data : all training observations
train.labels : activity label ID for the corresponding activity for each observation
train.subject : the subject ID that corresponds to each observation
train : a merged train data set which includes the observation data plus activity ID's and subject ID's

test.data : all test observations
test.labels : activity label ID for the corresponding activity for each observation
test.subject : the subject ID that corresponds to each observation
test : a merged test data set which includes the observation data plus activity ID's and subject ID's

data : the merged data set which includes all observations from the underlying test and training data observations.
data.mean_std : a subset of the data data set, which includes the first two columns and all other columns which contain the text of "mean" or "std" (for standard deviation)

data.molten : This contains the melted data set where columns are converted to rows to facilitate easy column aggregation.
data.tidy : This is the summarised (dcast) data set which contains the mean or average observation grouped by for each activity type and corresponding subject.
