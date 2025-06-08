# Adventure Works Cycles Power BI Report

## Purpose

This Power BI project delivers an end-to-end business intelligence solution for **Adventure Works Cycles**, simulating a first-consultant engagement. The report surfaces key metrics—including sales, costs, margins, quotas, and shipping performance—to support executive decision-making and meet detailed business requirements.

## Data Sources

* **AdventureWorks2017 OLTP**: Downloaded from the official Microsoft sample repository: [AdventureWorks2017 Installation & Configuration](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver17&tabs=ssms)
* **AW Quota.xlsx**: Quarterly sales quota data.
* **ExchangeRates.csv**: Static USD→local currency exchange rates.
* **Validation Reports.xlsx**: Example verification reports provided by the business.

## Data Preparation & Adjustments

To introduce realistic data-quality challenges, the provided SQL script (`scripts/AW-2017.update_script.sql`) was applied to the AdventureWorks2017 database:

1. **Duplicate Vendor Cleanup**: Marked duplicate vendors as non-preferred.
2. **Salesperson Pruning**: Removed extraneous entries from `SalesTerritoryHistory`.
3. **ShipDate Randomization**: Recalculated `ShipDate` around each order’s due date using a weighted distribution.
4. **Schema Simplification**: Dropped the obsolete `SalesPersonID` column.
5. **Employee Hierarchy**: Added and populated `ParentBusinessEntityID` to support a true organizational hierarchy.
6. **Territory History Normalization**: Aligned territory start/end dates to fiscal-quarter boundaries.

## Key Features

* **Fiscal Calendar Support**: Uses Adventure Works’ July–June fiscal year for all time-intelligence calculations.
* **Row-Level Security**: Simulated so that sales reps see only their own data.
* **Currency Toggle**: Switch between USD and local currencies using provided exchange rates.
* **Slowly Changing Dimensions**: Models territory assignments over time correctly.
* **Rolling & Point-in-Time Reporting**: Compare current vs. prior periods dynamically (e.g., rolling 12‑month).
* **Advanced Metrics**: Includes on-time shipment %, sales vs. quota variance, and special benchmarks (e.g., SalesComp, QuantityComp).

## Repository Structure

```plaintext
├── AdventureWorks2017.bak              # SQL Server backup
├── scripts/
│   └── AW-2017.update_script.sql      # Data-prep & complexity script
├── data/
│   ├── AW Quota.xlsx                  # Sales quota reference
│   ├── ShippingMethod.csv             # Shipping lookup
│   ├── ExchangeRates.csv              # USD-to-local exchange rates
│   └── Validation Reports.xlsx        # Business verification samples
├── CEO_Internet_Resellers.pbix        # Power BI report file
├── images/
│   └── screenshot.png                 # Sample dashboard preview
└── README.md                          # Project overview and instructions
```

## Getting Started

1. **Restore Database**

   * Load `AdventureWorks2017.bak` into your SQL Server instance.
2. **Apply Adjustments**

   * Run `scripts/AW-2017.update_script.sql` against the restored database.
3. **Open Report**

   * Launch `CEO_Internet_Resellers.pbix` in Power BI Desktop (v2.XX+) and update the data source to your SQL connection.
4. **Explore & Analyze**

   * Use slicers, bookmarks, and visuals to investigate sales, margins, quotas, and shipping KPIs.



## Performance Optimization

* To ensure peak report responsiveness, the **Measure Killer** tool was employed to analyze and streamline DAX measures, reducing redundant calculations and improving overall query performance.


---

*This solution demonstrates best practices in data modeling, DAX calculations, and report design tailored to Adventure Works Cycles’ business needs.*

