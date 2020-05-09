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
- - - 
```python 
# Calculate the Totals (Schools and Students)
school_count = len(school_data_complete["school_name"].unique())
student_count = school_data_complete["Student ID"].count()

# Calculate the Total Budget
total_budget = school_data["budget"].sum()

# Calculate the Average Scores
average_math_score = school_data_complete["math_score"].mean()
average_reading_score = school_data_complete["reading_score"].mean()
overall_passing_rate = (average_math_score + average_reading_score) / 2

# Calculate the Percentage Pass Rates
passing_math_count = school_data_complete[(school_data_complete["math_score"] > 70)].count()["student_name"]
passing_math_percentage = passing_math_count / float(student_count) * 100
passing_reading_count = school_data_complete[(school_data_complete["reading_score"] > 70)].count()["student_name"]
passing_reading_percentage = passing_reading_count / float(student_count) * 100
```

Once I created the items to the dataframe I will do some minor clean up and present the findings. 

```python
# Minor Data Cleanup
district_summary = pd.DataFrame({"Total Schools": [school_count],
                                 "Total Students": [student_count],
                                 "Total Budget": [total_budget],
                                 "Average Math Score": [average_math_score],
                                 "Average Reading Score": [average_reading_score],
                                 "% Passing Math": [passing_math_percentage],
                                 "% Passing Reading": [passing_reading_percentage],
                                 "% Overall Passing Rate": [overall_passing_rate]})

district_summary = district_summary[["Total Schools", "Total Students", "Total Budget",
                                     "Average Math Score",
                                     "Average Reading Score",
                                     "% Passing Math",
                                     "% Passing Reading",
                                     "% Overall Passing Rate"]]

district_summary["Total Students"] = district_summary["Total Students"].map("{:,}".format)
district_summary["Total Budget"] = district_summary["Total Budget"].map("${:,.2f}".format)

# Display the data frame
district_summary
```
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.431606</td>
    </tr>
  </tbody>
</table>
</div>




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
