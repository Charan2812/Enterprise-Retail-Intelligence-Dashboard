# ⚙️ Power Query Transformations  
### Complete ETL Documentation  
This document describes all data preparation steps performed in Power Query as part of the Enterprise Retail Intelligence Dashboard.

Power Query (M) is used for:
- Data cleaning  
- Standardization  
- Combining datasets  
- Preparing relationships  
- Ensuring data model quality  
- Creating a star-schema optimized for Power BI  

# 1️⃣ Global Transformations Applied Across All Tables

### ✔ Data Type Standardization
- Converted dates to **Date** type  
- OrderQuantity, ProductKey, CustomerKey, TerritoryKey → **Whole Number**  
- Revenue, Retail Price, Product Cost → **Decimal Number**  
- Category, Region, Subcategory, Product Name → **Text**

### ✔ Header Cleanup
- Promoted first rows to headers  
- Renamed columns for consistency  
- Removed unnecessary prefixes/suffixes (e.g., `dim_`, `tbl_`)

### ✔ Data Cleanup
- Removed blank rows  
- Replaced nulls with default values when safe  
- Trimmed and cleaned text fields  
- Removed errors  
- Ensured key columns were not null for fact tables  

# 2️⃣ Table-Specific Transformations

## 📦 Product Lookup (Dimension)
### Transformations:
- Split `ProductName` into:
  - ModelName  
  - ProductStyle  
- Added SKU formatting column  
- Merged with **Product Categories Lookup** using `ProductCategoryKey`  
- Merged with **Product Subcategories Lookup** using `ProductSubcategoryKey`  
- Cleaned product descriptions  
- Converted cost and price columns to Decimal type  

### Result:
A clean dimension supporting:
**Category → Subcategory → Product drill-down hierarchy**

## 🧩 Product Categories Lookup
- Removed duplicate categories  
- Cleaned category names  
- Ensured `ProductCategoryKey` is unique  

## 🧩 Product Subcategories Lookup
- Renamed columns for clarity  
- Ensured valid link to `ProductCategoryKey`  
- Removed duplicates  
- Sorted alphabetically  

## 👤 Customer Lookup (Dimension)
### Transformations:
- Combined FirstName + LastName into `Full Name`  
- Added derived fields:
  - BirthYear  
  - IsParent  
  - IncomeLevel  
- Cleaned demographic fields:
  - Gender  
  - Education  
  - HomeOwner  
  - Occupation  
- Standardized marital status  
- Removed invalid or incomplete customer records  

## 🌍 Territory Lookup (Dimension)
### Transformations:
- Standardized `Continent`, `Country`, `Region` naming  
- Removed inconsistencies (e.g., “USA” vs “United States”)  
- Ensured `SalesTerritoryKey` has unique values  
- Sorted for clean hierarchy use  
- Prepared hierarchy: **Continent → Country → Region**

## 💵 Sales Data (FACT TABLE)
This is your central fact table, so PQ cleaning is crucial.

### Transformations:
- Converted OrderDate & StockDate to Date type  
- Validated OrderQuantity > 0  
- Ensured numerical types for Revenue, RetailPrice  
- Merged with Product Lookup to validate ProductKey  
- Merged with Customer Lookup to ensure CustomerKey integrity  
- Removed cancelled or incomplete orders  
- Added calculated fields:
  - **Line Revenue** = OrderQuantity × Retail Price  
  - **Normalized OrderNumber** (if required)  
- Removed errors arising from joins  

### Result:
A clean, transaction-level table ready for DAX and analytics.

## 🔁 Returns Data (FACT)
### Transformations:
- Converted ReturnDate to Date  
- Ensured ReturnQuantity is numeric  
- Merged with Product Lookup to validate ProductKey  
- Cleaned up null or invalid TerritoryKey  
- Removed entries where ReturnQuantity = 0  
- Ensured referential integrity with Calendar & Territory tables  

## 📆 Calendar Lookup (Dimension)
### Transformations:
- Generated a continuous calendar range  
- Added derived fields:
  - Year  
  - Month  
  - Quarter  
  - Start of Week  
  - Start of Month  
  - Start of Quarter  
  - Day Name  
  - IsWeekend  
- Marked as **Date Table**  

## 🔄 Rolling Calendar (Helper Table)
### Transformations:
- Start/End boundaries for rolling windows  
- Added:
  - Rolling 10-day anchor  
  - Rolling 30-day anchor  
  - Start of Month  
  - Start of Quarter  
- Used for rolling KPI calculations (Revenue, Profit, Orders)  

## 🎚 What-If Parameter Tables

### 💲 Price Adjustment Percentage
Created using DAX in Modeling (not PQ), but included for completeness.

- DAX
GENERATESERIES(-1, 1, 0.1)

