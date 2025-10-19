# Automobile-dashboard
🚗 Automobile Data Analysis Dashboard (Power BI)
Project Overview :This Power BI project analyzes an Automobile dataset to uncover insights about car pricing, performance, fuel efficiency and manufacturer trends.  It includes data cleaning, transformation and advanced DAX calculations to deliver an interactive dashboard with drill-throughs, dynamic filters and KPIs.

 Dataset Information
Dataset name: `Automobile_data.csv`  
Source: Sample automobile dataset containing car specifications, pricing, and fuel efficiency metrics.

Key Columns:
- `make` – Car manufacturer  
- `fuel-type` – Fuel type (gas/diesel)  
- `body-style` – Type of body (sedan, hatchback, etc.)  
- `price` – Market price  
- `horsepower`, `engine-size` – Performance indicators  
- `city-mpg`, `highway-mpg` – Fuel efficiency  

Data Cleaning & Preparation:
Data transformation was performed in Power Query:
1. Removed duplicates and missing values  
2. Corrected column names (snake_case → proper format)  
3. Converted data types (numeric, text, etc.)  
4. Created calculated columns for:
   - `Price Category` (Low, Medium, High)
   - `Full Tank Range (Highway)` = `[highway-mpg] * 15`
   - `Power_to_Weight` and other ratios

 📊 Dashboard Features
**KPIs**
Aligned and locked single-row KPIs at the top:
- Total Cars  
- Average Price  
- Average Horsepower  
- Average City MPG  

 **Visuals**
| Visual | Purpose |
|---------|----------|
| Bar Chart | Car count by manufacturer |
| Pie/Donut Chart | Fuel-type distribution |
| Column Chart | Avg horsepower by body style |
| Scatter Chart | Engine size vs Price |
| Table | Car details with dynamic filtering |

 **Slicers**
- `Make`
- `Fuel-Type`
- `Body-Style`
- `Drive-Wheels`
- `Price Category`

**Drill-Through Page**
- Created *Manufacturer Deep Dive* page filtered by `make`  
- Displays detailed models, prices, and horsepower  

**Enhanced Tooltips**
- Custom tooltip page shows `make`, `horsepower`, and `engine-size` on hover  

 **Dynamic Top N Filter**
- Parameter table using `GENERATESERIES(1,20,1)`  
- Dynamic DAX measure ranks top N cars by price  

**Parent-Child Hierarchy**
- `Make → Body-Style → Fuel-Type` hierarchy for drill-down visuals  

**Row-Level Security**
Defined roles under **Model → Manage Roles**:
```DAX
[make] = "honda".

Key DAX Measure-
# Average_Price = AVERAGE(Automobile[price])

# Total_Cars = COUNTROWS(Automobile)

# Avg_DieselPrice =
CALCULATE(AVERAGE(Automobile[price]), Automobile[fuel-type] = "diesel")

# High_HP_Cars =
COUNTROWS(FILTER(Automobile, Automobile[horsepower] > 150))

# Price_Category =
SWITCH(TRUE(),
    Automobile[price] < 10000, "Low",
    Automobile[price] < 25000, "Medium",
    "High"
)

# Summary_Table =
SUMMARIZECOLUMNS(
    Automobile[make],
    "Average Price", AVERAGE(Automobile[price]),
    "Average Horsepower", AVERAGE(Automobile[horsepower]),
    "Average City MPG", AVERAGE(Automobile[city-mpg])
).

 Business Problem:
The automobile market includes a wide variety of vehicles differing by price, body style, performance, and fuel efficiency.  
However, management teams often lack visibility into which manufacturers, fuel types or body styles are driving profitability and efficiency.  

 The objective of this dashboard is to help stakeholders:
- Identify top-performing manufacturers and underperforming segments.  
- Understand how engine characteristicsimpact price and fuel efficiency.  
- Support data-driven decisions for marketing, production and pricing strategies.

 Key Business Questions:
1. How many cars does each manufacturer produce?  
2. What is the average price of cars across makes and fuel types?  
3. How does horsepower vary by body style?  
4. Which are the Top N most expensive cars?  
5. What is the relationship between engine size and price?  
6. How do fuel types (gas vs diesel) compare in terms of price and efficiency?  
7. What are the most fuel-efficient makes or models?  
8. How do city-mpg and highway-mpg correlate across fuel types?  
9. Which car segments (Low, Medium, High price) dominate the market?  
10. How can management drill into a specific manufacturer’s performance?.

 Business Impact:
✅ Improved decision-making for pricing and marketing through real-time insights.  
✅ Helped management understand manufacturer-wise performance and market share.  
✅ Identified inefficient or low-performing car models for potential optimization.  
✅ Enhanced reporting transparency by implementing Row-Level Security.  
✅ Enabled dynamic filtering to view Top N cars based on user-selected thresholds.  
✅ Supported strategic planning by comparing gas vs diesel market trends.  
✅ Simplified analysis with intuitive KPIs and interactive visuals.

 Insights Derived
Top Manufacturers:  Certain brands consistently produce higher-priced vehicles, indicating premium positioning.   Engine vs Price Correlation: Cars with larger engine sizes generally command higher prices, confirming performance-value linkage.  
Fuel Type Trend: Gas cars dominate the market, but diesel models offer higher highway efficiency.  
Underperforming Segments:Some body styles (e.g., hatchbacks) show lower average prices and horsepower, suggesting cost-driven appeal.  
Efficiency Insight: A balance between horsepower and MPG defines mid-segment cars that appeal to fuel-conscious buyers.  
Dynamic Insights:Using slicers and bookmarks, stakeholders can instantly switch between views to compare fuel categories and manufacturers.

 Conclusion:
This Power BI Automobile Dashboard transforms raw automotive data into actionable business insights.  
It empowers decision-makers to evaluate pricing, performance, and efficiency at every level — from brand to model — enabling smarter, data-driven strategies in the automobile industry.



