Author: Syeda Zehra Ali (MPP’ 2017 Candidate, Goldman School of Public Policy)

Course: PS239T 

Topic: Higher Education Enrolment Landscape in India (2015) 

Data Source: Ministry of Human Resource Development India, Population Census 



Data Description
==========================================================

The data being analized here has been published by Ministry of Human Resource Development, Government of India. It is a product of annual All India Survey on Higher Education. This survey covers entire higher education institutions in India, with responses from 716 universities, 29506 colleges, and 6837 stand-alone institutions. The data covers various aspects of higher education in India, like student enrollment (by state, social background, gender, level of study, etc.), teachers (by state, post, social background, gender, etc.), and pupil teacher ratio, etc. The data is a very useful to make informed policy decisions and research for development of education sector.

The other two data sets are population census datasets having total figures for muslim population (separated by male and female) and for other minority groups in India.




Methodology
==========================================================

The packages used for this analysis include dplyr, readr, ggplot2, tidyr and ggthemes

A. Comparing State Averages
—————————————————————————————————————

This plot has been created by using ggplot and plotting states on the x- axis and the enrol_percent_total on the y- axis. The enrol
_percent_total has been created by using the percentage calculation formula as follows:

IndiaEducation2015$Enroll_Percent_Total<- (IndiaEducation2015$ac_total/IndiaEducation2015$population_total)*100,

where ac_total is the total number of enrolled students in the state, and population total is the total population of the state that is between 18 to 23 years of age.


B. Comparing Male vs. Female Enrollment 
—————————————————————————————————————

For this analysis, two new columns have been added to the data set i.e percent_male and percent_female, whereby the respective representation in enrolment is calculated for the two groups based on their population using formulas:

IndiaEducation2015$Percent_Male<- (IndiaEducation2015$ac_m/IndiaEducation2015$ac_total)*100

IndiaEducation2015$Percent_Female<- (IndiaEducation2015$ac_f/IndiaEducation2015$ac_total)*100

The two newly created columns have been renamed as simply ‘Male’ and ‘Female’

Next, they have been gathered together in a long data format using the gather command with key being ‘gender’

Using this long data set, The Gender Based Relative Enrolment graph has been plotted with state on the x-axis and enroll_percent on the y, and this has been grouped by gender using fill= gender.


C. Gender Analysis: For religious minorities
——————————————————————————————————————

1. The education data has been merged with the population data on muslims for the purpose of this analysis

2. Two states that were not in population census 2011 have been dropped from the education data due to unavailability of data in census file.

3. The two datasets have been merged using the left_join command

4. Two new columns have been added to the merged dataset to show relative percentage of males and females, the base now being muslim population. 

Muslim_Education2011Pop$Percent_Male_Muslim <- (Muslim_Education2011Pop$muslim_m/ Muslim_Education2011Pop$muslim_pop_m)* 100

Muslim_Education2011Pop$Percent_Female_Muslim<- (Muslim_Education2011Pop$muslim_f/ Muslim_Education2011Pop$muslim_pop_f) *100

5. The data has again been converted to long format with the key= gender

6. The long data is now used to plot “Higher Education Proportion of Enrollment by Gender for Muslims” using ggplot and having state on the x-axis and enrol_percent on the y-axis, and the fill= gender. 



D. Comparing Overall Muslim Enrollment to State Averages
—————————————————————————————————————————

For this analysis, a new column has been added to the merged data set that calculates the total percentage of muslim population that is enrolled in college. This data set has now been transformed into another long data set to gather ‘muslim’ and ’state average’, where both variables refer to the average enrolment rates. This has then been plotted using ggplot and having state on the x-axis and enrol_percent on the y-axis, and the fill= class (which is the key in gather command). 



E. Analysis for 5 largest Minority States: Muslims/ SC/ ST compared to State Average
—————————————————————————————————————————

1. For analysis on 5 largest minorities the already merged dataset has now been merged again, using the left_join command,  with ‘minority_population_data’, which adds population information for scheduled tribe and scheduled caste.


2. The new dataset is now called “EducationAndPopulation”. A sum_minorities column is now added which is the sum of populations for muslims, scheduled tribes, and scheduled caste. This column has the been used to slice the top 5 states and stored into a new dataset called “EducationAndPopulationTop5”.

3. For all minority groups, their percentage representation in enrolment is now calculated by adding new columns to the data

4. These new columns are then gathered in a new long dataset called “data_long_top5” and then used for plotting relative enrolments in comparison to state averages using the facet_grid option. 



F. An Overall Comparison- Looking at Resource Allocation
—————————————————————————————————————————

The final chart in this analysis uses geom_text to label all states on two axis, x= student teacher ratio, and y= enrolment percentage. This plot has been layered by adding colour to every state label on the basis of strength of minority population. 




