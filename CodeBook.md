# COURSERA Getting and Cleaning Data project

### Original data and its description

1. Data: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 
2. Description: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 


### Information about the variables

The variables used in this project are described in the featires_info.txt file thet comes with the row data set. Below you can find a part of this description.

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

* tBodyAcc-XYZ
* tGravityAcc-XYZ
* tBodyAccJerk-XYZ
* tBodyGyro-XYZ
* tBodyGyroJerk-XYZ
* tBodyAccMag
* tGravityAccMag
* tBodyAccJerkMag
* tBodyGyroMag
* tBodyGyroJerkMag
* fBodyAcc-XYZ
* fBodyAccJerk-XYZ
* fBodyGyro-XYZ
* fBodyAccMag
* fBodyAccJerkMag
* fBodyGyroMag
* fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

* mean(): Mean value
* std(): Standard deviation


Addictionally there are data that identifies the subject id and the activity:
* Subject
* Activity


### Steps taken by the `"run_analysis.R"` script:

An order of code is not exactly the same as specified in the project description, but the actions and the results are exactly the same. 

The script does the following:

1. Reading in the test set and the training set with the descriptive variable names. Also the subject and activity ids:
    * Reading the test and the training sets with the descriptive variable names.
    * Adding to the data sets the id numbers of activities.
    * Adding to the data sets the id numbers of subjects.
    
    As a result you have two data frames one for test data, other for train data, each with variables and also subject and activity ids.
    
2. Merging the test and the training data sets to one data set. 

    As a result you have a data frame called data.set with 10299 obs. of 563 variables.
    
3. Using descriptive activity names to name the activities in the data set.

    In this step the activity id is replaced by the activity name.
    There are 6 different activity names: walking, walking_upstairs, walking_downstairs, sitting, standing, laying.

4. Extracting only the measurements on the mean and standard deviation for each measurement. 

    Mean and standard deviation variables are extracted by the function `"grep"`, also the information about the activity and the subject is added.
    
    According to a variables description from the original source the mean and standard deviation variables are those with thie part of a name like:
    * mean(): Mean value
    * std(): Standard deviation

    That means that as a result we have an extracted.data.set with 10299 obs of 68 variables (66 variables with mean and stdv plus the subject and activity)

5. Creating a second, independent tidy data set with the average of each variable for each activity and each subject. 

    This step is achieved by melting the extracted data set by "Activity" and "Subject" an then using the function `"dcast"` with the mean as the aggregator function.
    
    Melt the dataset by specifying activity ID, name and subject ID as the only ID variables.


6. Saving the result in the `"tidy_data_set.txt"`

