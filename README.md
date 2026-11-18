# Sales-Data-Analysis-with-Power-BI
An end-to-end sales analysis built during my Data Analysis training at Incubator Hub. The project covers the full Power BI workflow: extracting raw sales data, cleaning it in Power Query, modelling it in Power BI Desktop, analyzing it with DAX measures, and presenting the results in an interactive dashboard.
### Project Overview
Raw sales data rarely arrives ready for decision-making. The goal of this project was to turn a raw sales dataset into a clean, reliable data model and an interactive report that answers real business questions.


##### What this project demonstrates:


- Importing and cleaning data with Power Query
- Building table relationships in a data model
- Creating a calculated date table for time intelligence
- Writing DAX measures for business KPIs
- Designing an interactive, multi-visual dashboard

## Tools & Skills
| Area | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **Data Preparation** | Power Query (extract, clean, transform) |
| **Data Modelling** | Relationships, calculated date table |
| **Analysis** | Dax measures |
| **Visualization** | Interactive Power BI report |

### Project Workflow

#### 1. Data Extraction
 Connected Power BI to the source sales data (Excel / CSV / folder).
#### 2. Data Cleaning & Transformation (Power Query) 
- Promoted headers and set correct data types
- Removed duplicates and blank/null rows
- Standardised text values (trim, proper case)
- Renamed columns for clarity
- Created derived columns where needed
#### 3. Data Modelling
- Loaded the cleaned tables into Power BI Desktop
- Created relationships between the tables
- Built a calculated date table with DAX
#### 4. Analysis with DAX
  Created measures to calculate the core KPIs and grouped them into folders (see DAX Measures).
#### 5. Visualisation
Built a four-page report with charts, tables, slicers, and conditional formatting for interactive exploration (see Report Pages).


#### Data Model

| Table | Type | Purpose
|---|---|---|
| **Sales** | 	Fact | Sales, cost, quantity, and unit price transactions |
| **Date** | Dimension | Calculated date table with year, quarter, month, and fiscal hierarchy |
| **Product** | Dimension | Category, subcategory, product, colour, and standard cost |
| **Region** | Dimension | Sales regions (with hierarchy) |
| **Reseller** | Dimension | 	Business type and geography (country, state/province, city) |
| **Salesperson** | Dimension | Dimension |
| **Salesperson (Performance)** | Supporting | Used for the salesperson performance view | 
| **Targets** | Dimension | Sales targets used for variance analysis |







