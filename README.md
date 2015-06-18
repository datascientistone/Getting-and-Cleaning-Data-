Course assignment for Getting and Cleaning Data in R course
The script run_analysis.R takes the Human Activity Recognition Using Smartphones Dataset, which contains data from motion monitors on Smartphones, and produces a tidy dataset of summary statistics.

Each subject in the study performed a series of different activities while wearing a Smartphone. Activities were WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, and LAYING. Data from the accelerometer was summarised in a number of ways to produce a large set of features to describe each activity (see codebook.md for details). The dataset is divided into a 'training' and a 'test' dataset.

The script run_analysis.R first loads in data for the 'test' dataset, starting with the raw feature vector data, then a single column of subject data, and lastly a single column of activity code data. It merges these data by binding the columns together into one data.frame for further analysis. This process is then repeated for the 'training' dataset.

The two datasets are then merged together by binding their rows into one data.frame. This is possible because the order of the columns is the same in both datasets. The script then names the columns with informative variable names, which are drawn from a text file features.txt, which has a list of all the original variable names.

Next, the script loads in a file which contains the activity codes, and a descriptive name for those codes (activity_labels.txt). This is used to replace the activity codes in the dataset with the more descriptive names. This is accomplished using a subsetting approach, which works because the activity codes are integers from 1-6, which corresponds to their row in the label file.

Lastly, the script pulls out only the variables of interest in this assignment (means and standard deviations), before calculating their means for each subject and activity combination.

The mean and standard deviation variables are selected using the grep() function with a regular expression. The regular expression finds all column names that contains either "-mean()" or "-std()". The trailing "()" is included to exclude variable names which have meanFreq() in the name, which are not of interest here.

The means by subject and treatment are calculated using the dplyr package, using the group_by() and summarise() functions. group_by creates a data object which indexes the desired groupings. summarise applies any function to each subset of the data implied by the grouping index, and returns the result in a data.frame. The %.% operator is also part of the dplyr package and essentially is used to "pipe" the results of one function into the next without requiring an intermediate variable. The %>% operator from the magrittr package does the same thing for more general use.

The resulting data.frame has 68 columns. The first column refers to the subject being summarized, the second column refers to the activity being summarised. The remaining 66 columns are the means for each of the 68 mean and standard deviation variables in the original dataset.

Lastly, the script saves the data.frame to a csv file, which was submitted as part of this assignment.
