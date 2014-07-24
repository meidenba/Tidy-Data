Tidy-Data
Repository for Getting and Cleaning Data.
run_analysis.R

When sourced, the script displays instuctions for running data download and processing functions. The script checks if the required R packages are installed and tries to install them if previous installation is not found.

source('./run_analysis.R')
download.data()
run.analysis()
In the case the Samsung data is already unzipped and directory with the dataset is available as UCI HAR Dataset subdirectory of the current directory, the processing function run.analysis() can be called straight away.

Processing steps

When sourced, the script chechs if the required R packages are available and proceeds to install them if they are not found
Calling download.data() downloads the zipped dataset and unarchives it.
Calling run.analysis() starts the actual data processing:
Feature vector label data is loaded from features.txt
Using regex with grepl, subset of label data for selecting desired data coluns is created.
Activity labels are loaded from features.txt
Activity labels (id->label) and selected features (id->label) are given as parameters to function which loads the training or test dataset, based on the type value given also as a parameter.
Paths to data files are created based on type parameter
Data files are loaded. Feature vector data is filtered using ids of the selected features.
Activity and subject id data are loaded
Feature vector data is renamed using the names of selected features
Activies and subjects are given labels using factor levels of activity and subject id data.
Finally, processed dataset is returned.
(The previous processing is repeated to both training and test datasets.)
Training and test datasets are merged using rbind() and converted to data.table to make it easier to do groupwise operations in the following step
Mean is calculated for all variables for each activity and subject
Variable names are loaded to separate vector and tidied to follow camelCase-convention.
New names are applied to dataset
Tidy dataset is written to disk.
