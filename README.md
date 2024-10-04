# Electric-Vehicle-Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Questions](#questions)
- [Results/Findings](#resultsfindings)

### Project Overview
This project utilizes a dataset of Battery Electric Vehicles (BEVs) and Plug-in Hybrid Electric Vehicles (PHEVs) registered with the Washington State Department of Licensing (DOL). By using SQL, I aim to uncover patterns and trends in the data that can promote electric vehicle adoption and enhance the overall market for clean transportation.

The goal is to clean and analyze the dataset to derive valuable insights that support data-driven decision-making.

### Data Source
https://www.kaggle.com/datasets/rajkumarpandey02/electric-vehicle-population-data

### Tools
MS SQL Server Management Studio - SQL

### Data Cleaning/Preparation
- Create a temporary table
- Renaming a column
- Use ‘TRIM’ to remove all unwanted spaces from all text columns
- Check for duplicates
- Delete records where any of the specified columns are NULL or empty strings

### Questions

- Which electric vehicle manufacturers have the top 10 highest market shares?
- What is the distribution of the top 10 electric vehicles across different manufacturers and models?
- What are the trends in electric vehicle registrations by model year?
- Which electric utilities have the top 5 highest numbers of registered electric vehicles?
- How are the top 10 electric vehicles distributed across different legislative districts?
- What is the count of different types of electric vehicles?
- How has the total number of battery electric vehicles (BEVs) changed over the years?
- How has the total number of plug-in hybrid electric vehicles (PHEVs) changed over the years?
- What proportion of electric vehicles falls under different eligibility statuses for clean alternative fuel vehicle programs?

### Results/Findings
#### Which electric vehicle manufacturers have the top 10 highest market shares?

```sql
SELECT TOP 10 Make AS Manufacturer, Count(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Make
ORDER BY Total_Vehicles DESC;
```
<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res1.png" alt="First Image" width="200"/>

The analysis of electric vehicle (EV) reveals that Tesla dominates the landscape with a significant lead, boasting a market share of 68,821 units sold. Following Tesla, Nissan and Chevrolet rank as the next highest manufacturers, but their numbers are substantially lower at 13,481 and 12,003 units, respectively. The rest of the top ten, demonstrate a more fragmented market with sales ranging from approximately 3,283 to 7,592 units, indicating a diverse but competitive EV industry.


#### What is the distribution of the top 10 electric vehicles across different manufacturers and models?

```sql
SELECT TOP 10 Make AS Manufacturer, Model, Count(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Make, Model
ORDER BY Total_Vehicles DESC;
```

<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res2.png" alt="First Image" width="200"/>

The distribution of the top 10 electric vehicles reveals that Tesla leads the market with four models: Model Y, Model 3, Model S, and Model X, accounting for the highest sales figures, particularly the Model Y and Model 3 with 28,456 and 27,626 units, respectively. Nissan’s Leaf, with 13,171 units sold, is the only non-Tesla model to break the top five, indicating strong brand loyalty for Tesla’s offerings. Chevrolet’s Bolt EV and Volt come next, while Volkswagen’s ID.4, Kia’s Niro, and Chrysler’s Pacifica have much lower sales. This shows that although there is competition, Tesla still holds a strong lead in the EV market with a wide range of models.

#### What are the trends in electric vehicle registrations by model year?

```sql
SELECT Model_Year, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Model_Year
ORDER BY Model_Year;
``

<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res3.png" alt="First Image" width="200"/>

The data on electric vehicle registrations by model year shows a clear upward trend, with registrations increasing significantly over the years. Starting from just 1 registration in 1997, there was a gradual rise until 2008, after which growth accelerated sharply, peaking at 37,052 registrations in 2023. This upward trajectory indicates a growing acceptance and adoption of electric vehicles, though a small decline is expected in 2024. Overall, the trend highlights a strong growth in the EV market, reflecting increasing consumer interest and market expansion.

#### Which electric utilities have the top 5 highest numbers of registered electric vehicles?

```sql
SELECT TOP 5 Electric_Utility, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Electric_Utility
ORDER BY Total_Vehicles DESC;
```

<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res4.png" alt="First Image" width="200"/>

The data reveals that Puget Sound Energy Inc. dominates the electric vehicle registrations, with its highest total reaching 55,634 units. Another entry from Puget Sound Energy follows with 29,865 registrations. The City of Seattle, in partnership with the City of Tacoma, ranks third with 27,268 registered EVs. The Bonneville Power Administration appears twice in the top five, with 8,643 and 6,622 registrations. Overall, these figures demonstrate strong leadership by Puget Sound Energy INC in promoting electric vehicles.

#### How are the top 10 electric vehicles distributed across different legislative districts?

```sql
SELECT TOP 10 Legislative_District, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Legislative_District
ORDER BY Total_Vehicles DESC;
```
<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res5.png" alt="First Image" width="200"/>

The distribution of the top 10 electric vehicles across different legislative districts shows significant variation in registrations. District 41 leads with 9,969 registrations, followed by District 45 with 9,171 and District 48 with 8,419. Other districts, like 1, 36, and 5, have good numbers but have less than 7,000 registrations. The data shows that some districts are more engaged in adopting electric vehicles, while others have fewer registrations. This suggests there are different levels of consumer interest and access to EV options.

#### What is the count of different types of electric vehicles?

```sql
SELECT Electric_Vehicle_Type, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
GROUP BY Electric_Vehicle_Type
ORDER BY Total_Vehicles DESC;
```
<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res6.png" alt="First Image" width="200"/>

Battery Electric Vehicles (BEVs) are the most common type of electric vehicle sold in the market, with 116,583 units, which is 83,029 units higher or approximately 247.7% more than Plug-in Hybrid Electric Vehicles (PHEVs), which have only 33,554 units. 

#### How has the total number of battery electric vehicles (BEVs) changed over the years?

```sql
SELECT Model_Year, Electric_Vehicle_Type, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
WHERE Electric_Vehicle_Type = 'Battery Electric Vehicle (BEV)'
GROUP BY Model_Year, Electric_Vehicle_Type
ORDER BY Model_Year;
```
<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res7-1.png" alt="First Image" width="200"/>

The data indicates a significant increase in the number of Battery Electric Vehicles (BEVs) registered over the years, starting from just 1 unit in 1997 and rising to 31,340 units by 2023. This shows a strong upward trend in consumer adoption and market acceptance of BEVs. However, there is a notable decline in registrations projected for 2024, which may suggest market fluctuations or changing consumer preferences. 

#### How has the total number of plug-in hybrid electric vehicles (PHEVs) changed over the years?

```sql
SELECT Model_Year, Electric_Vehicle_Type, COUNT(*) AS Total_Vehicles
FROM #temp_electric_vehicle
WHERE Electric_Vehicle_Type = 'Plug-in Hybrid Electric Vehicle (PHEV)'
GROUP BY Model_Year, Electric_Vehicle_Type
ORDER BY Model_Year;

```

<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res7-2.png" alt="First Image" width="200"/>

Plug-in Hybrid Electric Vehicle (PHEV) registrations also shows a generally increasing trend from 2010 to 2023, starting with just 3 units in 2010 and peaking at 5,712 units in 2023, the data shows a noticeable decreases in some years, particularly in 2015 and 2020. The sharp drop to only 371 registrations projected for 2024 suggests potential challenges or shifts in consumer interest away from PHEVs.

#### What proportion of electric vehicles falls under different eligibility statuses for clean alternative fuel vehicle programs?

```sql
WITH VehicleCounts AS (
    SELECT 
        Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility, 
        COUNT(*) AS Total_Vehicles
    FROM 
        #temp_electric_vehicle 
    WHERE 
        Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility IN ('Clean Alternative Fuel Vehicle Eligible', 'Not eligible due to low battery range', 'Eligibility unknown as battery range has not been researched')
    GROUP BY 
        Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility
),
TotalCounts AS (
    SELECT 
        SUM(Total_Vehicles) AS Overall_Vehicles
    FROM 
        VehicleCounts
)

SELECT 
    vc.Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility, 
    vc.Total_Vehicles, 
    ROUND (CAST(vc.Total_Vehicles AS FLOAT) / tc.Overall_Vehicles * 100, 2) AS Percentage 
FROM 
    VehicleCounts vc,
    TotalCounts tc
ORDER BY 
    vc.Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility;
```

<img src="https://github.com/angelicamerced/Electric-Vehicle-Analysis/blob/main/images/res8.png" alt="First Image" width="200"/>

The distribution of electric vehicles by eligibility status for clean alternative fuel vehicle programs shows that a significant portion, 41.82%, is eligible, totaling 62,792 units. However, a larger share, 46.34% (69,580 units), falls into the category of unknown eligibility due to insufficient research on battery range. Additionally, 11.83% (17,765 units) are deemed not eligible because of low battery range. This indicates that while many vehicles qualify for clean alternative programs, a considerable number remain unassessed or ineligible based on battery performance.









