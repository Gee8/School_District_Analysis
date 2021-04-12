# School_District_Analysis

## Overview of the school district analysis: Explain the purpose of this analysis.
Using `students_complete.csv` and `schools_complete.csv`, we were able to draw an analysis on each school's student performance on reading and math scores. The information collected allowed us to see the percentage of students who passed reading, math and both. We were also able to see how students performed based on the funding each school alloted per student. Before we performed the analysis, prefixes and suffixes such as Dr. were removed from the students names. The analysis was done on the entire data set, but due to a suspicion of cheating among 9th grade students at Thomas High School, these grades we're removed and the analysis was repeated. The original analysis containing all students is located in the Module Code section and the analysis without the 9th grade Thomas High School students is located in the Challenge Code section. Both of these codes can be found within `PyCitySchools_Challenge.ipynb`.

## Results: Using bulleted lists and images of DataFrames as support, address the following questions.

- How is the district summary affected?
  - The following images depict the `district_summary_df` for the original and modified codes, respectfully. We did not change the total number of students, but when calculating the averages and percentages, we are leaving out the 9th grade Thomas High School students. We removed the 9th grade students by using the following: `student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "reading_score"] = np.nan`. After removing the 9th grade scores, we see that the Average Math Score, % Passing Math, % Passing reading and % Overall Passing have been slightly lowered.

  <img width="500" alt="district summary df before" src=".\Resources\district summary df before.png">
  <img width="500" alt="district summary df after" src=".\Resources\district summary df after.png">

- How is the school summary affected?
  - The following code and images depict the `per_school_summary_df` before and after we replace the Thomas High School values. To replace the values, we used the .loc function to replace the old values with the newly calculated values after we removed the scores from the 9th grade students. To change these values we used the following code:

    `per_school_summary_df.loc["Thomas High School", "% Passing Math"] = ths_passing_math_not_ninth_percentage`

    `per_school_summary_df.loc["Thomas High School", "% Passing Reading"] = ths_passing_reading_not_ninth_percentage`

    `per_school_summary_df.loc["Thomas High School", "% Overall Passing"] = ths_overall_passing_not_ninth_percentage`

    The following is the change for Thomas High School in the `per_school_summary_df`.

    <img width="500" alt="thomas high school before" src=".\Resources\thomas high school before.png">
    <img width="500" alt="thomas high school after" src=".\Resources\thomas high school after.png">

    Although the Total Students remains unchanged between the two dataframes, this is to show that there were in fact that many students in total. While all students were counted towards Total Students, the percentages were found using `new_student_count = student_count - ths_student_count` where `student_count` is the entire student population, and `ths_student_count` is the number of 9th grade students that we replaced their grades with NaN. To find the number of students whose grades we removed, we used:
    `ths_student_count = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "Student ID"].count()`.
    By using `new_student_count` to find the percentages, we can find accurate pass rates without ignoring the existance of the 9th graders.

  
- How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
  - Before we had replaced the ninth graders' math and reading scores, the percent passing reading, math, and overall were substantially below the other schools. Before making the change, Thomas High School ranked 8th by % Overall Passing. After replacing the scores, Thomas High School ranked second by % Overall Passing.
  
- How does replacing the ninth-grade scores affect the following:
  - Math and reading scores by grade
    - The math and reading scores by grade are generally unaffected, except after removing the 9th graders' results from Thomas High School, we get a NaN in place of the score for each reading and math. Shown below is the before and after results for the `math_scores_by_grade` and `reading_scores_by_grade`, respectively.

    <img width="300" alt="math scores by grade before" src=".\Resources\math scores by grade before.png">
    <img width="300" alt="math scores by grade after" src=".\Resources\math scores by grade after.png">


    <img width="300" alt="reading scores by grade before" src=".\Resources\reading scores by grade before.png">
    <img width="300" alt="reading scores by grade after" src=".\Resources\reading scores by grade after.png">
  
  - Scores by school spending
    - Since Thomas High School falls within the $630-644 spending range per student, our `spending_summary_df` is only affected within that range. Our final `spending_summary_df` is formatted to one decimal for the averages, and to the nearst percent for the % Passing columns. After this formatting, the values are identical, but if we look at the `spending_summary_df` before formatting, we can see there is a slight change. Show below is the `spending_summary_df` for the $630-644 range before and after removing the 9th graders' scores for Average Math Score, Average Reading Score, % Passing Math, % Passing Reading, and % Overall Passing before formatting.

    <img width="500" alt="spending ranges before" src=".\Resources\spending ranges before.png">
    <img width="500" alt="spending ranges after" src=".\Resources\spending ranges after.png">
  
  - Scores by school size
    - As a medium sized school, Thomas High School falls within the 1000-2000 student range. Like the scores by school spending, the difference between including the 9th grade scores or not is too small to affect the outcomes after formatting the dataframe. To see the change we have to look at our dataframes before formatting. After formatting the `size_summary_df`, they are identical. Shown below is the `size_summary_df` before and after removing the 9th grade scores before formatting. The affected row is the Medium (1000-2000) row.

    <img width="500" alt="size_summary_df before" src=".\Resources\size summary df before.png">
    <img width="500" alt="size_summary_df after" src=".\Resources\size summary df after.png">
  
  - Scores by school type
    - Just like our `spending_summary_df` and `size_summary_df`, the differences between retaining and removing the 9th grade scores within our `type_summary_df` is too small to make a difference after formatting. To see the differences we must look at our `type_summary_df` before formatting. Thomas High School is a Charter School, so that is our affected row. Shown below is the `type_summary_df` before and after removing the 9th grade scores before formatting.

    <img width="500" alt="type_summary_df before" src=".\Resources\type summary df before.png">
    <img width="500" alt="type_summary_df after" src=".\Resources\type summary df after.png">
  
## Summary: Summarize four major changes in the updated school district analysis after reading and math scores for the ninth grade at Thomas High School have been replaced with NaNs.
The largest impact of replacing the ninth grade math and reading scores at Thomas High School was within the `per_school_summary_df`. Without replacing the ninth grade scores with NaNs, Thomas High School passing rates of 66.9, 69.7 and 65.1 for math, reading and overall, respectively. When we replaced the ninth grade scores with NaNs, these scores improved to 93.2, 97, and 90.6. The difference is significant because we are affecting the entire population we are looking at. When looking at metrics that include all schools, the NaN replacement made a significantly smaller difference. As noted above, scores by school spending, size and type had changes so negligable we needed to check the differences before formatting. Although these changes weren't large enough to change the formatted dataframes, the replacement of the ninth graders' math and reading scores with NaN would have changed our final dataframes had we formatted them with just one more decimal point.
