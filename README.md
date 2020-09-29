# School_District_Analysis

## Overview of the school district analysis:
A chief data scientist for a city school district requested help with anlayzing student funding and standardized testing results to find performance trends and patterns.  Specifically, the deliverables requested were as follows:

   1. A high-level snapshot of the district's key metrics
   2. An overview of the key metrics for each school
   3. Tables presenting each of the following metrics:
        * Top 5 and bottom 5 performing schools, based on the overall passing rate
        * The average math score received by students in each grade level at each school
        * The average reading score received by students in each grade level at each school
        * School performance based on the budget per student
        * School performance based on the school size 
        * School performance based on the type of school
   4. Comparison of each metric after removing altered test scores for Freshman at Thomas High School
        
## Resources:
- Data source: schools_complete.csv & students_complete.csv
- Software: Python 3.8, Anaconda Navigator (anaconda3), Jupyter Notebook (anaconda3)

## Analysis Results:

- ***District Summary*** - The results of the district summary did not change after removing the altered test scores from the data.<br />
  | District Summary |
  |:------------------------|
  |![District Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/District%20Summary.png)|
 
- ***School Summary*** - The school summary results changed for the math scores, reading scores and % passing values for Thomas High School only.  Removing the altered scores actually increased their passing percentages by a small amount (less than 1%).

  | Original School Summary | Revised School Summary |
  |:------------------------|:-----------------------|
  |![Per School Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Per%20School%20Summary.png) | ![Revised Per School Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Per%20School%20Summary.png) |

- ***School Rankings*** - Removing the altered scores did not affect the rankings of the top five and bottom five schools based on overall passing percentage.  Thomas High School was the 2nd top school in both the original and the revised analysis.

   |Top Five Schools by % Overall Passing |Bottom Five Schools by % Overall Passing|
   |:------------------------|:-----------------------|
   |![Top Five Schools](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Top%20Five%20Schools.png)|![Bottom Five Schools](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Bottom%20Five%20Schools.png)

- ***Math Scores by Grade*** - Math scores by grade were not affected by removing the altered scores, except for the 9th grade at Thomas High School whose scores were removed.
     
  | Original Math Scores by Grade | Revised Math Scores by Grade |
  |:------------------------|:-----------------------|
  |![Math Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Math%20Scores%20by%20Grade.png) | ![Revised Math Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Math%20Scores%20by%20Grade.png) |
     
- ***Reading Scores by Grade*** - Reading scores by grade were not affected by removing the altered scores, except for the 9th grade at Thomas High School whose scores were removed.
  
  | Original Reading Scores by Grade | Revised Reading Scores by Grade |
  |:------------------------|:-----------------------|
  | ![Reading Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Reading%20Scores%20by%20Grade.png) | ![Revised Reading Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Reading%20Scores%20by%20Grade.png) |
      
- ***Scores by School Spending*** - Results based on school spending were not affected by removing the altered scores.
  | Scores by School Spending |
  |:------------------------|
  |![Results by Spending](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20Spending.png)|
   
- ***Scores by School Size*** - Results based on school size were not affected by removing the altered scores.
   
  | Scores by School Size |
  |:------------------------|
  |![Results by School Size](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20School%20Size.png) |
   
- ***Scores by School Type*** - Results based on school type were not affected by removing the altered scores.
  
  | Scores by School Size |
  |:------------------------|
  |![Results by School Tyoe](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20School%20Type.png)|

## Explanation of Analysis:


## Summary: Summarize four major changes in the updated school district analysis after reading and math scores for the ninth grade at Thomas High School have been replaced with NaNs.
