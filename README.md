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
A high-level view of sales, profit, and volume, filtered by Year (fiscal year) and Region slicers.

- Sum of Sales and Profit by Month: columns show monthly sales and a dotted line shows profit, across the fiscal year
- Sum of Sales by Category and Group: stacked columns showing each product category's sales split by sales group
- Sum of Quantity by Category: bar chart of units sold per category (for FY2019: Bikes 27.8K, Clothing 24.9K, Components 19.2K, Accessories 7.1K)
<img width="976" height="515" alt="Overview" src="https://github.com/user-attachments/assets/0b602b8a-e64c-467a-be33-d6348204201b" />

### 2. Profit
A detailed profitability breakdown, filtered by a Region slicer.

- Matrix that drills down from Year → Quarter → Month using the fiscal calendar
- Shows Orders, Sum of Sales, Sum of Cost, Profit, and Profit Margin at every level, with subtotals
- Conditional formatting highlights the figures, and losses appear in brackets, for example ($353,510)
<img width="977" height="541" alt="Profit" src="https://github.com/user-attachments/assets/8bb85fd4-025f-4c55-b819-bac8a133ff67" />

### 3. My Performance

Actual sales compared with targets, filtered by a Year slicer.

- KPI card showing Sum of Sales, Target, Variance, and Variance Margin
- Clustered column chart comparing monthly sales with the monthly target
- Bar Chart / Column Chart buttons that let the user switch the chart type
  <img width="985" height="555" alt="Performance" src="https://github.com/user-attachments/assets/db6975c0-21a1-4fd6-a502-bbfb4c8d9012" />

### 4. Product Details (drill-through)

A hidden detail page reached by drilling through from a product category, with a back button to return to the main report.

- Lists each subcategory with its colour, quantity sold, sales, and profit margin, with a total row
- Colour cells match the product colours
- Conditional formatting icons on profit margin: a green circle for healthy margins and a red diamond for negative margins
- Shown here for the Components category: about 46,472 units and $11.2M in sales at an 8.92% margin
  <img width="956" height="547" alt="Product Details" src="https://github.com/user-attachments/assets/126e597d-3cd3-44a3-8d61-58cb46aa32a6" />












