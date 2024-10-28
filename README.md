# Evaluating Uber and Lyft Ride Fares in NYC
## Contents
### Goal Statement
The goal of this project is to observe whether ride fares for Lyft and Ubers in New York share similar ride fare trends over time.
### Research Question
Is there a significant correlation between the average total passenger fare paid each month for Uber and average total passenger fare paid each month for Lyft in New York City?
## Section 1: Software and Platform
This project utilized Python, Jupyter Notebook, and GitHub. Both a Mac and Windows computer were used for this project, but this project can run on any platform that has the required installations.  <br />
The packages needed for this project include pandas, pyarrow, and os. <br /><br />
The data was provided as a collection of PARQUET files sorted by month and year. The files were read into a pandas dataframe using pyarrow.parquet. <br />
## Section 2: map of documentation
```bash
ds-nyc-ride-services-proj
├── DATA
│   ├── cleaned-data.csv
│   └── source data
├── OUTPUT
│   ├── Lyft-basefare-density.png
│   ├──Lyft-basefare-box.png
│   ├──Lyft-basefare-time.png
│   ├──Lyft-monthly.png
│   ├──Lyft-totalfare-box.png
│   ├──Lyft-totalfare-density.png
│   ├──Lyft-totalfare-time.png
│   ├──lyft-yearly.png
│   ├──Uber-basefare-box.png
│   ├──Uber-basefare-density.png
│   ├──Uber-basefare-time.png
│   ├──Uber-monthly.png
│   ├──Uber-totalfare-box.png
│   ├──Uber-totalfare-density.png
│   ├──Uber-totalfare-time.png
│   ├──uber-yearly.png
├── SCRIPTS
│   ├── cleaning_data.ipynb
│   └── data_analysis.ipynb
├── LICENSE.md
└── README.md
```
## Section 3: instructions for reproducing results
### Acquiring the Data:
From the link in source data, we downloaded the PARQUET file “High Volume For-Hire Vehicle Trip Records” which has records of data from every single Uber and Lyft ride in NYC from September 2019 to July 2024 [1]. Because the original data file is too large to upload in Github, we have provided the link to access the dataset in the file “source data” [1]. <br /><br />
After downloading the original PARQUET file, we added the file to the scripts folder and ran the script “cleaning_data.ipynb”. This script includes a method creating_clean_data that goes through the original data file and calculates the average Uber and Lyft data for each month. We also create a new field called “total fare” that is the sum of the base_passenger_fare, tolls, tips, tolls, tips, sales_tax, congestion_surcharge, and airport_fee for each ride. Another method in the script is process_directory which repeats this process for each PARQUET file in the folder and results in a new dataframe.<br /><br />
This dataframe is written to a csv file called “all_fares.csv”. <br /><br />
### Analyzing the Data:
To analyze the data the script “data_analysis.ipynb” was run. The data frame was first reconfigured to reset the Month and Year columns as a Date Time variable. This was added as a column labeled “Date.” Using the LinearRegression() method, a multivariable linear regression model was created comparing the average Lyft total fare and date (the x variables) against the Uber average total fares (y variable). From there, the mean squared error, variance, standard errors of coefficients, and t statistics for each coefficient in the model were calculated. The p value for each t stats were calculated as well. The R2 value (0.9), intercept (-2909), and slope(0.88) of the model were calculated. This allows us to understand the relationship and correlation between Uber and Lyft rates. There was a significant correlation between average Uber total fares and average Lyft total fares. <br /><br />
Once this strong correlation was determined, we used the linear regression model to predict Uber total fares. A scatter plot of the actual average Uber total fares and the predicted average Uber total fares was created. <br /><br />

### References
[1]“Raw Data - TLC,” Nyc.gov, 2024. https://www.nyc.gov/site/tlc/about/raw-data.page (accessed Oct. 21, 2024).
