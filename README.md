# An Estimation for Asymptomatic Covid-19 Cases of Turkey
### A multivariate polynomial regression model

### Acknowledgments

##### This project has 2 different dataset from 2 different sources. I have prepared one of them in another project which used data from "COVID-19 Data Repository by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University", link to their repo is https://github.com/CSSEGISandData/COVID-19.

##### Second dataset is processed with the data from the Ministry of Health in Turkey 

#### Studies of 

### Problem

Republic of Turkey was one of the countries which announce only symptomatic Covid-19 cases. Yet, this policy only took about 3 months.

The Ministry referred to these numbers as "patients" rather than "cases". They started to announce asymptomatic cases once again and revealed the total case numbers in the country. 

Secondary repositories kept these numbers as if they were case numbers and this caused significant changes in the recording standards for the country. Actual case numbers are now known but we still do not have the daily increases for this gap.

![](images/graph.PNG)

### Goal of the Project

This project aims to estimate daily increases of case numbers for these days. There are several facts and data that makes it possible to build a high accurate machine learning model to solve this problem. 

These facts are:

    1. Total case numbers are known.
    
    2. This policy only took part of the total duration of the pandemic and it was in the middle. 
       We know the case numbers of the first months and the last months. 
       
### Timeline
###### On 29th of July 2020, the phrase "Case" changed to "Patients" on the graphs that the Ministry of Health announces
            Turkey started to announce only the symptomatic cases.
            Secondary repositories kept recording these numbers as cases.
            
###### On 25th of November 2020 the Ministry started to announce the cases once again
            There were not any adjustments for the previous cases.
            
###### On 10th of December 2020 the Ministry revealed missing previous cases cumulatively
            Secondary repositories kept this number as if the cases were discovered that day.
            
### Methodology

  Linear correlation, p-value, cross-validation and comparing with the cumulative cases for the gap are used to measure the accuracy of the model.

  Daily tests and recovered cases are used as features in the model.
  
  The most related feature was increase in deaths from 15 days later. This feature is created to acquire a stronger relation. It takes approximately 15 days to die from Covid-19   (Linton et al., 2020). Inspirations of this feature were mentioned in the acknowledgements section.
  
### The Most Important Variables in the Notebook

  "df" represents a dataframe object which contains data from the secondary source.
      Columns of this dataframe are Date, Confirmed(cumulative cases), Deaths(cumulative deaths), Death Rate(%), Increase(increase in the cases). 
      
  "turkey" represents a dataframe object which contains data from the Ministry.
      Columns of this dataframe are Date, Inc_Test, Inc_Case, Inc_Patient, Inc_Deaths, Inc_Recovered, Total_Tests, Total_Patient, Total_Deaths, Total_Recovered, Heavily_Ill,	         Pneumonia_Ratio where columns that start with Inc_ holds daily increases and the ones that start with Total_ shows total numbers at the date.
      
### Problems with the Datasets

Case numbers of Turkey were being recorded in the patients column until 29th of July. The dataframe from the ministry does not have records in this column until 27th of March 2020. These were filled with the secondary source.

The daily case numbers between 29th of July 2020 and 25th of November 2020 are unknown. These days are being mentioned as "the gap" 

"Inc_Patient" column starts recording symptomatic cases on 29th of July 2020. On the same day "Inc_Case" column starts recording the cases. Any sudden leaps or falls can not be observed for the "Inc_Patient" on that day. Meaning that the distinction between the cases and the symptomatic cases was not precise at the beginning.

Two columns are desired as independent variables: "Inc_Patient" and "Inc_Deaths"(or "IncreaseDeath").

Values will be taken starting from 25th of November 2020 since they were cases before that. 
The gap will be excluded.

Corresponding deaths for the day will be taken from the date which is 15 days later since covid-19 causes death approximately 15 days after the illness starts. 
