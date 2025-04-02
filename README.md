# Power-BI-Sales-Profitability-Analysis
### Process Explanation, Dashboard Screen shots, & Analysis

This project demonstrates my expertise in Power BI and Power Query through a comprehensive dashboard report. It includes a detailed process explanation, dashboard screenshots, and a report analysis, highlighting my ability to transform data into actionable insights. The report showcases data visualization, interactive reporting, and analytical capabilities, making it a valuable asset for business decision-making. 
Part 1 contains detailed technical summary to prepare a data model & custom metrics for visualization. Report 1 & Report 2 are prepared with the help of the data model. Detailed report analysis is given along with it. 

The dashboard summaries are attached in the files: report 1 & report 2

Technical summary explained below:
		
## Dataset Overview
In order to create reports for Universal Export for two purposes:
1.	An annual report of operational status report to the stakeholders of the company
2.	A sales performance report to the management 
The report uses five different sources of datasets. These are:
1.	Transactions table (CSV format): A transactional data of all garment orders received by Universal Export in the last year (2023). It contains 110187 rows.
2.	Customers (XLSX format): A master table of all customer information such as name, address, category, new customer or not. It has a total of 48 customers information for the year 2023
3.	Products (CSV format): A master table containing product related information like name, category, color, etc with a unique id attached to each product for differentiation. There are 109 unique SKUs in 2023
4.	Logistics (TXT format): Information of all the shipment companies used to deliver orders. Each company is linked with a unique id. There were total of 20 shipment companies employed in 2023 to carry logistic operations
5.	Salespeople (JSON format): A master data file of all sales team information. There are 18 salespeople in the team for the year 2023

## Data Extraction
Power BI is solely used for the purpose of the project. Each data file was loaded in Power BI environment. The following is the information of the dataset created:

![image](https://github.com/user-attachments/assets/9932b1e1-e77a-4d61-afb7-08a38fdee4bb)

## Data Transformation
### Handling null values
Examining dataset further, products.csv file has empty values in the following columns:
•	Price_per_unit
•	Product Cost
•	Product Color
Since, null values contain less than 5% of the data rows, these empty value rows are ignored for the creating concise and clean visualisations.

### Removing unnecessary columns
Many columns in data tables are not useful for the purpose of the project and hence are ignored. These columns are:
1.	Logistics.txt: email & contact number
2.	customers.csv: Customer name, customer address, contact email

### Data typea
After a detailed examination of columns in dataset, having correct data type to each column is necessary. ‘sales_id’ in salespeople.json and customers.xlsx were converted to text data type from numeric for analysis purposes.

### Adding New Measures
In order to move ahead for analysis, new measures in the data are needed to calculate important KPIs for the reports. The new metrics derived were
```
profit = SUM('transactions'[product_price]) - SUM('transactions'[product_cost])
```
```
profit_percentage = DIVIDE(SUM('transactions'[product_price])- SUM('transactions'[product_cost]),SUM('transactions'[product_price]),0)
```
```
profit_month-on-month = IF(ISFILTERED('Transactions'[TRANSACTION_DATE]),
    ERROR("Time intelligence quick measures can only be grouped or filtered by the Power BI-provided date hierarchy or primary date column."),
     VAR __PREV_MONTH = CALCULATE(
         SUM('Transactions'[PROFIT]),
           DATEADD('Transactions'[TRANSACTION_DATE].[Date], -1, MONTH))
RETURN 
DIVIDE(SUM('Transactions'[PROFIT]) - __PREV_MONTH,__PREV_MONTH))

```
```
product_profit_margin = sum(Products[PRICE_PER_UNIT]) - sum(Products[COST])
```
```
new_customer_count = Conditional column based on if newin2023 = TRUE then 1, else 0
```

## Data Management
### Data modelling
To create a data model, each dataset primary key can be linked to another table’s  key to create relationships between tables. There are 5 tables used in the analysis. The model relationship is given below:

![image](https://github.com/user-attachments/assets/403c6cd4-06d4-4d88-8c23-ba06e841b3df)

Each key has a ‘many-to-one’ relationship with respective datasets.
You may refer to attached power bi file to track changes.



