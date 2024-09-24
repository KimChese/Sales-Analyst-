# Sales-Analyst
# AdventuresWork Sales Analyst Project

## Project Overview
The AdventureWorks Sales Analyst project leverages Power BI and SQL to analyze sales data and extract actionable insights. The focus of the analysis is on understanding regional sales performance, product category trends, and identifying growth opportunities across different sub-categories.

### Tools Used:
- **SQL**: Used for data extraction, cleaning, and aggregation.
- **Power BI**: Used for visualizing sales insights and creating a dashboard.


### Key Insights:
**Sales Performance by Region**:
North America is the leading region, contributing 71.85% of the total sales.
Europe follows with 22.44%, while the Pacific region contributes 5.71%, showing growth potential.
**Top Performing Products**:
Bikes are the top-selling product category, accounting for approximately 40% of total sales revenue.
Other high-performing categories include Accessories and Clothing.
**Sales Key Insights by Region**:
The following are the top 10 sub-categories for each region, showcasing regional sales differences:
Region	Top Sub-Categories	Revenue (USD)

**Bottom 10 Sub-Category Revenue**:
Sub-categories such as Chains, Locks, and Socks rank among the lowest in terms of sales, though they still contribute to overall revenue.
There is potential to explore strategies to optimize these categories and boost their performance.
## Dashboard Preview
Here’s a preview of the Power BI dashboard created for this project:
![image](https://github.com/user-attachments/assets/a4851918-c8a5-4152-b530-f7fca9572663)


Creating Model Relationship between Table
<img width="728" alt="Model relationship " src="https://github.com/user-attachments/assets/3e02a5c5-413a-435a-bef0-51ebea78b23e">

The full dashboard file is available [here]https://drive.google.com/file/d/13AsjpE59YyU_orxxG_WdxcDo3xW8EEbW/view?usp=sharing.

## SQL Queries


USE AdventureWorksDW2019;
GO
CREATE VIEW dbo.Customer_view AS
select
    f.CustomerKey,
    CONCAT(FirstName,' ', LastName) as FullName,
    SalesTerritoryCountry,
    YEAR(OrderDate) as OrderYear,
    COUNT(distinct SalesOrderNumber) as NumberOfOrder,
    round(sum(SalesAmount*EndOfDayRate),2) as TotalSalesUSD,
    round(sum((TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalCostUSD,
    round(sum(SalesAmount*EndOfDayRate-(TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalProfitUSD
from FactInternetSales f
left join DimCustomer c on f.CustomerKey=c.CustomerKey
left join FactCurrencyRate cr on f.CurrencyKey=cr.CurrencyKey and f.OrderDateKey=cr.DateKey
left join DimSalesTerritory terri on f.SalesTerritoryKey = terri.SalesTerritoryKey
group by f.CustomerKey, FirstName, LastName, SalesTerritoryCountry, YEAR(OrderDate);
Go


USE AdventureWorksDW2019;
GO
CREATE VIEW dbo.Reseller_view AS
select
    f.ResellerKey,
    ResellerName,
    SalesTerritoryCountry,
    YEAR(OrderDate) as OrderYear,
    COUNT(distinct SalesOrderNumber) as NumberOfOrder,
    round(sum(SalesAmount*EndOfDayRate),2) as TotalSalesUSD,
    round(sum((TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalCostUSD,
    round(sum(SalesAmount*EndOfDayRate-(TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalProfitUSD
from FactResellerSales f
left join DimReseller r on f.ResellerKey=r.ResellerKey
left join FactCurrencyRate cr on f.CurrencyKey=cr.CurrencyKey and f.OrderDateKey=cr.DateKey
left join DimSalesTerritory terri on f.SalesTerritoryKey = terri.SalesTerritoryKey
group by f.ResellerKey, ResellerName, SalesTerritoryCountry, YEAR(OrderDate)
;
GO

USE AdventureWorksDW2019;
GO
CREATE VIEW dbo.Reseller_view AS
select
    f.ResellerKey,
    ResellerName,
    SalesTerritoryCountry,
    YEAR(OrderDate) as OrderYear,
    COUNT(distinct SalesOrderNumber) as NumberOfOrder,
    round(sum(SalesAmount*EndOfDayRate),2) as TotalSalesUSD,
    round(sum((TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalCostUSD,
    round(sum(SalesAmount*EndOfDayRate-(TotalProductCost+TaxAmt+Freight)*EndOfDayRate),2) as TotalProfitUSD
from FactResellerSales f
left join DimReseller r on f.ResellerKey=r.ResellerKey
left join FactCurrencyRate cr on f.CurrencyKey=cr.CurrencyKey and f.OrderDateKey=cr.DateKey
left join DimSalesTerritory terri on f.SalesTerritoryKey = terri.SalesTerritoryKey
group by f.ResellerKey, ResellerName, SalesTerritoryCountry, YEAR(OrderDate)
;
GO


