# run_analysis
This the script, readme, and codebook for the Coursera course "Getting and Cleaning Data" course project

This readme serves to explain the necessary conditions of my script:

1) All the samsung files were in the working directory, so that they could be called just by their file name and then would be loaded into R.

2) I used the dplyr package in my script.  This requires the the dplyr package is installed before the script is run. I did not inlcude a "install.packages("dplyr") line in my code, but I did include a "library(dplyr)" line; I was told it is bad etiquette to force someone to download something from the internet if they try and run a script.

Below is the explanation of my script.  There are also notes in the actual script which may be easier to read.

I aggregated the data by first combining the train data and test data row-wise so the two sets of data sat "on top" of 
one another in a single dataframe.  

I then loaded the features txt file and used those features to rename the train/test dataframe variables.  
I made the assumption that the the feature names and the train/test data were in the same order, 
meaning that the first feature had measurements in the first column of the train/test data and so on.
	Note:  I had to assume this because I was not part of the original experiment, and I needed this step to more forward; 
	I think the original data team mainted the order of the variables in the features txt file and the train/test data.

The next part of the assignment had me select only the features that were mean and standard deviation for each measurement. 
I interpreted this as meaning, find and select features that had "mean()" or "std()" in their name.
	Note: I did not include measurements of meanFreq(); I did not think that the meanFreq was the same as the mean() and std() of the measurements (I could be wrong though).
	Note2: I renamed the variables by removing parenthesis, dashes, underscores, and made the variable names one continuous string; this made the variables easier to use in R and dplyr and easier to read, in my opinion.
	Note3: I did not do any renaming after that.  I thought that this project could be a step in a larger goal of data tidying; I wanted to maintain as much of the original name as possible because of this.

After that, I loaded the train and test Subjects (numbered 1-30) and combined them row-wise (so they sat on top of one another).  I also loaded the train and test Activities (numbered 1-6) and combined them row-wise (so they sat on top of one another)

At this point, the Activites were listed as numbers; these numbers corresponded to the actual activity:

1-Walking
2-Walking_Upstairs
3-Walking_Downstairs
4-Sitting
5-Standing
6-Laying

I used a for loop to rename the activities so it showed the respective activity name (instead of the number).

Finally, with everything labeled correctly, I combined the features, Subjects, and Activities column wise.  Almost done!

I used the package dplyr and the function group_by to group the data by Subject and then by Activity.  
This means that I can find the mean of feature variables first by Subject then by Activity

Finally, I used dplyr and the summarise_each function to find the means of each of the feature variables.  
This means that each Subject had 6 Activites, and summarise_each found the means of all of the features associated to each 
Subject and Activity.

And that's it!
