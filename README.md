☕ Coffee Shop Sales Analysis Dashboard

A Power BI dashboard designed to visualize and analyze sales performance for a coffee shop chain. This interactive analytics solution highlights key revenue metrics, product performance insights, store comparisons, and sales trends across days and hours — enabling data-driven decision-making for business growth.

📊 Overview

This dashboard helps stakeholders:

Identify top-performing products & categories

Monitor total sales, orders, and quantity sold

Analyze seasonal and hourly purchasing trends

Compare store performance month-over-month

Optimize pricing and product strategy

📁 Dataset Details
Column Name	Description
transaction_id	Unique identifier for each transaction
transaction_date	Date of the transaction
transaction_time	Time of the transaction
transaction_qty	Quantity of items sold
store_id	Unique identifier for the store
store_location	Store location (city/branch)
product_id	Unique product identifier
unit_price	Price per unit
product_category	Product category (coffee, tea, bakery, etc.)
product_type	Sub-category of the product
product_detail	Specific product details
🧮 DAX Measures Used

Key metrics and calculations:

-- Total Sales
Total Sales = SUM(Transactions[Sales])

-- Total Orders
Total Orders = DISTINCTCOUNT(Transactions[transaction_id])

-- Total Quantity Sold
Total Quantity Sold = SUM(Transactions[Transaction_Qty])

-- Average Daily Sales
Average Sales =
AVERAGEX(
    ALLSELECTED(Transactions[transaction_date]),
    'Date Table'[Total Sales]
)

-- Previous Month Sales
Previous Month Sales =
CALCULATE('Transactions'[CM], DATEADD('Date Table'[Date], -1, MONTH))

-- Previous Month Orders
Previous Month Orders =
CALCULATE('Transactions'[CM Orders], DATEADD('Date Table'[Date], -1, MONTH))

-- Previous Month Quantity Sold
Previous Month Quantity Sold =
CALCULATE('Transactions'[CM Qty], DATEADD('Date Table'[Date], -1, MONTH))

-- Current Month Sales (MTD)
Current Month Sales =
VAR selected_month = SELECTEDVALUE('Date Table'[Month])
RETURN
    TOTALMTD(
        CALCULATE(SUM(Transactions[Sales]), 'Date Table'[Month] = selected_month),
        'Date Table'[Date]
    )

📌 Dashboard Components
Visual	Insights Provided
KPIs	Total sales, orders, quantity, MoM change
Sales by Date Line Chart	Daily performance with average sales reference line
Weekday vs Weekend Donut Chart	Weekly behavior and peak days
Sales by Product Category	Compare major category contributions
Sales by Product Type	Identify best-selling product variants
Store Performance Comparison	Store-level MoM benchmarking
Day & Hour Heatmap	Peak selling hours & staffing optimization
