# matplotlib-challenge
## Matplotlib assignment - Data Analytics Bootcamp

### Setting up folders in Github

1. Created a new repository for the project called matplotlib-challenge in Github. Cloned the repository to the local computer.

2. Created new directory within pandas-challenge called Pymaceuticals

3. Inside the new directory, created a pymaceuticals_starter.ipynb file and a folder data to hold the two csv files for the studies Mouse_metadata.csv and Study_results.csv.

4. Executed the python code for each step.

### Pymaceuticals

   * Imported the pandas module.
```
import matplotlib.pyplot as plt
import pandas as pd
import scipy.stats as st
```
  * Read the csv files into dataframes and merged the 2 files using field 'mouse_study_merge'
```
mouse_metadata_path = "data/Mouse_metadata.csv"
study_results_path = "data/Study_results.csv"

# Read the mouse data and the study results
mouse_metadata = pd.read_csv(mouse_metadata_path)
study_results = pd.read_csv(study_results_path)

# Combine the data into a single dataset
mouse_study_merge = pd.merge(study_results, mouse_metadata, on = 'Mouse ID', how = 'outer')
```

# Cleaning Up the Dataset

* Calculated the number of mice in the original merged dataframe and found it be 249 mice

* Determined the mouse with duplicate Mouse_ID and Timepoint using the pandas 'duplicated' method. The duplicate Mouse ID is 'g989'.

* Retrieve all the 13 records for the Mouse ID 'g989' using loc. Remove all the 13 rows for the duplicate Mouse ID and create a new dataframe mouse_study_clean.

* Calculated the number of mice in the cleaned dataframe with the duplicate mouse deleted and found it be 248 mice.

# Generating Summary Statistics

* Grouped the clean Dratframe by Drug Regimen and calculated
	* Mean
	* Median
	* Variance
	* Standard Deviation
	* SEM (Standard Error of Mean)
* Created a summary dataframe with all the above details for each Drug regimen using mean(), median(), var(). std() and sem().

* Generated a new summary dataframe using the aggregate method to obtain the above statistics measures.

# Bar and Pie Charts

* Used the above dataframe grouped by Drug Regimen to obtain the sum of timepoints for all mice tested for each drug regimen

	* Created a bar plot using pandas method .plot() with drug regimens plotted along the x-axis and total timepoints plotted           against the y-axis.
	* Repeated the same to generate the same bar plot for drug regimen vs total timepoints using matplotlib pyplot.bar().

* Grouped by the cleaned datframe mouse_study_clean by Mouse_ID to obtain the number of male and female mice using the unique() method.

	* Plotted a scatter plot using pandas with .plot() to show the male vs female mice percentage.
	* Plotted the same scatter plot using matplotlib using pyplot.scatter() to show male vs female mice percentage.

# Quartiles, Outliers and Boxplots

* Grouped the clean dataframe mpuse_study_clean by Mouse_ID and Timepoint to obtain the maximum timepoint for each mouse with all the other details.

* Put specific drug regimen treatments in a list - 'Capomulin', 'Ramicane', 'Infubinol', 'Ceftamin'

* Created empty lists for each of the four drug regimens to store the tumour volumes using loc.

* For each of the drug regimens, calculated the quartiles, lower quartile, upper quartile, Inter Quartile Range (IQR), lower boundary and upper boundary using the below formulas. Example for drug capomulin shown below. Checked for any outliers that lie outside the lower and outer boundary.
```
quartiles_capomulin = capomulin_tumor_volume.quantile([.25,.5,.75])
lowerq_capomulin = quartiles_capomulin[0.25]
upperq_capomulin = quartiles_capomulin[0.75]
iqr_capomulin = upperq_capomulin-lowerq_capomulin

lower_bound_capomulin = lowerq_capomulin - (1.5*iqr_capomulin)
upper_bound_capomulin = upperq_capomulin + (1.5*iqr_capomulin)

bool_capomulin = False
for cap in capomulin_tumor_volume:
    if (cap < lower_bound_capomulin) or (cap > upper_bound_capomulin):
        print('Outlier for drug capomulin: ' + str(round(cap),2))
        print('\n', end='')
        bool_capomulin = True
        
if bool_capomulin == False:
    print('No potential outliers for drug capomulin')
    print('\n', end='')
```
* Only one outlier was found for drug infubinol.

* Generated a quantitative summary dataframe with all the above calculations for each drug and also printed details of the outlier.

* Genrated a box plot for each of the 4 drug regimen and displayed the outlier for drug Infubinol. 

# Line and Scatter Plots

* Selected only records for mice treated by druf Capomulin/

* Selected a specific mouse = 'w914' being treated by drug Capomulin.

* Located in the Mouse ID in the dataframe using loc and obtained timepoint and tumor volume for mouse 'w914'.

* Plotted a line chart to show the tumor volume vs time plot for the mouse 'w914'.

* Grouped the Capomulin datframe by Mouse ID to obtain average tumor volume for each mouse.

* Plotted a scatter plot of average tumor volume against mouse weight.

# Correlation and Regression

* Using linregress from Scipy, calculate the regress values for the above scatter plot of average tumor volume vs mouse weight.

* Obtain the slope, intercept and r-values.

* Calculate the line equation as y = slope * x + intercept

* Plot the best fit line using pyplot() and display the best fit line equation using annotate. The line equation for this plot is 
y = 0.95x+21.55.

* Calculate the r-square value by squaring the r-value (correlation coefficient). It is found to be 0.71.
 
  