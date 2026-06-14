# US-Airline-Performance-Delay-Analysis-2015

## Project Objective

Every year, U.S. airlines operate millions of domestic flights â€” and a meaningful share of them run late or get cancelled, costing airlines money and frustrating travelers. This capstone project analyzes a full year (2015) of U.S. domestic flight data to uncover **why flights are delayed or cancelled**, **which airlines and airports perform best**, and **how time of day, day of week, and month affect delays**. The goal is to turn raw operational data into clear, data-backed recommendations for airlines and airport authorities.

## Tools Used

~ MySQL Workbench — data cleaning, transformation, and integration of raw CSV files
~ Power BI Desktop — data modeling, DAX-based KPI calculation, and dashboard design (dark theme)

## Dataset Used
Source: 2015 U.S. Department of Transportation flight performance data (~5.82 million domestic flight records), provided as part of this capstone project. The same dataset is publicly available as the 2015 Flight Delays and Cancellations dataset on Kaggle.
Three raw files:
`flights.csv` — individual flight records (departure/arrival times, delays, cancellations, diversions) — 5.8M+ rows
`airlines.csv` — airline codes mapped to airline names
`airports.csv` — airport codes mapped to airport details (city, state, latitude, longitude)
> ⚠️ **Note:** `flights.csv` is too large (~580MB) to host directly on GitHub (100MB limit). Please download it from the [Kaggle dataset link above](https://www.kaggle.com/datasets/usdot/flight-delays) to reproduce the full analysis.

## Questions (KPIs)
1. What is the overall on-time performance and cancellation rate for 2015?
2. What are the average arrival and departure delays across all flights?
3. Which factor contributes the most to delay-minutes — carrier, weather, late aircraft, NAS, or security?
4. Which airlines have the best and worst on-time performance?
5. Is there a relationship between flight volume and punctuality for an airline?
6. Which airports are the busiest, and how does that relate to their average delay?
6. What is the leading cause of flight cancellations?
7. How do delays vary by hour of day, day of week, and month of the year?
8. Which states/regions experience the highest average delays?

## Process
1. Data Cleaning (MySQL Workbench)
* Converted departure/arrival time fields from raw `HHMM` string format into usable hour/time values for temporal analysis.
Handled missing delay values carefully — nulls represent flights that were either on-time or cancelled, so they were not blindly filled with zero.
* Mapped cancellation reason codes (A, B, C, D) into readable labels: Carrier, Weather, National Air System, Security.
* Added a unified flight-date field to enable month/day-of-week level analysis.
* Joined the flights table with the airline and airport lookup tables to replace codes with actual airline names, airport names, cities,    and states.
2. Data Modeling & KPI Definition (Power BI)
* Built a relational data model linking flights, airlines, and airports.
* Created DAX measures for: Total Flights, On-Time Performance (arrivals within 15 minutes), Average Arrival/Departure Delay,               Cancellation Rate, and Delay-Minute share by cause.
3. Dashboard Design
* Designed a 5-page interactive Power BI dashboard with a modern dark theme, using slicers for dynamic filtering across airlines, airports, months, and dates.


## Dashboard
The dashboard consists of 5 pages:
1. Overview — headline KPIs (total flights, on-time %, cancellation rate), average delay cards, on-time gauge, delay-by-cause breakdown, and monthly trend.
2. Airline Performance — average arrival delay by airline, on-time leaderboard, flight volume by airline, and delay-cause mix per carrier.
3. Airport Network — cancellation reasons, busiest origin airports with their average delays, and a U.S. map shaded by regional delay severity.
4. Temporal Trends — average delay by hour of day, by day of week, monthly trend, and a flight-volume vs. delay scatter plot.
5. Insights & Actions — key findings and data-backed recommendations for stakeholders.


<img width="927" height="532" alt="U S_Airline_Dashboard_Page1" src="https://github.com/user-attachments/assets/69eb369e-99f3-4d82-a57e-cfbdf84c09c4" />

<img width="927" height="530" alt="U S_Airline_Dashboard_Page2" src="https://github.com/user-attachments/assets/f7c49514-bd1c-4364-b4fa-6d3de4869f84" />

<img width="925" height="532" alt="U S_Airline_Dashboard_Page3" src="https://github.com/user-attachments/assets/272096d3-34f4-4e03-a59c-9df817438493" />

<img width="926" height="532" alt="U S_Airline_Dashboard_Page4" src="https://github.com/user-attachments/assets/829d9c7b-db75-410b-ab2b-b64c42af9af8" />

<img width="925" height="530" alt="U S_Airline_Dashboard_Page5" src="https://github.com/user-attachments/assets/98ac0ec4-b2ca-47cd-b109-a3d28d73d13a" />

## Key Insights
- Out of 5.82 million flights analyzed, 82.1% landed on time and the cancellation rate was just 1.54% (~90,000 flights).
- Average arrival delay was 4.41 minutes, while average departure delay was 9.34 minutes.
- Late-arriving aircraft is the single largest contributor to delay-minutes (~39.84%), followed by carrier-related issues (~32.2%) — together accounting for nearly three-quarters of all delays. Weather, despite its reputation, accounts for only ~5% of delay-minutes.
- Hawaiian Airlines (89.5%) and Alaska Airlines (87.7%) had the best on-time performance, while Spirit and Frontier had the highest average arrival delays (14.5 and 12.5 minutes).
- High flight volume doesn't mean poor punctuality — Southwest and Delta, the two busiest airlines by flight count, were not among the worst delay performers.
- Hartsfield-Jackson Atlanta is the busiest airport (~347K flights) but maintains a low average delay (3.05 minutes), whereas Chicago O'Hare has high volume and the worst average delay (8.60 minutes) among major hubs.
- Of the cancelled flights, 54% were due to weather — the leading cancellation cause.
- Departure delays rise steadily through the day, peaking in the early evening (6–8 PM), indicating a cascading delay effect.
- Monday and Thursday are the most delay-prone days, while Saturday is the calmest.
- June is the worst month for delays (9.6 minutes average arrival delay), while September–October are the smoothest.

## Recommendations
1. Protect aircraft turnaround buffers at hub airports — Since late-arriving aircraft cause ~40% of all delay-minutes and concentrate at     busy hubs, adding 10–15 minutes of scheduled ground buffer time and prioritizing gate/crew readiness for first flights of the day         could break the delay cascade early. (High impact, medium effort — Airlines)
2. Re-time flights away from the late-afternoon peak — Since delay accumulates into the evening, shifting flexible flights to the 6–10 AM    window and trimming peak-hour frequency on the worst weekdays could reduce knock-on delays. (Medium-high impact, low effort — Airlines    & Schedulers)
3. Build weather contingency into seasonal schedules — Since weather drives 54% of cancellations and June/February are the worst months,     pre-staging summer storm and winter de-icing plans along with padded schedules and crew reserves would soften the seasonal impact.        (High impact, higher effort — Airlines & Airport Authorities)

## Final Conclusion
The 2015 data shows that U.S. air travel was largely on time, but the delays that did occur were concentrated, predictable, and addressable. The biggest single lever for improvement is the aircraft turnaround process — preventing aircraft from falling behind early in the day prevents a large share of downstream delays. By combining operational changes (turnaround buffers, smarter scheduling) with seasonal weather preparedness, airlines and airport authorities can meaningfully improve on-time performance and reduce cancellations in future years.

---
Project by: Alveena Fatima
Tools: MySQL Workbench, Power BI Desktop


   
