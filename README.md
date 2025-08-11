# Credit Card Company Financial Dashboard

## Objective
Build an interactive financial dashboard for a credit card company using SQL and Power BI to track:
Customer demographics
Transaction patterns
Revenue performance

## Workflow: CSV → SQL → Power BI → Weekly Data Refresh → Business Insights

### Tech Stack
SQL (MySQL / PostgreSQL) → Data storage & querying
Power BI → Dashboard creation & KPI visualization
CSV → Data source
DAX → Calculated fields

## DAX Queries used :
 AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
 )
 IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)

 week_num2 = WEEKNUM('public cc_detail'[week_start_date])
 Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
 Current_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]))) 
Previous_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1)


### Process Overview
<img width="1536" height="1024" alt="f4250d23-eec9-4741-b71d-b246f5f0cdb9" src="https://github.com/user-attachments/assets/7f0fe359-2512-400b-8450-a34dce417ddd" />

Import CSV data (Customer & Transaction) into SQL database.
Connect SQL to Power BI using Direct Query/Import.
Create 2 Dashboards:
Customer Report → Demographics, card types, activation/delinquency rates.
Transaction Report → Revenue, interest, category spending, trends.
Weekly Refresh:
Added Week 53 (31st Dec) CSV data to SQL.
Refreshed dashboards for updated KPIs.

### Week 53 Insights (31st Dec)
Week-over-Week Change:

Revenue ↑ 28.8%

Year to date Overview:

Revenue: 57 M

Interest Earned: 8 M

Transaction Amount: 46 M

Male Revenue: 31 M | Female Revenue: 26 M

Card Type Share: Blue & Silver → 93% of transactions

Top Regions: TX, NY, CA → 68% of transactions

Activation Rate: 57.5%

Delinquency Rate: 6.06%

### Key Recommendations
Leverage Blue & Silver card dominance with targeted promotions.
Expand regional offers in TX, NY, CA to maximize transaction volume.
Increase customer activation rate via onboarding incentives.
Closely monitor delinquency trends to reduce financial risk.

### final dashboards :
![cc_page-0001](https://github.com/user-attachments/assets/d708af44-09b0-4d31-a436-ef06c3140226)
![cc_page-0002](https://github.com/user-attachments/assets/d815659b-c90d-4d6f-9381-bf6424714b7b)




