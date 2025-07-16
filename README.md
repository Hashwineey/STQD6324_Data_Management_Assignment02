# STQD6324_Data_Management_Assignment02

## Introduction
Hi and Welcome back! 
This project explores flight performance in the US for the year 2004, focusing on flight delays and cancellations. Using Python, SQL (Hive), and Plotly for visualizations, the analysis identifies:
+ Airlines, airports, routes, and flights with the highest delays or cancellations
+ Patterns over time (month, time of day)
+ Insights into which factors correlate with poor performance

The goal is to help stakeholders in the airline industry make data-driven operational decisions to improve punctuality and reduce customer disruptions using analysis of past data.

## Tools and Technologies

- Python 3.9
- HiveQL
- Hadoop HDFS
- Jupyter Notebook
- Plotly Express
- Docker Sandbox for Hive setup

## Overview of Project Flow
![Project_Flow](https://github.com/user-attachments/assets/ff09ccd9-e97d-47ed-aca8-ddfc4d339fa3)

## Data Collection
The dataset was obtained from [Kaggle](https://www.kaggle.com/datasets/wenxingdi/data-expo-2009-airline-on-time-data/data?select=2004.csv). As mentioned earlier, the 2004 dataset was used for this project.
[US DOT Bureau of Transportation Statistics (BTS)](https://www.transtats.bts.gov/Fields.asp?P74_e19=-LM&P74_P1y=&n22yB_4n6r=&5146_p1y7z0=&frn4pu_Y11x72=&sv0q=&5146_14qr4=) was also referred to get the meaning of the abbrevations in the dataset.

## Data Preparation
Since the data from Kaggle is too large to be uploaded to Hive, the dataset was split into two distinct datasets: df_delay_2004.csv and df_cancelled_2004.csv. 
df_delay_2004.csv contains all the data of delayed flights in 2004 and df_cancelled_200.csv contains all the data of cancelled flights in 2004.
You may refer to the "Data Cleaning.ipynb" file for the data preparation steps.

## Upload Data to Hive
Now that we have two cleaned datasets, it is time to upload them to Hive in order for us to analyse the datasets.

For that, first, the CSV files were copied from the local drive to the hdp-sandbox.
![Local_to_Sandbox](https://github.com/user-attachments/assets/7f4a8a1b-b9ac-47b2-b1fd-f192354707e2)

Then, the files were uploaded to HDFS
![HDFS Upload](https://github.com/user-attachments/assets/967ac06a-67bd-48e9-ab18-20417edf65f0)

Lastly, the datasets were mapped to Hive tables that were created for these datasets. You may find the codes to create table in Hive in "Create_Hive_Table.txt" file. 
![Hive_Table](https://github.com/user-attachments/assets/f0167863-2dc8-4dcc-92cf-6c58f6fe6837)

## Data Analysis and Data Visualization
Once the datasets are uploaded to Hive, Jupyter Notebook was then connected to Hive to make Data Analysis and Data Visualization easier.
The analysis for this dataset includes:
+ Identifying delay patterns
+ Determining factors contributing to delayed flights
+ Identifying reasons behind flight cancellation and how it correlates to specific airlines, airports and time of the day.
+ Identifying problematic routes, carriers or flights and analysing them.

### Delay Patterns

#### 1. Average Delays by Time of Day
![Delay_by_Time](https://github.com/user-attachments/assets/6c08dddb-3840-4c91-a45f-17a1cc610cc9)

***Morning flights tend to delay the least on average compared to Afternoon or Evening flights***

According to [Frommer's.com](https://www.frommers.com/tips/airfare/5-reasons-early-morning-flights-are-less-likely-to-be-delayed/), flights are less likely to be delayed in the morning because:
1. there is no need to wait for plane arrival from another destination
2. air traffic is lighter in the morning
3. there are lesser thunderstorms in the morning compared to in the afternoon or evening.
4. airlines prioritize early flights to stay on schedule because delays in early flights would mess up their whole day.

#### 2. Days of the Week Show Better On-Time Performance
![Days_Performance](https://github.com/user-attachments/assets/75f27677-1a70-4a8d-be8f-9c6b72b627cc)

Above is a bar chart that shows the average flight delays for each day of the week. From the plot, we can see that Saturdays usually has the lowest average delay of approximately 2.65 minutes, while Mondays, Thursdays and Fridays show the highest averages near 8 minutes. This suggests that flights on Saturdays generally experience fewer delays, likely due to reduced air traffic compared to other days of the week, when business travel and holiday travel peaks. Overall, Saturdays show better on-time performance compared to other days of the week.

#### 3. On-Time Performance by Months/Seasons
![Months_Performance](https://github.com/user-attachments/assets/d8637ba9-be52-48e9-9116-692343955c4f)

The analysis shows how average flight delays vary by month. 

+ Overall, September stands out as the month with the least average delays, recording just about 1 minute on average — likely due to fewer travelers and stable weather conditions. April and March also show relatively low average delays, under 4 minutes, making early spring an ideal time to fly with minimal disruptions.
+ In contrast, June and December have the highest average delays at around 11 and 10.9 minutes, respectively. This is expected as June marks the start of the summer travel peak, often accompanied by thunderstorms, while December brings heavy holiday travel and possible winter weather challenges.
+ The pattern suggests that peak vacation and holiday months (June–August and December) tend to have higher delays due to increased passenger volume and seasonal weather impacts. Meanwhile, off-peak months like September, and parts of spring, generally offer better on-time performance.

### Delay Factors

#### Top 5 Factors That Contribute to Flight Delays and their Impact
![Factor_Proportion](https://github.com/user-attachments/assets/e34271eb-61ab-466e-bb2d-e3ed3ff9bd2c)

From the above donut pie chart, we can say that:

In 2004, Late Aircraft Delays and National Aviation System, NAS Delays were the dominant factors driving flight delays, together accounting for over two-thirds of all delay time. Besides that, Carrier Delays accounted for roughly 26%, while Weather and Security delays were much smaller contributors. Even though this data is historical, analysing it in 2025 helps show where airlines and airports may have focused operational improvements over the past two decades. Understanding these patterns provides a valuable benchmark for measuring how much these categories have improved or changed in today’s aviation operations.

![Delay_Minutes_by_Factor](https://github.com/user-attachments/assets/e9fb94b3-7e16-4c10-9e4e-d431907bf42f)

This bar chart ranks the main factors that contributed to flight delays in 2004, based on total delay minutes and their percentage share.

In the 2004 dataset, operational issues such as late aircraft connections and NAS-related delays were the biggest drivers of total flight delay minutes. This pattern highlights where major efficiency gains and investments in air traffic management could have the biggest long-term impact, which can be a lesson that can be applied when comparing historical trends with improvements by 2025.

### Primary Reasons for Flight Cancellations
![Cancel_Reasons](https://github.com/user-attachments/assets/27b599db-f288-4d1b-b39e-1aeedaa556c1)

This pie chart illustrates the proportion of flight cancellations in 2004 categorized by the U.S. Department of Transportation’s (DOT) standard cancellation codes:

+ A – Carrier: Cancellations due to airline-related problems such as mechanical issues, crew unavailability, or operational decisions.
+ B – Weather: Cancellations primarily driven by adverse weather conditions (e.g., storms, fog, or snow).
+ C – NAS (National Airspace System): Cancellations caused by air traffic control delays, heavy traffic volume, or system capacity constraints.
+ D – Security: Cancellations due to security concerns such as threats, lockdowns, or other security-related disruptions.

And from the pie chart, we can see that:
1. Carrier-related issues (Code A) were the largest contributor, making up ~46% of all cancellations in 2004. This suggests that airline operations and logistics were a significant driver of flight disruptions that year.
2. Weather-related cancellations (Code B) accounted for about 35%, highlighting how unpredictable weather conditions still heavily impacted flight reliability — a pattern that remains relevant today.
3. NAS delays (Code C) made up around 19%, reflecting the challenges within the national airspace system such as air traffic congestion or limited airport capacity.
4. Security-related cancellations (Code D) were negligible (<1%), indicating that in 2004, security issues were not a major factor in overall flight cancellations.

The analysis shows that while uncontrollable weather events still play an important role, operational efficiency within airlines (Carrier) was the top reason flights were cancelled in 2004. This insight can help modern airlines and airports prioritize resource planning, maintenance, and contingency strategies to reduce cancellations due to controllable factors.

### Flight Cancellation Correlation

#### 1. Cancellations by Airline
![Cancel_Airline](https://github.com/user-attachments/assets/6a544059-debc-4732-b69d-ee9e0e2224c7)

From the above graph, we can see that, in 2004, MQ Airline had the most cancelled flights. Referring to [U.S./BTS](https://www.transtats.bts.gov/FieldInfo.asp?Svryq_Qr5p=h0v37r%FDPn44vr4%FDP1qr.%FDjur0%FD6ur%FD5nzr%FDp1qr%FDun5%FDorr0%FD75rq%FDoB%FDz7y6v2yr%FDpn44vr45%FP%FDn%FD07zr4vp%FD57ssvA%FDv5%FD75rq%FDs14%FDrn4yvr4%FD75r45%FP%FDs14%FDrAnz2yr%FP%FDcN%FP%FDcN%FLE%FM%FP%FDcN%FLF%FM.%FDh5r%FD6uv5%FDsvryq%FDs14%FDn0nyB5v5%FDnp4155%FDn%FD4n0tr%FD1s%FDBrn45.&Svryq_gB2r=Pun4&Y11x72_gnoyr=Y_haVdhR_PNeeVRef&gnoyr_VQ=FGJ&flf_gnoyr_anzr=g_bagVZR_eRcbegVaT&fB5_Svryq_anzr=bc_haVdhR_PNeeVRe), MQ is Envoy Air. PSA Airlines Inc. (OH) and 	American Airlines Inc. (AA) are also among the airlines that had the most cancelled flights. These carriers might have operated high-volume regional routes prone to weather disruptions or operational constraints.

#### 2. Cancellations by Airport
![Cancel_Airport](https://github.com/user-attachments/assets/e8b2bcfe-c788-4b86-bd3a-0cf270013443)

Based on above analysis, ORD airport had the most cancelled flights. In contrast, the LAX airport had the least number of cancelled flights. Busy hubs like ORD (Chicago O’Hare) are more sensitive to ripple effects of weather, congestion, and connecting flights. This is deduced based on Chicago's inconsistent weather, as discussed in the [Climate of Chicago, Illinois: The What and Why of Every Season](https://theclare.com/blog/climate-chicago-illinois/#:~:text=The%20polar%20jet%20stream%E2%80%94a,temperatures%20in%20winter%20and%20summer.) article. 

#### 3. Cancellations by Month/Season
![Cancel_Month](https://github.com/user-attachments/assets/f4b4e85f-f018-45f0-a493-ab987fbc8713)

Above analysis shows clear seasonal patterns, where peaks occurred in January, September, and December, and the lowest in April. This could possibly due to winter storms in January and December, and potential operational adjustments in September, which may have contributed to spikes.

#### 4. Cancellations by Time of Day
![Cancel_Time](https://github.com/user-attachments/assets/3466e5a8-a00b-4b3c-9176-2f4b0ac7096c)

Our analysis above shows that flights scheduled in Afternoon and Morning are the ones that mostly got cancelled, in 2004. This could be related to the fact that afternoon flights and morning flights would be delayed the most. 

#### Overall Summary on Correlation of Flight Cancellations
Based on the 2004 dataset, flight cancellations clearly correlate with certain airlines, origin airports, and time patterns. The visualizations indicate that specific carriers and airports contributed significantly to the total cancellations. Seasonal trends and times of day further show when cancellations were most likely to occur, providing actionable insights for future operational improvements. Identifying these patterns helps airlines and airports proactively manage resources, adjust schedules, and minimize passenger disruptions.

### Problematic Aspects (Routes, Carriers, Flights)

#### 1. Top 5 Most Problematic Routes (Delayed or Cancelled Flights)
![Problematic_Routes](https://github.com/user-attachments/assets/58e13cce-c0f6-421a-9cd5-a9669a292291)

The grouped bar chart shows the top 5 origin–destination routes with the highest total number of delays or cancellations. The group bar represents different events (delayed or cancelled) summed together for a full "problematic" picture. For easy comparison, the total delays and total cancellations are plotted side by side.

**Our analysis:**
- Routes like HOU–DAL and DAL–HOU have very high delay counts and non-trivial cancellations, making them the most problematic.
- Some routes, like ATL–LGA, have a high delay count but a relatively small cancellation count, showing that operational reliability is more about managing delays than preventing cancellations there.
- Combining both factors of delayed flights and cancelled flights provides us a comprehensive view of route reliability issues.
- Routes with high counts for both delays and cancellations are likely suffering from multiple operational challenges — weather, congestion, or carrier factors — and could be priorities for improvement.

#### 2. Top 5 Most Problematic Carriers (Delayed or Cancelled Flights)
![Problematic_Carriers](https://github.com/user-attachments/assets/c749f7c2-7978-468a-a966-6cb78524243e)

The grouped bar chart shows the top 5 airlines with the highest number of flights that were delayed or cancelled. The same concept from previous analysis is applied here.

**Our analysis:**
- **WN (Southwest Airlines)** has the largest number of delays, indicating widespread late departures or arrivals but relatively fewer cancellations.
- **DL (Delta)** and **AA (American Airlines)** follow a similar pattern.
- **MQ (Envoy Air)** stands out for having the highest cancellation count among these top carriers, suggesting different operational challenges compared to the majors, like weather, regional connection challenges, or scheduling issues.
- Overall:
  - delays are a far more frequent issue than cancellations across major US carriers, reflecting how airlines prefer to delay rather than cancel flights when disruptions occur.
  - We can also see that airlines with very high delays but low cancellations may have capacity or scheduling inefficiencies but manage to operate flights instead of cancelling outright.
  - An airline with both high delays and higher cancellations (like MQ) might have struggled with more disruptive issues like resource limitations or reliance on smaller regional airports.

  #### 3. Top 5 Most Problematic Flights (Delayed or Cancelled Flights)
  ![Problematic_Flights](https://github.com/user-attachments/assets/ba6c1031-738e-42de-9025-cab3a7e48960)

  The grouped bar chart shows the top 5 individual flight numbers with the highest number of delays or cancellations combined.

**Our analysis:**
- **WN Flight 1406** was the most problematic, with 899 delays and 2 cancellations.
- Other Southwest Airlines flights (WN 2020, WN 574, WN 2546) all experienced 800+ delays, highlighting recurring on-time performance issues.
- **HP Flight 530** had 800 delays and also higher 17 cancellations, suggesting possible operational or route-specific challenges.
- Overall:
  - Delays are the dominant factor for problematic flights, while cancellations are rare for these specific flight numbers. This suggests these flights regularly operate but struggle to stay on schedule, pointing to potential issues like high route demand, tight scheduling, or frequent ground delays.

## Conclusion
This analysis explored US domestic flight performance for the year 2004, focusing on the root causes and patterns behind delays and cancellations. By combining both Hive and Python tools, we were able to break down massive raw flight data into actionable insights that airlines and airport stakeholders can still find relevant today.

### What can we takeaway from all of this?

- **Delays remain the dominant issue:**  
  The majority of “problematic” flights, routes, and carriers showed far higher delays than cancellations. Airlines often choose to delay rather than cancel outright to avoid lost revenue and stranded passengers.

- **Morning flights are your best bet:**  
  Flights scheduled in the morning consistently experienced fewer delays than afternoon or evening flights, aligning with known industry trends related to lighter air traffic and weather conditions.

- **Seasonality and weekly trends matter:**  
  Months like June and December had the worst average delays, which lines up with peak summer travel, winter weather, and holiday surges. Meanwhile, Saturdays and September showed better on-time performance, offering opportunities for airlines to adjust capacity planning.

- **Late Aircraft and NAS issues drive delays:**  
  Operational factors like late-arriving aircraft connections and National Aviation System (NAS) delays were the biggest contributors to total delay minutes. This shows that improving scheduling buffers and air traffic management efficiency could yield the largest impact.

- **Carrier-related issues top cancellation reasons:**  
  Almost half of all cancellations were caused by airline operational issues. This highlights the need for robust maintenance scheduling, crew management, and better contingency planning to reduce cancellations.

- **Specific airlines, routes, and flights are repeat offenders:**  
  Visualizing delays and cancellations side by side revealed that certain airlines (e.g., WN for delays, MQ for cancellations) and busy hub airports like ORD were especially prone to disruptions. Likewise, specific high-frequency short-haul routes (like HOU–DAL) surfaced repeatedly as problem areas.

### Why this matters?

By analysing these historical patterns, the aviation industry can benchmark how far operational performance has improved since 2004. Stakeholders today can apply these insights to:
- Revisit buffer times for aircraft turnaround and connections
- Optimise flight schedules around known seasonal and time-of-day patterns
- Strategically allocate resources at high-risk airports and on high-volume routes
- Design contingency plans that target controllable cancellation factors

### How it will impact the future?

This project demonstrates the value of turning raw flight logs into clear, data-driven stories. In an industry where every minute counts, even small improvements in understanding patterns and root causes can help airlines boost reliability, cut costs, and improve passenger trust.

## References
- [US DOT Bureau of Transportation Statistics](https://www.transtats.bts.gov/)
- [Kaggle: US Flight Delays Dataset](https://www.kaggle.com/)

**Thank you for your attention! Hope this analysis would be helpful!**


  





























