## Anti-Wage Theft Data Project

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/cover.jpg />
  
#### Team members and assigned tasks:
- :pushpin:Lyn Ngoc: data analysis, compiling report
- :pushpin:Aichu Tan: data cleaning and data analysis
- :pushpin:Pilar de Haro: data cleaning, data analysis, literature reviews and compiling report
- :pushpin:Eddie Rosas: Website and Video

**Report link :** :point_right:[here](https://sites.google.com/sdsu.edu/wagetheft/home?authuser=1)

**Video link :** :point_right:[here](https://www.youtube.com/watch?v=JLkuwMMDtyE)


#### 1. Problem Statement :bookmark_tabs:

Wage theft is a pervasive and troubling issue in the U.S., affecting millions of workers and costing billions in unpaid wages each year. The [Economic Policy Institute](https://www.epi.org/publication/wage-theft-2021/) reports that from 2017 to 2020, over $3 billion was recovered through various channels, yet this represents only a fraction of the total wage theft that occurs, as many cases go unreported or unresolved. In Los Angeles alone, wage theft is estimated at $1.4 billion annually, with only 17% of workers who win cases actually receiving the wages owed to them. Industries like construction, food service, and retail are especially affected, with low-wage and immigrant workers being the most vulnerable (Mangundayao et al.).

Understanding the wage theft claims process is essential to advocating for workers' rights and helping individuals recover lost earnings. This project aims to reveal the issues within the wage claims recovery process by pointing out the patterns and trends in wage claim cases across
various industries, and predicting the duration of the wage claim process. Using time-series modeling and exploratory data analysis, the research will address critical questions, including the average time it took from filing a claim to a hearing and closing a claim, the rate of retrieving stolen wages, and trends by industries.

#### 2. Literature Review :open_book:
##### 2.1 Confronting Wage Theft: Barriers to Claiming Unpaid Wages in San Diego

This 2017 study by the San Diego State University Department of Sociology, the Center on Policy Initiative, and the Employee Rights Center of San Diego examines the challenges San Diego workers face when trying to recover their stolen wages through the wage claim process with the Labor commissioner’s office in San Diego. The study surveyed 305 workers who were in the process of filing or had filed a claim of wage theft, conducted 30 additional in-depth interviews with workers and analyzed data obtained from the labor commissioner's office. Because we are using the same data source, it was important for us to compare our findings with these trends and understand the context found in this study.

The study’s findings related to our data analysis tied to identifying the industry with the highest counts of wage claims reported, the highest type of violation type and how long the process took to receive a hearing and collect their stolen wages. This study found that the restaurant and construction industries had the most complaints filed. And, that 71% of reported claims were from violations of regular wages and 25% reported overtime violations. The study also highlighted the long wait times that surpass the legally required timeline. 59% of workers they surveyed reported waiting for a conference double the 30-day wait limit. Lastly, most workers don’t recover what they believe they are owed. Their analysis from the Labor Commissioner data from 2010- 2016 shows that workers, “...collect, on average, only 15% of the amounts awarded at hearings.”

This study pointed out the lack of staffing and capacity of The Labor Commissioner office limited them to investigate fewer than half the 2,852 wage claims that were reported in 2016. The study’s recommendations to protect workers and better enforcement are to actively enforce sick days and minimum wage law, increase funding for proactive investigation at worksites, better protection against workplace retaliation, effective workers rights outreach to explain the process in different languages, and create an online complaints form. At the time of this study, workers were required to complete a form and either mail it to the labor commissioner's office or submit it in person.

##### 2.2 Regulating Wage Theft

This comprehensive analysis of 141 state and local anti-wage theft laws, spanning twenty-four states and fifty-seven localities between 2005 and 2018, highlights that while traditional anti-wage theft laws are unlikely to significantly reduce wage theft, it identifies new "collaborative approaches" that could strengthen agency enforcement and incorporate nongovernmental strategies beyond regulation.
Some of the traditional approaches found in “authorizing worker complaints” brought up in this report include the systematic barriers for low-income workers to file and retrieve their stolen wages and the lack of agency resources for better enforcement of wage and hour laws. Out of the 141 laws surveyed, 40% of the laws provide workers with a path to report wage theft or extend the time available to them for doing so.

This analysis makes the point that we must look beyond government regulation through collaboration with workers, and community groups to improve the wage claim process and reduce wage theft. These solutions also extend to allowing workers to make anonymous complaints, making it less risky for the worker who may be threatened by retaliation, and other forms of labor abuse. Also, placing more regulation on high-risk employers by requiring them to provide a wage bond in order to operate their business, and submit a wage report to the agency. Both of these employer regulations could help the investigation and recoup workers owed wages.

##### 2.3 Unpaid & Unaware :moneybag:

The San Diego State University Center for Community Research and Engagement and the Center on Policy Initiatives presented a 2024 report on wage theft in San Diego County, California, based on a survey of over 900 workers, primarily students. The report sheds light on the ongoing problem of wage theft, particularly in the food and drink/hospitality, construction, and healthcare industries. It indicates that employers in San Diego conform to broader patterns of labor law violations observed elsewhere.
Some of the key findings in the report indicate that workers often need to be made aware of their rights and the resources available to them, such as the complaint process. The report recommends that local governments improve enforcement, disincentivize wage theft, and empower workers through education and co-enforcement initiatives.

#### 3. Database management and Data Process procedure

We used two datasets obtained from the San Diego Labor Commissioner’s Office, from January 2011 to June 2016 that include fields like date_filed, date_closed, verified_amount_due, wages_collected, judgment_day and others that were used for this analysis.

We obtained the records through a public request act, so we found that the datasets needed to be reformatted, cleaned and merged. We removed extra spacing, duplicates and reassigned data types in R. In cases where there were slight variations between records, such as one differing field, they were considered duplicates. This is because there were duplicate case numbers with identical information across records, except for differences in the defendant field. This indicated that the same individual opened two claims on the same day for the same amount against the business entity (where they worked at the time the wage theft occurred) and individual (the owner, or supervisor of the establishment where the wage theft occurred). We removed the duplicates since individuals are only paid out the owed amount once and for the purposes of this analysis it shouldn’t be counted twice.

Before proceeding with the analysis, we correctly reassigned data types in R, ensuring that numeric values, dates, and character fields were properly formatted. We were able to join the two datasets with the related “CASE” field, to provide a fuller picture of all the fields pertaining to the individual wage theft complaint. We observed discrepancies between the fields 'date_filed', 'closing_date', and 'judgment_date'. The 'date_filed' should represent the earliest date, but we found numerous records where the 'closing_date' and 'judgment_date' were earlier than the 'date_filed' of the complaint.

Part of the pre-processing included finding the mean and standard deviation of the amount of the “verified wages found due”, and creating a histogram to confirm if the verified wages found are a normal distribution. We noticed that the histogram and Q plot we created was a bit skewed, so we reviewed the highest and lowest amounts of wages. We found that there were a high number of outliers, some which we identified as errors. We were able to resolve some of these errors by removing records with “0” in the “verified wages found due” column. After cleaning we were left with 6,551 records that were verified by the state.
This was stored and maintained in a relational database to support the relational component of our datasets and standardized fields.

#### 4. Data Analysis and Visualization

We conducted the majority of our data analysis in R to summarize some of the statistics and used time series modeling to predict the wage claim durations over time. And, we also use Tableau to display our findings.

##### 4.1 The duration of the wage claims process

On average, we found that it took 230 days from the filing of a claim to the hearing, with a median duration of 215 days. And, the longest case to receive a hearing took 991 days while the shortest was 78 days. Under California labor law, the Labor Commissioner is required to notify the worker of a hearing date within 30 days of the claim being filed. But, our results indicate that the process is taking more than double the expected time outlined by the law. We found that 72% of verified cases had not received a hearing date after 30 days of filing.

We also discovered that out of the 6,551 verified cases where the labor commissioner ruled in favor of the worker, only 734 cases were closed. Furthermore, when comparing the total duration from the date a worker files a complaint to the date their case is closed, we found an average of 160 days.

In R, we leveraged the dplyr library to use the filter function to filter by verified claims and other fields, the difftime function to calculate the differences between the two dates, judgment date and file date, in days. Then used the mean, median, max, min functions to find the results.

##### 4.2 Forecasting the time it will take to close a wage claim file in 3 years

We used the forecast package and the ARIMA model in R to predict the number of days it will take for a wage claim to close in the years following 2015. The predictions are based on the duration between the filing and closing dates of a wage claim. Using data from 2011-2015 (excluding 2016 due to incomplete data), our model projected that, for the period between 2016 and 2018, the average time to close a claim would be 264 days, with a predicted range from a minimum of 62 days to a maximum of 467 days.

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig1.jpg />

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig2.jpg />

 To develop this forecast model, we first filtered the data by filing date to calculate the number of days it took for each case to close. Then, we used the ts() function to create a time series object and fitted the ARIMA model to it. We determined that ARIMA(0,0,0) with a non-zero mean was the best model due to the stationarity of our data, indicating fewer detectable trends. We followed a tutorial by [Simple SPSS](https://www.youtube.com/watch?v=VPhyVSJMbpA) to help us identify the appropriate ARIMA model, interpret the plots, and validate our results.

 <img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig3.jpg />

 ##### 4.3 The rate of workers recovering their stolen wages
Our findings show only 35% of the total wages verified by the state have actually been paid out, indicating that workers received only a portion of what they were owed. The 2017 "Confronting Wage Theft" report highlights that it's common for workers not to recover the full amount of their wages. One contributing factor is that many workers settle for less than their full claims due to the need for immediate funds to cover living expenses or the inability to take time off from a new job to continue the claims process.

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig4.jpg />

We calculated this figure by summing the "amounts found due" field, then dividing it by the total “verified wages due”, and multiplying by 100 to determine the percentage of total wages that have been paid.The average amount of verified wages owed was $5,379. The largest verified amount owed was $357,198, while the smallest was $1.32.

##### 4.4 Trends by Industry
Our analysis showed that wage claims were highly concentrated in certain industries, particularly those employing low-wage and temporary workers. However, one industry code in our dataset encompassed a variety of sectors, complicating efforts to identify the industry with the highest number of claims. This category (439: Other - chainsaw & lawn mower repair, home health care, employment agencies, non-boarding schools, cable TV) was grouped under the label "Service Industry, Education, and Media" for clearer presentation in our results. However, the second and third most affected industries were the food service sector and construction. This aligns with findings from the report Confronting Wage Theft, which also uses data from the Labor Commissioner’s office in San Diego.

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig5.jpg />

These two industries also reported the highest amounts of minimum wage violations, with the construction industry accounting for $25,527 and the food industry for $25,003.

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig6.jpg />

##### 4.5 Wage Theft Cases by Employer Locations :round_pushpin:
This map shows the distribution of Wage Theft Cases by Employer Locations from 2011 to 2016. We used the information in the 'defendant_address' field, which contains Zipcode data. By extracting the Zipcode using the RIGHT() function in Tableau, we created a new field called 'defendant_zipcode.' After removing an uncategorized location that could not be mapped in Tableau, we produced [an interactive visualization map](https://public.tableau.com/views/WageTheftCasesbyEmployerLocations/Dashboard2?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) that allows filtering wage theft cases by year, industry category, employer name, and the verified wage amount collected.
From the visualization map, we observed that employers involved in wage theft cases in San Diego were spread throughout the United States, not limited to the San Diego area. This finding emphasizes that wage theft occurred across various sectors nationwide.

<img src = https://github.com/AichuTan/BDA-594-Final-Project/blob/main/Fig7.jpg />

##### Discussion for the limitations and challenges in our projects:

Cleaning the datasets was a long process, because we kept finding errors and discrepancies. We believe this was due to how the data was transferred from a physical intake form to a database system. We also needed context to understand how to clean these records of information, which did take some time to research the process and regulations of filing a wage claim before diving into the analysis. When we started to prepare our data for the forecasting process, we realized that we needed to omit the year 2016 since there was only data representing half of the year, and that was initially skewing the forecasting. So, the challenges were trial and error as we were learning how to apply forecasting and making sure the data was as accurate as possible. 

##### Conclusion (Future Development Plan and References)

In conclusion, our analysis highlights the need for a restructuring or reform of the wage claim intake and processing system. This points to broader issues such as inadequate enforcement, lack of labor rights education for workers, and insufficient resources at the San Diego labor commissioner’s office. The numerous inaccuracies we encountered made it challenging to conduct a thorough analysis, which also delays reporting for policy and advocacy groups.

Looking ahead, we believe that progress can be achieved through nontraditional strategies, as highlighted in the Regulating Wage Theft report. This includes collaborating with workers and community groups to address the flaws in the current system. Additionally, there is a clear need to create protections for workers who are more vulnerable to labor exploitation by implementing stronger employer regulations.


**Bibliography** :books:

Lee, Jennifer J., and Annie Smith. “Regulating Wage Theft.” *Washington Law Review*, vol. 94, no. 2, June 2019, pp. 759–822.
[](https://scholarshare.temple.edu/bitstream/handle/20.500.12613/6755/Lee-JournalArticle-2019-.pdf?sequence=1)

Mangundayao, Ihna, et al. “More than $3 Billion in Stolen Wages Recovered for Workers Between 2017 and 2020”. *Economic Policy Institute*, 22 Dec. 2021.[](https://www.epi.org/publication/wage-theft-2021/)

Galvin, D. J. (2016). “Deterring wage theft: Alt-labor, state politics, and the policy determinants of minimum wage compliance”. *Perspectives on Politics*, 14(2), 324-350. [](https://doi.org/10.1017/S1537592716000050)

Green, Llezlie L. "Wage Theft in Lawless Courts." California Law Review, vol. 107, no. 4, Aug. 2019, pp. 1303. [](https://doi.org/10.15779/Z38FF3M08W.)

San Diego State University Department of Sociology, Center on Policy Initiative, and Employee Rights Center. "Confronting Wage Theft: Barriers to Claiming Unpaid Wages in San Diego." 2017.[](https://ccre.sdsu.edu/_resources/docs/reports/labor/Confronting-Wage-Theft.pdf)

"Time Series Analysis-ARIMA Model using R software: A step by step approach." *YouTube*, uploaded by Simple SPSS, 30 Mar. 2020, [](www.youtube.com/watch?v=VPhyVSJMbpA)
