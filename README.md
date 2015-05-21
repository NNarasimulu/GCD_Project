#Getting and Cleaning Data Project

This documents explains how the scripts work to transform the data sets into a "tidy" data set.
This explains how all of the scripts work and how they are connected.

Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained: 

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The R script (run_analysis.R) contained in repository performs the following operations:
  1.  Reads in the two data sets (training & test), assigns, and merges the activity and subjects for the observations.
  2.  the respective data sets for training & test are merged to create one data set.
  3.  The measurements on the mean and standard deviation columns are extracted as a new data set. 
  4.  Descriptive activity names, sourced from the activity file is used to assign activity descriptions to the corresponding   activity ID's.
  5.  the subset of mean and standard deviation data, is transformed into a "tidy data set", which contains the mean of each   variable for each activity and each subject.
  6.  The "tidy data set" is written to a text file "UCIHAR_Tidy_Dataset.txt".
