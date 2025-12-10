# 📘 Data Dictionary

This document provides detailed descriptions of all tables and fields used in the Enterprise Retail Intelligence Dashboard.  
It helps users understand the structure, purpose, and meaning of each dataset.

## 📅 Calendar Lookup (Date Table)

The **Calendar Lookup** table is a foundational date dimension used for all time-intelligence calculations in the dashboard.  
It enables Month-over-Month, Year-to-Date, rolling averages, and seasonality analysis.

### 📌 Columns in the Date Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Date | Date | The unique calendar date; primary key of the table. |
| Day Name | Text | Full name of the day (Monday, Tuesday, etc.). |
| Day of Week | Whole Number | Numeric representation of the weekday (e.g., 1 = Monday). |
| Month | Whole Number | Month number (1–12). |
| Month Name | Text | Full month name (January–December). |
| Month Number (SWITCH) | Whole Number | Custom month number used for sorting or switching logic. |
| Month Short | Text | Abbreviated month name (Jan, Feb, etc.). |
| Start of Month | Date | First day of the calendar month. |
| Start of Quarter | Date | First day of the quarter (Q1, Q2, Q3, Q4). |
| Start of Week | Date | Start date of the week (based on chosen week start setting). |
| Start of Year | Date | First day of the calendar year. |
| Weekend | Boolean | Indicates whether the date falls on a weekend. |
| Year | Whole Number | The year extracted from the date field. |

### 📝 Notes
- This table is marked as a **Date Table** in Power BI to enable advanced time intelligence.  
- Columns like **Start of Month**, **Start of Quarter**, and **Start of Week** support grouping and rolling metrics.  
- The **Month Number (SWITCH)** column is often used when overriding default month sorting.  

### 🎯 Business Purpose
The Calendar Lookup table is essential for:
- Trending Revenue, Profit, Returns, and Orders  
- Creating rolling 10-day / 90-day metrics  
- Comparing current vs previous periods  
- Year-to-date and month-to-date calculations


## 👤 Customer Lookup (Customer Dimension)

The **Customer Lookup** table contains demographic and behavioral attributes about each customer.  
It is used for segmentation, customer analytics, lifetime value calculations, and targeted insights such as income-based or occupation-based ordering behavior.

### 📌 Columns in the Customer Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| AnnualIncome | Whole Number / Decimal | Customer's annual income used for income segmentation. |
| Birth Year | Whole Number | Year of birth for age-based analysis. |
| BirthDate | Date | Full date of birth (may be used to calculate precise age). |
| Customer Full Name (CC) | Text | Concatenated customer full name (cleaned & standardized). |
| Customer Priority | Text / Category | Indicates priority segment or customer tier. |
| CustomerKey | Whole Number | Primary key identifying each customer uniquely. |
| Domain Name | Text | Email domain (e.g., gmail.com); useful for marketing segmentation. |
| EducationLevel | Text | Customer’s highest level of education. |
| EmailAddress | Text | Customer’s email contact details. |
| FirstName | Text | Customer first name. |
| Full Name | Text | Full name derived from FirstName + LastName. |
| Gender | Text | Gender of the customer. |
| HomeOwner | Boolean | Indicates whether the customer owns a home. |
| Income Level | Text (Low / Average / High) | Derived category used for income-based segmentation. |
| Is Parent? | Boolean | Indicates if the customer has children. |
| LastName | Text | Customer last name. |
| MaritalStatus | Text | Customer marital status (Single, Married, etc.). |
| Occupation | Text | Customer’s job role/category (Professional, Skilled Manual, Management). |
| Prefix | Text | Title prefix (Mr., Ms., Mrs., etc.). |
| TotalChildren | Whole Number | Number of children for deeper demographic segmentation. |

### 📝 Notes
- This table is used heavily on the **Customer Insights Dashboard**.  
- Columns like **Income Level**, **Occupation**, and **EducationLevel** support demographic segmentation visuals.  
- Parent/children fields help build family-oriented customer profiles.  
- HomeOwner and MaritalStatus allow more detailed lifestyle segmentation.  

### 🎯 Business Purpose
This dimension enables:
- Customer segmentation  
- High-value customer identification  
- Behavioral trend analysis (orders by income, occupation, family status)  
- Personalized marketing opportunities  

## 👥 Customer Metrics Selection (Parameter Table)

The **Customer Metrics Selection** table is a DAX-generated parameter table used to enable dynamic switching between customer-related KPIs in the dashboard.  
This table allows users to interactively choose which measure they want to visualize, such as Total Customers or Revenue per Customer.

It enhances dashboard flexibility and improves user experience by eliminating the need for multiple static visuals.

### 📌 Columns in the Customer Metrics Selection Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Customer Metrics Selection | Text | Display name of the metric option shown to the user (e.g., "Total Customers"). |
| Customer Metrics Selections Fields | Text | Stores the fully qualified DAX measure reference used by the selection (e.g., `'Measure Table'[Total Customers]`). |
| Customer Metrics Selections Order | Whole Number | Defines the order in which the metrics appear in the slicer or selection panel. |

### 🧠 How It Works

This table is generated through a DAX expression like:

- DAX
Customer Metrics Selection = {
    ("Total Customers", NAMEOF('Measure Table'[Total Customers]), 0),
    ("Revenue per Customer", NAMEOF('Measure Table'[Revenue per Customer]), 1)
}

## 💲 Price Adjustment Percentage (What-If Parameter Table)

The **Price Adjustment Percentage** table is a DAX-generated *what-if parameter* that allows users to simulate changes in product pricing.  
Using this parameter, the dashboard can dynamically recalculate revenue, profit, and margin under different pricing scenarios.

This enables powerful business use cases such as discount impact analysis and price sensitivity modeling.

---

### 📌 Table Definition (DAX)

- DAX
Price Adjustment Percentage =
    GENERATESERIES(-1, 1, 0.1)

## 🛍️ Product Categories Lookup

The **Product Categories Lookup** table defines the top-level product categories used throughout the dashboard.  
It acts as a dimension table that enables grouping, filtering, and high-level category analysis for sales, orders, profit, and return metrics.

### 📌 Columns in the Product Categories Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| CategoryName | Text | The name of the product category (e.g., Bikes, Clothing, Accessories). |
| ProductCategoryKey | Whole Number | Primary key linking each category to related products in the Product Lookup table. |

### 📝 Notes
- This table contains **one row per product category**.  
- Used in slicers, visuals, and drill-down hierarchies.  
- Provides category-level grouping for metrics such as:
  - Category Sales  
  - Category Revenue  
  - Category Profit  
  - Category Return Rate  

### 🎯 Business Purpose
This dimension enables:
- High-level product grouping  
- Category performance comparison  
- Product segmentation in Executive and Product Performance dashboards  

## 🏷️ Product Lookup (Product Dimension)

The **Product Lookup** table contains detailed information about each product sold.  
It is a core dimension table used for category-level, subcategory-level, and SKU-level analysis across the dashboard.

This table supports critical metrics such as revenue, profit, return rate, and demand trends.

### 📌 Columns in the Product Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Discount Price | Decimal / Measure | The discounted selling price used in promotional analysis. |
| ModelName | Text | The product’s model or variant name. |
| Price Point | Decimal / Category | A price classification (e.g., Budget, Premium). |
| ProductColor | Text | The color of the product (when applicable). |
| ProductCost | Decimal | The cost to produce or procure the product. |
| ProductDescription | Text | Full descriptive text for the product. |
| ProductKey | Whole Number | Primary key that uniquely identifies each product. |
| ProductName | Text | The product’s name as shown in listings and reports. |
| ProductPrice | Decimal | Standard selling price before discounts or adjustments. |
| ProductSKU | Text | Stock Keeping Unit identifier used for inventory tracking. |
| ProductStyle | Text | Style or design classification (e.g., Mountain, Road for bikes). |
| ProductSubcategoryKey | Whole Number | Foreign key linking to product subcategories. |
| SKU Category | Text | Grouping of SKUs into broader performance categories. |
| SKU Type | Text | More granular classification of the SKU, often used for filtering. |

### 📝 Notes
- This table is central to the **Product Performance Dashboard**.  
- Measures such as *Bike Sales*, *Bike Return Rate*, or *Average Retail Price* rely on this table.  
- `ProductSubcategoryKey` links this table to deeper category hierarchies.  
- `ProductCost` and `ProductPrice` feed profitability calculations.

### 🎯 Business Purpose
The Product Lookup dimension enables:
- Category and subcategory performance analysis  
- SKU-level breakdowns for sales and returns  
- Profitability tracking by product  
- Price sensitivity and simulation modeling  
- Detailed segmentation for product managers and analysts  

## 📊 Product Metric Selection (Disconnected Table)

The **Product Metric Selection** table is a dynamic helper table used to enable **metric switching** on the Product Performance Dashboard.  
It allows users to choose which measure (Orders, Revenue, Profit, Returns, Rate) should appear in charts, cards, or visuals.

This table is manually constructed using DAX and is not connected to any other tables in the data model.

### 🧩 DAX Definition

- DAX
Product Metric Selection = {
    ("orders", NAMEOF('Measure Table'[Total Orders]), 0),
    ("Revenue", NAMEOF('Measure Table'[Total Revenue]), 1),
    ("Profit", NAMEOF('Measure Table'[Total Profit]), 2),
    ("Returns", NAMEOF('Measure Table'[Total Returns]), 3),
    ("Rate", NAMEOF('Measure Table'[Return Rate]), 4)
}

## 🧩 Product Subcategories Lookup

The **Product Subcategories Lookup** table stores the subcategory-level grouping of products.  
It forms the middle layer of the product hierarchy:

**Product Category → Product Subcategory → Product**

This dimension is used throughout the dashboard to analyze performance at a more granular level than category alone.

### 📌 Columns in the Product Subcategories Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| ProductCategoryKey | Whole Number | Foreign key linking each subcategory to its parent product category. |
| ProductSubcategoryKey | Whole Number | Primary key that uniquely identifies each subcategory. |
| SubcategoryName | Text | Name of the product subcategory (e.g., Mountain Bikes, Road Bikes, Tires, Jerseys). |

### 📝 Notes
- This table connects directly to the **Product Lookup** table via *ProductSubcategoryKey*.  
- It enables slicers, hierarchical drill-downs, category-based grouping, and subcategory performance reports.  
- It enriches analysis by allowing comparisons at the subcategory level instead of only broad categories.

### 🎯 Business Purpose
This dimension supports:
- Subcategory profitability analysis  
- Subcategory-level return rates  
- Trend analysis for product lines  
- Category hierarchy drill-downs (Category → Subcategory → SKU)  

## 🔄 Returns Data (Fact Returns Table)

The **Returns Data** table contains information about product returns, including the date of return, the product involved, the geographic territory, and the quantity returned.  
It is used for analyzing return trends, calculating return rates, and identifying quality or satisfaction issues across products and regions.

### 📌 Columns in the Returns Data Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| ProductKey | Whole Number | Foreign key linking the returned item to the Product Lookup table. |
| ReturnDate | Date | The date on which the returned product was recorded. |
| ReturnQuantity | Whole Number | Number of units returned for the specific product on the given date. |
| TerritoryKey | Whole Number | Foreign key identifying the geographic region where the return occurred. |

### 📝 Notes
- This table is used alongside sales fact data to compute **Return Rate**.  
- The `ProductKey` connects returns to product attributes such as category, subcategory, price, and cost.  
- The `TerritoryKey` enables regional return analysis (e.g., high-return regions).  
- `ReturnQuantity` is aggregated into measures such as:  
  - **Total Returns**  
  - **Return %, Return Rate**  
  - **Category-level or SKU-level return analysis**

### 🎯 Business Purpose
This table enables insights into:
- Product quality issues  
- Customer dissatisfaction indicators  
- Region-specific return patterns  
- High-return product categories  
- Return rate trends (weekly, monthly, yearly)  
- Comparison of sales vs. returns at product or category level  

Understanding returns is crucial for optimizing:
- Inventory planning  
- Product improvement  
- Customer satisfaction  
- Warranty management  
- Profitability analysis

## 📆 Rolling Calendar (Rolling Date Table)

The **Rolling Calendar** table is a specialized date dimension used for rolling-period calculations such as 10-day, 30-day, 90-day, and weekly moving averages.  
It includes dates along with period start boundaries, making it ideal for analyzing recent time trends and short-term performance metrics.

This table operates alongside the main Date table but is optimized for **rolling window measures**.

### 📌 Columns in the Rolling Calendar Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Date | Date | Individual calendar date; primary key of the table. |
| Year | Whole Number | Calendar year extracted from the date. |
| Start of Quarter | Date | First day of the quarter for the given date. Used for quarter-based rollups. |
| Start of Month | Date | First day of the month for the given date. Used for monthly grouping and rolling calculations. |

### 📝 Notes
- This table is typically used for **time intelligence** that requires precise rolling windows.  
- It enables the calculation of:
  - **10-day rolling revenue**  
  - **90-day rolling profit**  
  - **Rolling return rates**  
  - **Rolling average orders**  
- The `Start of Month` and `Start of Quarter` fields make it easy to group rolling windows into consistent periods.

### 🎯 Business Purpose
The Rolling Calendar table supports:
- Short-term trend analysis  
- Smoothing out seasonal fluctuations  
- Monitoring operational KPIs with rolling time windows  
- Enhanced forecasting and decision-making  
- Comparing current rolling windows to prior periods  

This table is critical for dashboards requiring continuous tracking of sales, profit, returns, and customer activity.

## 💵 Sales Data (Fact Table)

The **Sales Data** table is the central fact table of the model.  
It stores detailed transaction-level information for all retail sales and drives key metrics such as revenue, profit, order volume, and category performance.

Each row represents a single line item from a customer order.

### 📌 Columns in the Sales Data Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| CustomerKey | Whole Number | Foreign key linking the sales transaction to the Customer Lookup table. |
| OrderDate | Date | The date the transaction occurred. Used for trends, seasonality, and time intelligence. |
| OrderLineItem | Whole Number / Measure | Line item identifier within each order. |
| OrderNumber | Text / Whole Number | Unique identifier for the sales order. |
| OrderQuantity | Whole Number | Number of units purchased for the given product in the transaction. |
| ProductKey | Whole Number | Foreign key linking the sales transaction to the Product Lookup table. |
| Quantity Type | Text | Indicates quantity classification (e.g., Bulk, Retail). |
| Retail Price | Decimal | Selling price per unit before discounts or adjustments. |
| Revenue | Decimal | Total revenue from the transaction, typically calculated as (OrderQuantity × Retail Price). |
| StockDate | Date | Date the product was stocked or made available; sometimes used for inventory analysis. |
| TerritoryKey | Whole Number | Foreign key linking to the geographic or sales territory. |

### 📝 Notes
- This table links directly to multiple dimensions:
  - **Product Lookup**
  - **Customer Lookup**
  - **Territory / Geography Lookup**
  - **Date Table**
- It is the **primary source** for:
  - Total Revenue  
  - Total Orders  
  - Total Profit (via DAX using ProductCost)  
  - Return Rate (via relationship to Returns Data)  
  - Rolling revenue and rolling volume analytics  
- `Retail Price` combined with `ProductCost` supports margin and profitability calculations.

### 🎯 Business Purpose

The Sales Data fact table enables:

- Revenue trend analysis  
- Profitability analysis  
- Order volume tracking  
- Product-level and category-level insights  
- Customer order behavior analysis  
- Regional performance evaluation  
- Time-series and rolling-window KPI calculations  
- Comparison of sales vs returns  

This table is the foundation of all dashboards and KPIs within the project.

## 🌍 Territory Lookup (Geography Dimension)

The **Territory Lookup** table provides geographic attributes that categorize sales and returns by region.  
This table supports mapping visuals, regional performance comparison, and continent-level rollups.

It acts as a geography dimension linked to the Sales Data and Returns Data tables through `SalesTerritoryKey`.

### 📌 Columns in the Territory Lookup Table

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Continent | Text | The broader continent classification (e.g., North America, Europe, Pacific). |
| Country | Text | Country name associated with the sales territory. |
| Region | Text | Sub-regional grouping within the country (e.g., Northwest, Southeast). |
| SalesTerritoryKey | Whole Number | Primary key that links geographic information to sales and returns fact tables. |

### 🧭 Territory Hierarchy

The **Territory Hierarchy** provides a structured drill-down path for geographic reporting:

**Continent → Country → Region**

It allows users to explore sales performance and return metrics at multiple geographic levels.

### 📝 Notes
- This table is essential for the **Geographic Analysis Dashboard**.  
- Allows filtering and grouping by:
  - Region  
  - Country  
  - Continent  
- Provides accurate context for:
  - Revenue by region  
  - Profit by geography  
  - Regional return rates  
  - Territory-level order trends 

### 🎯 Business Purpose

The Territory Lookup dimension supports:
- Interactive map visuals  
- Regional performance comparisons  
- Territory drill-down analysis  
- Identifying high- and low-performing markets  
- Strategic planning by geography  
