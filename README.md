# Academy-of-Py
This project uses Python, Pandas, and Numpy to give key metrics and analysis on district wide standardized test results.

![Education](image/education.png)

In this role I have become the Data Analysts for Py city's school district. In this capacity, I will be helping the school board and mayor make strategic decisions regarding future school budgets and priorities.
I've been asked to analyze the district-wide standardized test results. I was granted access to every student's math and reading scores, as well as various information on the schools they attend. My responsibility is to aggregate the data to and showcase obvious trends in school performance.

### Prerequisites

```python 
# Dependencies and Setup
import pandas as pd
import numpy as np


# Read School and Student Data File and store into Pandas Data Frames
school_data = pd.read_csv("schools_complete.csv")
student_data = pd.read_csv("students_complete.csv")
```
- - - 

Explore the data using df.head() and df.columns to find out more about the information you are using. 

The data frames both have school names as the primary key. I will use pd.merge() method on the primary key 'school_name' to merge the two data sets and then the analysis will begin.
- - - 
```python 
# Combine the data into a single dataset
school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])
```
- - - 

District Summary

I will create a high level snapshot (in table form) of the district's key metrics, including:

  * Total Schools
  * Total Students
  * Total Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)




School Summary

Create an overview table that summarizes key metrics about each school, including:

School Name
School Type
Total Students
Total School Budget
Per Student Budget
Average Math Score
Average Reading Score
% Passing Math
% Passing Reading
Overall Passing Rate (Average of the above two)
