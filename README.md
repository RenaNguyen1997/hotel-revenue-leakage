# Hotel Cancellation Risk & Revenue Leakage Analysis

## Introduction 
This project analyses hotel booking cancellation patterns to identify high-risk revenue segments and simulate the impact of targeted cancellation policy adjustments.

Dataset includes:
- Booking details
- Customer type
- Distribution channel
- Region
- Length of stay
- Revenue and revenue lost

## Objective

The goal was to:
1. Identify segments contributing most to revenue leakage
2. Distinguish between high volume vs high structural risk
3. Build a Power BI dashboard for dynamic exploration
4. Implement a what-if simulation for leakage reduction

## Data processing 

This process was done by using Python, including following steps:
- Cleaned dataset: Missing data and Duplications, Format data types
- Created derived metrics:
  - realized_revenue
  - revenue_lost
  - cancellation_status
  - lead_time_buckets
  - total_nights_buckets
  - region
  - arrival details (Month, year, is weekend?)
- Generated segmentation-ready dataset
````
python hotel_demand_dataset.py
````
## Visualization 

PowerBI was the main visualization tool for this project. To be able to open the file, either PowerBI local app or PowerBI service must be created

Dashboard page:
- 1st page "Revenue stability overview":  Problem Validation, assist to answer the question "Does Cancellation Truly Drive Revenue Instability?"
- 2nd page " Policy recommendation": Strategic Risk & Exposure Analysis, applying a  two-layer analytical framework to guide decision-making

Key components:
- Dynamic segmentation slicer (Field Parameter)
- Scatter plot: Cancellation Rate vs Leakage Rate
- Mixed Chart: Total revenue lost and Total revenue by months across 3 years
- Bar chart: Leakage rate by months across 3 years
- Drill-down bar chart for segment combinations
- What-if parameter for cancellation reduction

Key Measures:

```` DAX
--Leakage rate metrics
Leakage rate = DIVIDE ([Total Revenue Lost], [Total Revenue],0)
Leakage rate (overall) = CALCULATE([revenue cancellation ratio], ALL(hotel_demand_dataset))
Adjusted Leakage Rate (by segments) = DIVIDE(SUM(hotel_demand_dataset[revenue_lost]), [Total revenue (overall)])
Cancellation Proportion = DIVIDE(
    CALCULATE(COUNT(hotel_demand_dataset[is_canceled]), hotel_demand_dataset[is_canceled] = 1),
    COUNTROWS(hotel_demand_dataset),
    0
)

--Revenue metrics
Revenue Lost (Overall) = CALCULATE(SUM(hotel_demand_dataset[revenue_lost]), ALL(hotel_demand_dataset))
Revenue (Overall) = CALCULATE(SUM(hotel_demand_dataset[revenue]), ALL(hotel_demand_dataset))
Simulated revenue lost = [Simulated leakage rate] * SUM(hotel_demand_dataset[revenue])
Projected revenue saved = SUM(hotel_demand_dataset[revenue_lost]) - [Simulated revenue lost]
Projected revenue saved (by segments) = SUM(hotel_demand_dataset[revenue_lost]) * 'Reduction%'[Reduction% Value]
````

Scenario Simulation: Users can:
- Select a risky segment
- Adjust reduction %
- View projected revenue saved
- Compare portfolio leakage before and after intervention

## Result
The dashboard enables:
- Identification of top leakage drivers
- Dynamic drill-down analysis
- Quantification of revenue exposure
- Scenario-based decision support

## Folder structure

````
/hotel_demand_dataset.csv
/README.md
/EDA.ipynb
/dashboard.pbix
````

## Useful Link:
Portfolio: 
LinkedIn: 


