# Enterprise-Retail-Intelligence-Dashboard
A complete Power BI analytics solution delivering actionable insights across sales performance, profitability, customer behavior, product trends, and global market distribution.

## 📌 Overview
The **Enterprise Retail Intelligence Dashboard** is a multi-page, enterprise-level Business Intelligence solution built using **Power BI**.

This capstone project demonstrates advanced analytical and visualization skills through:

- Data cleaning & transformation  
- Star schema data modeling  
- DAX measure creation  
- KPI & trend analysis  
- Enterprise dashboard UI/UX  
- Storytelling with data  

The dashboard converts raw retail data into a centralized analytical system supporting strategic decisions in sales, marketing, customer segmentation, forecasting, and product performance analysis.

## 🛠 Tech Stack

| Component | Tool |
|----------|------|
| BI Tool | Power BI Desktop |
| ETL / Data Prep | Power Query (M Language) |
| Data Modeling | Star Schema, Fact & Dimension Tables |
| Calculations | DAX Measures |
| Dataset | AdventureWorks Retail Dataset |
| File Types | .pbit, .pdf |

## 📂 Data Sources
This dashboard uses cleaned and curated tables from the AdventureWorks dataset, including:

### Sales Data
- Order Date  
- Revenue  
- Profit  
- Quantity  
- Return Rate  

### Product Data
- Category  
- Subcategory  
- SKU  
- Cost & Price  

### Customer Data
- Name  
- Occupation  
- Income Level  
- Demographics  

### Geography
- Country  
- Region  
- Market Zones  

### Calendar Table
- Month  
- Year  
- Time intelligence support  

All datasets were combined into a clean BI model with relationships established following best practices.

# 📊 Dashboard Pages & Detailed Breakdown

## 1. Executive Summary Dashboard
(Main performance overview for business leaders)

### KPIs Displayed
- $24.9M Total Revenue  
- $10.5M Total Profit  
- 25.2K Total Orders  
- 2.2% Return Rate  

These metrics give instant clarity on retail performance.

### Trend Visualizations
- Weekly Revenue Line Chart  
- Monthly Revenue (MoM comparison)  
- Monthly Orders & Returns charts  

### Category Insights
Order distribution across:
- Accessories — 17K  
- Bikes — 13.9K  
- Clothing — 7K  

### Top 10 Product Table
Includes:
- Orders  
- Total Revenue  
- Return Rate  

This helps identify best sellers, high-revenue SKUs, and products requiring quality checks.

## 2. Geographic Sales Dashboard
(Full interactive world map dashboard)

### Regions Covered
- United States  
- Canada  
- Australia  
- United Kingdom  
- France  
- Germany  

### Regional Filters
- Select All  
- Europe  
- North America  
- Pacific  

### Business Insight
This dashboard helps businesses identify:
- High-performing markets  
- Underperforming regions  
- Growth opportunities  

Bubble sizes represent total revenue contribution by country.

## 3. Product Performance Dashboard
(Complete analysis for product profitability & demand)

### Monthly KPIs vs Targets
Gauge visuals show:
- Actual vs Target Orders  
- Actual vs Target Profit  
- Actual vs Target Revenue  

### Price Adjustment Simulator
A dynamic slider allows users to:
- Adjust product price percentage  
- View updated Adjusted Profit  
- See market impact immediately  

### Trend Charts
Tracking over time:
- Orders  
- Revenue  
- Profit  
- Returns  
- Return Rate  

## 4. Customer Insights Dashboard
(Full customer segmentation & behavior analysis)

### Customer-Level KPIs
- 17.4K Unique Customers  
- $1,431 Revenue per Customer  

### Weekly Customer Trend
Reveals retention, loyalty patterns, and seasonality.

### Top Customers by Revenue
Example:
- Mr. Maurice Shan — $12.4K Revenue  

### Segmentation
#### By Income Level
- Average Income — 11.6K  
- Low Income — 11.1K  
- High Income — 2K  

#### By Occupation
- Professional — 7.9K  
- Skilled Manual — 6K  
- Management — 4.4K  

### Customer Detail Table
Every customer displayed with:
- Total Orders  
- Total Revenue  
- Demographic attributes  

# ⭐ Key Features of This Project
- Multi-page enterprise dashboard  
- Clean UI/UX with intuitive navigation  
- KPI storytelling with actionable business insights  
- Price sensitivity & profitability simulation  
- Customer, product, and market analytics in one system  
- Professional data model using BI best practices  
- Advanced DAX time intelligence and dynamic measures
  
## 🚀 How to Use

Download the .pbit file

Open in Power BI Desktop

Load the data (AdventureWorks)

Refresh all visuals

Navigate across pages for insights

## 🎯 Business Impact

This dashboard empowers organizations to:

Identify revenue trends & seasonal patterns

Evaluate high-performing & underperforming products

Analyze customer behavior & segmentation

Track geographic sales performance

Optimize pricing decisions

Improve return management

Support data-driven decision making

## 🏁 Conclusion

The Enterprise Retail Intelligence Dashboard is a powerful demonstration of advanced analytics, BI visualization, data modeling, and business storytelling. It functions as an enterprise-ready solution capable of supporting strategic decision-making across product, sales, marketing, and customer management teams.

This project reflects strong skills in:

Data Analysis

Power BI Development

DAX / Power Query

Dashboard Design

Business Intelligence

## 🖼 Screenshots

## Executive Summary
![Executive Summary](https://github.com/Charan2812/Enterprise-Retail-Intelligence-Dashboard/blob/main/Screenshots%20Files/Executive_Summary.png)

## Geographic Sales
![Geographic Sales](https://github.com/Charan2812/Enterprise-Retail-Intelligence-Dashboard/blob/main/Screenshots%20Files/Geographic%20Sales.png)

## Product Anlaysis
![Product Analysis](https://github.com/Charan2812/Enterprise-Retail-Intelligence-Dashboard/blob/main/Screenshots%20Files/Product%20Analysis%20.png)

## Customer Insights
![Customer Insights](https://github.com/Charan2812/Enterprise-Retail-Intelligence-Dashboard/blob/main/Screenshots%20Files/Customer%20Insights.png)

## 📁 Recommended Repository Structure

```plaintext
Enterprise-Retail-Intelligence-Dashboard/
│
│── Dashboard Files/
│     ├── Enterprise_Retail_Intelligence_Dashboard.pbit
│     ├── Retail_Dashboard_Report.pdf
│
│── Screenshots/
│     ├── executive_summary.png
│     ├── geographic_analysis.png
│     ├── product_performance.png
│     ├── customer_insights.png
│
│── README.md
│── Data Dictionary/
│── DAX Measures/
│── Power Query Transformations/
