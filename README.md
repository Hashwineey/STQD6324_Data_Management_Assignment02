# STQD6324_Data_Management_Assignment02

## Introduction
Hi and Welcome back! 
This project explores flight performance in the US for the year 2004, focusing on flight delays and cancellations. Using Python, SQL (Hive), and Plotly for visualizations, the analysis identifies:
+ Airlines, airports, routes, and flights with the highest delays or cancellations
+ Patterns over time (month, time of day)
+ Insights into which factors correlate with poor performance

The goal is to help stakeholders in the airline industry make data-driven operational decisions to improve punctuality and reduce customer disruptions using analysis of past data.

## Overview of Project Flow
![Project_Flow](https://github.com/user-attachments/assets/ff09ccd9-e97d-47ed-aca8-ddfc4d339fa3)

## Data Collection
The dataset was obtained from [Kaggle](https://www.kaggle.com/datasets/wenxingdi/data-expo-2009-airline-on-time-data/data?select=2004.csv). As mentioned earlier, the 2004 dataset was used for this project.
[US DOT Bureau of Transportation Statistics (BTS)](https://www.transtats.bts.gov/Fields.asp?P74_e19=-LM&P74_P1y=&n22yB_4n6r=&5146_p1y7z0=&frn4pu_Y11x72=&sv0q=&5146_14qr4=) was also referred to get the meaning of the abbrevations in the dataset.

## Data Preparation
Since the data from Kaggle is too large to be uploaded to Hive, the dataset was split into two distinct datasets: df_delay_2004.csv and df_cancelled_2004.csv. 
df_delay_2004.csv contains all the data of delayed flights in 2004 and df_cancelled_200.csv contains all the data of cancelled flights in 2004.
You may refer to the "Data Cleaning.ipynb" file for the data preparation steps.

## Upload Data to Hive
Now that we have two cleaned datasets, it is time to upload them to Hive in order for us to analyse the datasets.

For that, first, the CSV files were copied from the local drive to the hdp-sandbox.
![Local_to_Sandbox](https://github.com/user-attachments/assets/7f4a8a1b-b9ac-47b2-b1fd-f192354707e2)

Then, the files were uploaded to HDFS
![HDFS Upload](https://github.com/user-attachments/assets/967ac06a-67bd-48e9-ab18-20417edf65f0)

Lastly, the datasets were mapped to Hive tables that were created for these datasets. You may find the codes to create table in Hive in "Create_Hive_Table.txt" file. 
![Hive_Table](https://github.com/user-attachments/assets/f0167863-2dc8-4dcc-92cf-6c58f6fe6837)

## Data Analysis and Data Visualization
Once the datasets are uploaded to Hive, Jupyter Notebook was then connected to Hive to make Data Analysis and Data Visualization easier.














