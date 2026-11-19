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
| **Salesperson (Performance)** | Bridge |Links salespeople to the sales territories (regions) they cover | 
| **Targets** | Dimension | Sales targets used for variance analysis |

#### Hierarchies created: 
Region,Product,Reseller geography,and Date (Fiscal).

### Data model image
<img width="960" height="531" alt="Data model image" src="https://github.com/user-attachments/assets/f0a4d645-ca21-4522-aea2-e84f4cb4806b" /> 

### DAX Measures:


Measures are organised into display folders in the Sales table:
| Folder | Measures | What they answer |
|---|---|---|
| **Count** | Order Lines, Orders | How many orders and order lines were placed |
| **Pricing** | Avg Price, Max Price, Median Price, Min Price | How selling prices are distributed |
| **Profitability** | Profit, Profit Margin | How much profit was made, and as a % of sales |
| **Ratio** | Sales % of All, Sales % of Group | Each item's share of total or group sales |
| **Time Intelligence** | Sales YoY Growth, Sales YTD | Growth versus last year and year-to-date totals |
| **Targets table** | Target, Variance, Variance Margin | Actual performance against target |

### Featured Measures:


```
Profit = [SUM('Sales'[Sales]) - SUM('Sales'[Cost])]

Profit Margin = [DIVIDE([Profit], SUM('Sales'[Sales]))]

Sales YTD = [TOTALYTD(SUM(Sales[Sales]),'Date'[Date],"6-30")]

Sales YoY Growth = 
VAR SalesPriorYear =
	CALCULATE(
		SUM(Sales[Sales]),
		PARALLELPERIOD(
			'Date'[Date],
			-12,
			MONTH
		)
	)
RETURN
	DIVIDE(
		(SUM(Sales[Sales]) - SalesPriorYear),
		SalesPriorYear
	)]

Variance =
IF(
	HASONEVALUE('Salesperson (Performance)'[Salesperson]),
	SUM(Sales[Sales]) - [Target]
)]
```

## Report Pages

The report has four pages, each focused on a different question.

### 1. Overview
- the Year and Region slicers
- the sales and profit chart by month
- sales by category and group
- quantity by category (Bikes 27.8K down to Accessories 7.1K).
<img width="976" height="515" alt="Overview" src="https://github.com/user-attachments/assets/0b602b8a-e64c-467a-be33-d6348204201b" />










