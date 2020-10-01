# School District Analysis

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
The following deliverables were obtained from the analysis both prior to replacing the altered 9th grade math and reading scores and after replacing the scores with NaN's.

- ***District Summary*** - Below is the high-level snapshot of the district's key metrics. The results of the district summary did not change after removing the altered test scores from the data.<br />
  | District Summary |
  |:------------------------|
  |![District Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/District%20Summary.png)|
 
- ***School Summary*** - The school summary shows an overview of the key metrics for each school in the district. The school summary results changed for the math scores, reading scores and % passing values for Thomas High School only.  Removing the altered scores actually increased their passing percentages by a small amount (less than 1%).

  | Original School Summary | Revised School Summary |
  |:------------------------|:-----------------------|
  |![Per School Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Per%20School%20Summary.png) | ![Revised Per School Summary](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Per%20School%20Summary.png) |

- ***School Rankings*** - The following tables show the top five and bottom five ranking schools based on overall passing percentage (% of students who passed both math and reading).  Removing the altered scores did not affect the rankings of the top five nor the bottom five schools.  Thomas High School was the 2nd top school in both the original and the revised analyses.

   |Top Five Schools by % Overall Passing |Bottom Five Schools by % Overall Passing|
   |:------------------------|:-----------------------|
   |![Top Five Schools](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Top%20Five%20Schools.png)|![Bottom Five Schools](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Bottom%20Five%20Schools.png)

- ***Math Scores by Grade*** - The table below shows the math and reading scores for each school broken down by grade levels.  Math and reading scores by grade were not affected by removing the altered scores, except for the 9th graders at Thomas High School, whose scores were removed.
     
  | Original Math Scores by Grade | Revised Math Scores by Grade |
  |:------------------------|:-----------------------|
  |![Math Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Math%20Scores%20by%20Grade.png) | ![Revised Math Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Math%20Scores%20by%20Grade.png) |
     
  | Original Reading Scores by Grade | Revised Reading Scores by Grade |
  |:------------------------|:-----------------------|
  | ![Reading Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Reading%20Scores%20by%20Grade.png) | ![Revised Reading Scores by Grade](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Revised%20Reading%20Scores%20by%20Grade.png) |
      
- ***Scores by School Spending*** - When comparing school performance based on the budget per student, the results showed that schools who had a smaller budget actually had higher overall passing percentages while schools with a larger budget had lower overall passing percentages. Results based on school spending were not affected by removing the altered scores.
  | Scores by School Spending |
  |:------------------------|
  |![Results by Spending](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20Spending.png)|
   
   - ***Scores by School Size*** - Comparing the school performance based on the school size, the data showed that medium sized schools (1000-2000 students) performed best while large schools (2000-5000 students) performed worst.  Results based on school size were not affected by removing the altered scores.
   
  | Scores by School Size |
  |:------------------------|
  |![Results by School Size](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20School%20Size.png) |
   
- ***Scores by School Type*** - When comparing school performance based on school type, charter schools had an overall passing percent of 90% while district schools only had 54%. Results based on school type were not affected by removing the altered scores.
  
  | Scores by School Type |
  |:------------------------|
  |![Results by School Type](https://github.com/whitneylosinski/School_District_Analysis/blob/master/Resources/Result%20by%20School%20Type.png)|

## Summary: 
While there weren't many changes to the outcomes of the final analysis results when comparing school performance, there were some key changes that took place within the analysis itself after the altered math and reading scores for the 9th graders at Thomas High School were replaced with NaN's.  The four major changes are as follows.

  1. ***Recalculating Passing Percentages*** - Because some of the reading and math scores were replaced with NaN's, the total student count needed to be updated to get accurate passing percentages.  To do this, a `.loc()` function was used in combination with the `.count()` function to count the number of null (NaN) reading score entries for 9th graders.  The overall student count was then found by using the `.count()` function to count the total number of student ID's.  Subtracting the null entries for 9th graders from the overall student count resulted in the revised student count that would be used to calculate the passing percentages as shown below.
      
      ```py
      # Step 1. Get the number of students that are in ninth grade at Thomas High School.
      # These students have no grades. 
      THS_fresh_student_count = school_data_complete_df.loc[school_data_complete_df["reading_score"].isnull()].count()["Student ID"]

      # Get the total student count 
      student_count = school_data_complete_df["Student ID"].count()

      # Step 2. Subtract the number of students that are in ninth grade at 
      # Thomas High School from the total student count to get the new total student count.
      revised_student_count = student_count - THS_fresh_student_count
      ```
       To find the passing percentages, conditionals were used to count the number of students with math scores greater than or equal to (>=) 70 and to count the number of students with reading scores >= 70.  These numbers were then divided by the revised student count and multiplied by 100 to calculate the passing percentages for math and reading.
      
      ```py
         # Calculate the passing rates using the "clean_student_data".
         passing_math_count = school_data_complete_df[(school_data_complete_df["math_score"] >= 70)].count()["student_name"]
         passing_reading_count = school_data_complete_df[(school_data_complete_df["reading_score"] >= 70)].count()["student_name"]
      
         # Step 3. Calculate the passing percentages with the new total student count.
         revised_passing_math_percentage = passing_math_count / revised_student_count * 100
         revised_passing_reading_percentage = passing_reading_count / revised_student_count * 100
      ```
       Similar conditionals and calculations were used to find the overall passing percentage but this time, the conditional was set to count the number of students with both math AND reading scores >= 70
   
      ```py
      # Calculate the students who passed both reading and math.
      passing_math_reading = school_data_complete_df[(school_data_complete_df["math_score"] >= 70)
                                               & (school_data_complete_df["reading_score"] >= 70)]

      # Calculate the number of students that passed both reading and math.
      overall_passing_math_reading_count = passing_math_reading["student_name"].count()


      # Step 4.Calculate the overall passing percentage with new total student count.
      revised_overall_passing_percentage = overall_passing_math_reading_count / revised_student_count * 100
      ```
      
   2. ***Recalculating the Passing Students from Thomas High School*** - Because the data for Thomas High School changed when the altered scores were removed.  All of the average scores for math and reading needed to be recalculated for the 10th, 11th and 12th grades.  To do this, the `.loc()` and `.notnull()` functions were used to look up all of the rows in the school summary with the school name listed as Thomas High School and a math score with any value except null (NaN).  The `.count()` function was then used to count the number of student ID's for those rows.  This provided the total number of 10th-12th graders at Thomas High School.  
   
      ```py
      # Step 5.  Get the number of 10th-12th graders from Thomas High School (THS).
      THS_student_count = school_data_complete_df.loc[((school_data_complete_df["school_name"] == "Thomas High School")&(school_data_complete_df["math_score"].notnull()))].count()["Student ID"]
      ```
      Next, the `.loc()` function was used with a conditional to find the rows with the school name listed as Thomas High School and a math score >= 70.  Again, the `.count()` function was used to count the number of student names in those rows, providing the number of students who passed math from Thomas High School.  The same process was used to find the number of students passing reading from Thomas High School.
      
      ```py
      # Step 6. Get all the students passing math from THS
      THS_passing_math_count = school_data_complete_df.loc[(school_data_complete_df["school_name"] == "Thomas High School")&(school_data_complete_df["math_score"] >= 70)].count()["student_name"]
      
      # Step 7. Get all the students passing reading from THS
      THS_passing_reading_count = school_data_complete_df.loc[(school_data_complete_df["school_name"] == "Thomas High School")&(school_data_complete_df["reading_score"] >= 70)].count()["student_name"]
      ```
      To calculate the number of students passing both reading and math from Thomas High School, the `.loc()` and `.count()` functions were combined with two conditionals to find count the number of rows with both the school name listed as Thomas High School, math scores >=70 AND reading scores >=70.
      
      ```py
      # Step 8. Get all the students passing math and reading from THS
      THS_overall_passing_count = school_data_complete_df.loc[(school_data_complete_df["school_name"] == "Thomas High School")&(school_data_complete_df["math_score"] >= 70)&(school_data_complete_df["reading_score"] >=70)].count()["student_name"]
      ```
      
   3. ***Recalculating Passing Percentages for Thomas High School*** - Using the new values for the passing students and the total students at Thomas High School, simple calculations were completed to find the new passing percentages for math, reading and overall.  For each calculation, the number of passing students at Thomas High School was divided by the total number of students with scores at Thomas High School and multiplied by 100 as shown below.
   
      ```py
      # Step 9. Calculate the percentage of 10th-12th grade students passing math from Thomas High School. 
      THS_passing_math_percentage = THS_passing_math_count / THS_student_count * 100
      
      # Step 10. Calculate the percentage of 10th-12th grade students passing reading from Thomas High School.
      THS_passing_reading_percentage = THS_passing_reading_count / THS_student_count * 100
      
      # Step 11. Calculate the overall passing percentage of 10th-12th grade from Thomas High School. 
      THS_overall_passing_percentage = THS_overall_passing_count / THS_student_count * 100
      ```
   
   4. ***Updating the School Summary*** - Because the passing percentages changed after being recalculated, the school summary needed to be updated for Thomas High School to reflect the correct values.  To do this, the `.loc()` function was used to find the row with an index of Thomas High School and set the passing percentages equal to their defined variable as shown below.
   
      ```py
      # Step 12. Replace the passing math percent for Thomas High School in the per_school_summary_df.
      per_school_summary_df.loc["Thomas High School","% Passing Math"] = THS_passing_math_percentage
      
      # Step 13. Replace the passing reading percentage for Thomas High School in the per_school_summary_df.
      per_school_summary_df.loc["Thomas High School", "% Passing Reading"] = THS_passing_reading_percentage
      
      # Step 14. Replace the overall passing percentage for Thomas High School in the per_school_summary_df.
      per_school_summary_df.loc["Thomas High School", "% Overall Passing"] = THS_overall_passing_percentage
      ```
      After updating the school summary, the remaining script could be carried out identically to the original script to compare school performance based on different metrics.
