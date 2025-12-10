
# 📊 DAX Measures – Calculation Logic

This file contains the primary DAX calculations used to power KPIs, trends, and business logic in the Enterprise Retail Intelligence Dashboard.

### Order Measures

- % of All Orders = 
DIVIDE(
    [Total Orders], 
    [All Orders])

- All Orders = 
CALCULATE(
    [Total Orders], 
    ALL(
        'Sales Data'
    )
)

- Bulk Orders = 
CALCULATE(
    [Total Orders],
    'Sales Data'[OrderQuantity] > 1
)

- High Ticket Orders = 
CALCULATE(
    [Total Orders],
    FILTER(
        'Product Lookup',
        'Product Lookup'[ProductPrice] > [Overall Average Price]
    )
)

- Previous Month Orders = 
CALCULATE(
    [Total Orders],
    DATEADD(
        'Calendar Lookup'[Date],
        -1,
        MONTH
    )
)

- Total Orders = 
DISTINCTCOUNT(
    'Sales Data'[OrderNumber]
)

- Weekend Orders = 
CALCULATE(
    [Total Orders],
    'Calendar Lookup'[Weekend] = "Weekend"
)

### Revenue Measures

- 10-day Rolling Revenue = 
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(
        'Calendar Lookup'[Date],
        MAX(
            'Calendar Lookup'[Date]
        ),
        -10,
        DAY
    )

- Adjust Revenue = SUMX('Sales Data','Sales Data'[OrderQuantity]*[Adjusted Price])

- Previous Month Revenue = 
CALCULATE(
    [Total Revenue],
    DATEADD(
        'Calendar Lookup'[Date],
        -1,
        MONTH
    ))

- Revenue per Customer = 
DIVIDE(
    [Total Revenue], 
    [Total Customers])

- Total Revenue = 
SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity]
    *
    RELATED(
        'Product Lookup'[ProductPrice]
    ))

- YTD Revenue = 
CALCULATE(
    [Total Revenue],
    DATESYTD(
        'Calendar Lookup'[Date]
    ))

### Profit Measures

- 90-day Rolling Profit = 
CALCULATE(
    [Total Profit],
    DATESINPERIOD(
        'Calendar Lookup'[Date],
        LASTDATE(
            'Calendar Lookup'[Date]
        ),
        -90,
        DAY
    ))

- Adjusted Profit = [Adjust Revenue]-[Total Cost]
 
- Previous Month Profit = 
CALCULATE(
    [Total Profit],
    DATEADD(
        'Calendar Lookup'[Date],
        -1,
        MONTH
    ))

- Total Profit = 
[Total Revenue] - [Total Cost]

### Price Measures

- Adjusted Price = [Average Retail Price]*(1+'Price Adjustment Percentage'[Price Adjustment Percentage Value])
  
- Average Retail Price = 
AVERAGE(
    'Product Lookup'[ProductPrice])

- Overall Average Price = 
CALCULATE(
    [Average Retail Price],
    ALL(
        'Product Lookup'
    ))

### Returns Measures

- % of All Returns = 
DIVIDE(
    [Total Returns],
    [All Returns])

- All Returns = 
CALCULATE(
    [Total Returns],
    ALL(
        'Returns Data'
    ))

- Bike Returns = 
CALCULATE(
    [Quantity Returned],
    'Product Categories Lookup'[CategoryName] = "Bikes")

- Bike Return Rate = 
CALCULATE(
    [Return Rate],
    'Product Categories Lookup'[CategoryName] = "Bikes")

- Previous Month Returns = 
CALCULATE(
    [Total Returns],
    DATEADD(
        'Calendar Lookup'[Date],
        -1,
        MONTH
    ))

- Quantity Returned = 
SUM(
    'Returns Data'[ReturnQuantity])

- Return Rate = 
DIVIDE(
    [Quantity Returned],
    [Quantity Sold],
    "No Sales")

- Total Returns = 
COUNT(
    'Returns Data'[ReturnQuantity])

### Target Measures

- Order Target = 
[Previous Month Orders] * 1.1

- Profit Target = 
[Previous Month Profit] * 1.1

- Revenue Target = 
[Previous Month Revenue] * 1.1

### Bike Sales Measure

- Bike Sales = 
CALCULATE(
    [Quantity Sold],
    'Product Categories Lookup'[CategoryName] = "Bikes")

### Quantity Sold Measure

- Quantity Sold = 
SUM(
    'Sales Data'[OrderQuantity])

### Total Cost Measure

- Total Cost = 
SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity]
    *
    RELATED(
        'Product Lookup'[ProductCost]
    ))

### Total Customers Measure

- Total Customers = 
DISTINCTCOUNT(
    'Sales Data'[CustomerKey]
)
