## Salary & Experience Across Global Industries

This project analyzes a global salary survey dataset to understand how salary and total compensation vary across industries, job roles, experience levels, education, gender, and geographic locations. The dataset was cleaned and standardized, stored in a MySQL database, and queried using SQL to extract meaningful insights. The results were exported to Excel and visualized using pivot tables and an interactive dashboard to highlight career and compensation trends.

#### Tools & Technologies

- MySQL

- Microsoft Excel

- SQL

- Pivot Tables & Charts

#### Key Insights

- Salary and compensation vary significantly across industries and job roles.

- Higher experience and education levels generally lead to increased earnings.

- Certain industries and countries consistently offer higher-paying roles.

- Additional monetary compensation plays an important role in total earnings.

#### SQL Queries:

/*1. Average Salary by Industry and Gender Compare the average salary within each industry, split by gender. This helps identify potential salary discrepancies based on gender within industries. */

select industry,Gender,round(avg(Total_Salary_USD),2) AS Average_Salary from salary_survey group by Industry,gender order by Industry,gender ;

/-----------------------------------------------------------------------------------------------------------/ /*2. Total Salary Compensation by Job Title Find the total monetary compensation (base salary + additional monetary compensation) for each job title. This can show which roles have the highest overall compensation. */

select Job_Title,round(sum(Total_Salary_USD),2) as total_salary from salary_survey group by Job_Title order by Total_Salary desc;

/--------------------------------------------------------------------------------------------------/ /3. Salary Distribution by Education Level Find the salary distribution (average salary, minimum, and maximum) for different education levels. This helps analyze the correlation between education and salary./

select Highest_Level_of_Education_Completed as Education_level, round(avg(Total_Salary_USD),2) as average_salary, round(min(Total_Salary_USD),2) as minimum_salary, round(max(Total_Salary_USD),2) as maximum_salary from salary_survey group by Education_level;

/------------------------------------------------------------------------------------------/ /* 4. Number of Employees by Industry and Years of Experience Determine how many employees are in each industry, broken down by years of professional experience. This can show if certain industries employ more experienced professionals. */

select industry , Years_of_Professional_Experience_in_Field as Experience, count(name) as no_of_employees from salary_survey group by industry,experience order by experience desc;

/----------------------------------------------------------------------------------------/ /* 5. Median Salary by Age Range and Gender Calculate the median salary within different age ranges and genders. This can provide insights into salary trends across different age groups and gender. */

select Gender,Age_Range,round(avg(Total_Salary_USD),2) as median from salary_survey group by Gender,Age_Range;

/--------------------------------------------------------------------------------------/ /*6. Job Titles with the Highest Salary in Each Country Find the highest-paying job titles in each country. This can help understand salary trends across different countries and highlight high-paying positions. */

select country, job_title, Total_Salary_USD from (select country,job_title,Total_Salary_USD, row_number() over (partition by country order by Total_Salary_USD desc) as rn from salary_survey) as ranked where rn=1 order by Total_Salary_USD desc;

/----------------------------------------------------------------------------------------------------/ /* 7. Average Salary by City and Industry Calculate the average salary for each combination of city and industry. This shows which cities offer higher salaries within each industry. */

select city,industry, round(avg(Total_Salary_USD),2) as Average_salary from salary_survey group by city,industry;

/----------------------------------------------------------------------------------------------------------/ /*8. Percentage of Employees with Additional Monetary Compensation by Gender Find the percentage of employees within each gender who receive additional monetary compensation, such as bonuses or stock options. */

select gender,round(count(Additional_Monetary_Compensation)100/ (select count() from salary_survey),2) as percentage from salary_survey group by gender order by percentage;

/*9. Total Compensation by Job Title and Years of Experience o Determine the total compensation (salary + additional compensation) for each job title based on years of professional experience. This can help highlight compensation trends based on experience levels within specific job titles. */

select Job_Title, Years_of_Professional_Experience_in_Field as Experience, round(sum(Total_Salary_USD),2) as total_salary from salary_survey group by Job_Title,experience;

/10. Average Salary by Industry, Gender, and Education Level o Understand how salary varies by industry, gender, and education level. This query can provide a comprehensive view of how multiple factors influence salary./

select industry, gender, Highest_Level_of_Education_Completed as Education_level, round(avg(Total_Salary_USD),2) as Average_Salary from salary_survey group by Industry,gender,education_level;

#### Dashboard:
