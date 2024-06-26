# Maven-Market-Analytics

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



