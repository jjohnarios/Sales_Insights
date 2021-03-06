# Sales Insights :chart_with_upwards_trend:
Sales Insights for an Unnamed Company in India.
Dashboard links: [Sales_Insights](https://public.tableau.com/views/SalesInsights_16181408686320/SalesDashboard?:language=en&:retry=yes&:display_count=y&:origin=viz_share_link)&emsp; & &emsp; [Profit Analysis](https://public.tableau.com/views/Profit_Analysis_16182248368330/ProfitAnalysisDashboard?:language=en&:retryBootstrapAttempts=1&:display_count=y&:origin=viz_share_link)

![MySQL](https://img.shields.io/badge/-MySQL-blue) ![Tableau](https://img.shields.io/badge/-Tableau-orange)

## Main Idea - Problem Statement
The company provides hardware to other firms and recently realized that their sales are decreasing. The manager asked the Data Analysis Team for Data Insights. Initially, they were looking to find:
- Revenue by cities
- Revenue by year
- Top 5 costumers by revenue
- Top 5 products by revenue

## Project Planning - Aims Grid
<p align="center">
  <img src="AimsGrid.png" width="600" title="Aims Grid">
</p>

## Dataset
**Version 1** -> Database (MySQL) with five tables: customers, date, markets, products, transactions 
`sales_db.sql`.<br>
Data Cleaning and preprocessing using Tableau:
- Removal of null values. For example, old companies that no longer take hardware from the Unnamed company.
- Removal of invalid values and filtering (e.g. >= 1 sales quantity etc.)
- Currency conversion ("USD" to "INR"). All prices need to be in Indian Rupee for proper insights.

**Version 2** -> Preprocessed database (MySQL) with three additional columns in the transactions table (profit,profit_margin,cost_price) 
`sales_db_v2.sql`.
## Sample SQL queries for Data Analysis

1. Show number of transactions performed in 2019 <br>
`SELECT COUNT(*) FROM sales.transactions WHERE YEAR(order_date)="2019";`
2. Show transcations for Bengaluru market (market_code='Mark006') <br>
`SELECT * FROM transactions where market_code='Mark006';`
3. Show total revenue in 2020 (INR) <br>
`SELECT SUM(sales.transactions.sales_amount) 
FROM sales.transactions 
WHERE YEAR(order_date)="2020";`
4. Show number of distinct customers that made a transaction <br>
`SELECT COUNT(DISTINCT sales.customers.customer_code) AS "Number Of Customers" 
FROM sales.customers
		INNER JOIN sales.transactions 
                ON sales.customers.customer_code=sales.transactions.customer_code;`
5. Show customers with more than 20 million total INR on our tansactions <br>
`SELECT customers.customer_code,customers.custmer_name,sum(sales_amount) AS Price FROM sales.transactions
INNER JOIN customers ON transactions.customer_code=customers.customer_code
group by customer_code HAVING Price >20000000;`

## Update - Version 2
The manager asked gave feedback and asked the Data Analysis Team for another dashboard with profit analysis. This dashboard (version_2) should contain:
- Profit Margin by Market
- Revenue by Customer Type
- Profit Margin, Revenue for each Customer
- Profit Trend

Acknowledgments to @codebasics for providing the dataset.
