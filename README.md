![images](https://github.com/user-attachments/assets/98075f6a-8f92-45e6-9494-6afa31b93fbf)

## Introduction
Ensuring the efficient management of patients waiting is crucial for any healthcare practice. It's a well-known frustration when you must stay at the hospital for minutes or even hours to see a doctor or specialist. Every year, millions of patients are placed on waitlists. A hospital waitlist is a list of patients who are awaiting treatment or admission to the hospital. Several reasons are responsible for this including the lack of beds, absence of a specialist, surgical procedure, etc.
My job is to analyse the healthcare dataset for three patient groups. This will provide insights into how the waitlist varies between specialities, patient types, and age groups.
## Problem Statement
The hospital management is worried about the massive number of patients waiting for medical services. The stakeholders seek to understand how the waitlist varies. As a Data Scientist, I aim to analyse the given healthcare dataset and provide information and insights for efficient management of patients waiting at the hospital.
## Project objectives:
1.	To track the current status of the patient waiting list
2.	To analyse the historical monthly trend of waiting lists in the Inpatient and Outpatient categories.
3.	To provide detailed specialty-level and age profile analysis.
##### Metrics Required
-	The average and median waitlist.
-	The current total waitlist.
## Data collection and scop
The management provided the dataset. The file contains 4 CSV tables for Inpatient and Outpatient respectively. The Inpatient data was further categorized into Inpatients or Day Cases. The scope of the data was from January 2018 to March 2021.
## Data transformation and modelling
After a thorough check of the datasets, the rows are the same for both Inpatient and Outpatient tables. Also, the column headings are almost the same except for one incomplete nomenclature and one missed column due to the nature of the dataset – which I fixed before appending the two tables using Power BI. The new table was renamed, and the two tables (Inpatient and Outpatient) were hidden.
The speciality mapping CSV file was imported and promoted column headers. I created a relationship between the new table and the mapping speciality table.
## Data visualization blueprint
A discussion was held on how the dashboard will look. A sketch of the dashboard was done. 
## Data Analysis
I created two pages in Power BI: 
-	A summary page
-	A detailed/Granular page
## Summary page
This contains:
- 1.	Total waitlist comparison
I used a card that shows the total current month's waitlist vs the total previous month's waitlist. I created a new metric to make this field dynamic. I used DAX and created new measures:
-	Last Month Waitlist = CALCULATE(SUM(All_Data[Total]),All_Data[Archive_Date] = MAX(All_Data[Archive_Date])) + 0
-	PY Latest Month Waitlist = CALCULATE(SUM(All_Data[Total]),All_Data[Archive_Date] = EDATE(MAX(All_Data[Archive_Date]), -12)) + 0
- 2.	Average vs. Median Toggle buttons
There were outliers in the data, so the average alone is not enough to provide insights, we need the median. I created two slicers (Average and Median) and two new DAX measures for the Average Waiting List and Median Waiting List as shown below:
Average Waitlist = AVERAGE(All_Data[Total])
Median Waitlist = Median(All_Data[Total])
We need one more measure to help us interact with the slicer buttons:
Avg/Med Waitlist = SWITCH(VALUES('Calculation Method'[Calc Method]), "Average", [Average Waitlist], "Median", [Median Waitlist])
- 3.	Donut chart that provides insight on case type split and the overall by average or median
- 4.	Stacked column chart to show the relationship between the Time Band and each Age profile
- 5.  Create a Top 5 speciality list using a multi-row card, based on Avg/Med waitlist
- 6. Created separate visuals for waiting list trends for inpatients/case day vs. outpatients
## Detailed page
I created a matrix of the total patient wait list using Case_Type, Age_Profile, Time_Band, Specialty, and Archive_Date.
## Sharing the Insights
-	The number of people on a waitlist has increased dramatically since the previous year (640K last year vs. 709K for the current year).
-	Most patients on a waitlist are outpatients.
-	The highest waitlist periods are between 0 to 3 months and 18+ months, based on the median waitlist.
-	Most patients on the waiting list are between 16 to 64 years of age. 
-	The waitlist for Inpatients and Day Cases has remained steady over the past few years, however, a minimal crease was observed for the day cases around March 2020.
-	Compared with the number of inpatients and day cases, the number of Outpatients waitlist continued to steadily increase over the same period.
-	The top 5 specialties based on the median waitlist are: Accident & Emergency, Dermatology, Clinical Genetics, Cardiology, and Pain Relief.
## Recommendation
The hospital management and stakeholders should prioritise the top five specialities. This might include hiring more health workforce and procuring equipment including beds to expedite operations. 
