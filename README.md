# Maven-Market-Analytics 



![2024-06-27](https://github.com/vishalvinod175/Maven-Market-Analytics-DAX/assets/164670302/3cff44ee-17d5-4607-9229-aa1698b8c0ce)   




1. Load all the Data. Open the PowerQuery Editor to change the name of the tables and columns, according to your ease. Make sure the data is accurate with the correct Datatypes.
2. Add a new folder on your desktop (or in your documents) named "MavenMarket Transactions", containing both the MavenMarket_Transactions_1997 and MavenMarket_Transactions_1998 csv files.
3. Rename the tables for your ease of work. Check that the headers have been promoted.


**Power Query Editor**



5. In the 'Customers' table, add a new column 'full_name' merging the 'first_name' and 'last_name' column.
6. In the 'Customers' table, add a new column 'birth_year' extracting the year from the 'birth_date' column.
7. In the 'Customers' table, add a conditional column named 'has_children' which equals 'N' if the column 'total_children'=0, else 'Y'.
8. In the 'Products' table, add a calculated column 'discount_price' equalling 90% of the original retail price. Round it upto 2 decimal places.
9. In the 'Products' table, replace 'null' values in the 'recyclable' and 'low fat' columns.
10. In the 'Stores' table, add a new column 'full_address' merging the 'store_city', 'store_state and 'store_country' column, seperated by commas.
11. In the 'Stores' table, add a new column called 'area_code' extracting the characters before the '-' in the 'area_phone' column.
12. In the 'Calendar' table, add new date columns in the Power Query Editor, such as 'Start of Week' (starting Sunday), 'Name of Day', 'Start of Month', 'Name of Month', 'Quarter of Year', 'Year'.


 
**Data Modelling**


12. Open the model view, arrange the lookup tables below the data tables.
13. Connect 'Transaction' table to 'Customers', 'Products', 'Stores' tables with appropriate primary/foreign keys.
14. Connect 'Transaction' to 'Calendar' using both date fields, with an inactive "stock_date" relationship.
15. Connect 'Returns' to 'Products', 'Calendar', and 'Stores' using appropriate primary/foreign keys.
16. Connect 'Stores' to 'Regions' as a "snowflake" schema.
17. Hide all foreign keys in both data tables from Report View, as well as 'region_id' from the 'Stores' table.
18. Update all date fields (across all tables) to the "M/d/yyyy" format using the formatting tools in the Modeling tab.
19. Update 'product_retail_price', 'product_cost', and 'discount_price' to **Currency ($ English)** format.
20. In the 'Customers' table, categorize 'customer_city' as **City**, "customer_postal_code" as **Postal Code**, and "customer_country" as **Country/Region**.
21. In the 'Stores' table, categorize "store_city" as **City**, 'store_state' as **State or Province**, 'store_country' as **Country/Region**, and 'full_address' as **Address**.



**DAX EXPRESSIONS**   



22. In the 'Calendar' table, add a column named 'Weekend' where 'Y' equal Saturday/Sunday or 'N'.   
    `IF ('Calendar'[Day Name] = "Saturday" || 'Calendar'[Day Name] = "Sunday", "Y", "N")`
23. In the 'Calendar' table, add a column named 'End of Month' returning the last date of the month.   
     `EOMONTH('Calendar'[date],0)`
24. In the 'Customers' table, add a column named 'Current Age' calculating the age using the birthdate.   
    `DATEDIFF(Customers[birthdate].[Date], TODAY(),YEAR)`
25. In the 'Customers' table, add a column named 'Priority' which equals high for customers owning homes and gold membership cards.
    `IF(Customers[homeowner] = "Y" && Customers[member_card] = "Golden","High","Low")`
26. In the 'Customers' table, add a column named 'Short_Country' returning the first 3 letters of the country name, all capitallized.
    `UPPER(LEFT(Customers[customer_country],3))`
27. In the 'Customers' table, add a column named 'House Number' extracting characters before the first space in the 'customer_address' column.   
    `LEFT(Customers[customer_address], SEARCH(" ",Customers[customer_address])-1)`
28. In the 'Products' table, add a column named 'price_tier' equals 'high' if 'retail_price'>$3, 'mid' if >$1 and 'low' otherwise.
    `IF(Products[product_retail_price]>3,"High",IF(Products[product_retail_price]>1,"Mid","Low"))`
29.  In the 'Stores' table, add a column named 'Years_Since_Remodel' giving the years between today and the last year of remodelling.
    `DATEDIFF(Stores[last_remodel_date],TODAY(),YEAR)`   
    **Add a new measures, accordingly to whichever table**
30. 'Quantity Sold' = `SUM(Transaction_data[quantity])`
31. 'Quantity Returned' = `SUM(Return_data[quantity])`
32. 'Total Transactions' = `COUNTROWS(Transaction_data)`
33. 'Total Returns' = `COUNTROWS(Return_data)`
34. 'Return Rate' = `DIVIDE([Quantity Returned],[Quantity Sold])` **Format to Percentage*
35. 'Weekend Transactions' = `CALCULATE([Total Transactions], 'Calendar'[Weekend]="Y")`
36. 'All Transactions' = `CALCULATE([Total Transactions],ALL(Transaction_data))`
37. 'All Returns' = `CALCULATE([Total Returns], ALL(Return_Data))`
38. 'Total Revenue' = `SUMX(Transaction_Data, Transaction_Data[quantity] * related(Products[product_retail_price]))`
39. 'Total Cost' = `SUMX(Transaction_data, Transaction_data[quantity] * RELATED(Products[product_cost]))`
40. 'Total Profit' = `[Total Revenue] - [Total Cost]`
41. 'Profit Margin' = `DIVIDE([Total Profit],[Total Revenue])`  **Format to Percentage*
42. 'Unique Products' = `DISTINCTCOUNT(Products[product_name])`
43. 'YTD Revenue' = `CALCULATE([Total Revenue],DATESYTD('Calendar'[date]))`
44. '60-Day Revenue' = `CALCULATE([Total Revenue], DATESINPERIOD('Calendar'[date], MAX('Calendar'[date]),-60,DAY))`
45. 'Last Month Transactions' = `CALCULATE([Total Transactions], DATEADD('Calendar'[date], -1, MONTH))`
46. 'Last Month Revenue' = `CALCULATE([Total Revenue], dateadd('Calendar'[date], -1 , MONTH))`
47. 'Last Month Profit' = `CALCULATE([Total Profit], DATEADD('Calendar'[date], -1, MONTH))`
48. 'Last Month Returns' = `CALCULATE([Total Returns], DATEADD('Calendar'[date], -1, MONTH))`
49. 'Revenue Target' = `[Last Month Revenue] * 1.05` based on 5% increase over 'Last Month Revenue'  **Format to $*
50. You can design the report in your own ways through the Measures above. Thank you.






