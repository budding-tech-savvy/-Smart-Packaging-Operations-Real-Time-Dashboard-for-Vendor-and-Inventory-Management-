# -Smart-Packaging-Operations-Real-Time-Dashboard-for-Vendor-and-Inventory-Management-
Optimized packaging material availability and vendor delivery management by automating data integration from MySQL Workbench into Power BI. Developed a real-time dashboard to monitor inventory and delivery schedules, replacing manual processes in Google Sheets and Excel, saving 15+ hours per week and improving operational accuracy by 25%, ensuring seamless vendor coordination and material availability.

![image](https://github.com/user-attachments/assets/d927d58a-f78d-4a2c-9373-02545828513d)                                   

```sql
#flow chart for basic understanding
Start
   ↓
[Data Import Through MySQL Query]
   ↓
[Load Data into Power BI]
   ↓
[Create Visualizations in Power BI]
   ↓
[Publish Report]
   ↓
End
```
# Let's understand this project step by step
# Step 1: Create a MySQL Query to Fetch Required Data

**Write a MySQL query to fetch the required data that will be used for visualization. Ensure that your query returns accurate and clean data.**

```sql
#Fetched these columns by writing this query.
SELECT 
    store_code AS "Store Code",
    store_name AS "Store Name",
    region AS "Region",
    code AS "Code",
    cc AS "CC",
    target_average AS "Target/Average",
    category AS "Category",
    material_description AS "Material Description",
    per_unit_cost AS "Per Unit COST",
    uom AS "UOM",
    closing_stock_physical AS "Closing Stock Physical as on current_date",
    average_per_day AS "Average Per Day (Last 30 Days)",
FROM 
    packaging_material_data
WHERE 
    date = '2024-11-04';
```

```sql
#fetched this data from another table to identify the material to be dispatched.
SELECT 
    cc AS "CC",
    pending_qty_from_vendor AS "Pending Qty From Vendor Side",
    minimum_order_qty AS "Minimum Order Qty"
FROM 
    vendor_orders;
```
```sql

# Merged both datasets to compile this into one table
SELECT  
    p.store_code AS "Store Code",
    p.store_name AS "Store Name",
    p.region AS "Region",
    p.code AS "Code",
    p.cc AS "CC",
    p.target_average AS "Target/Average",
    p.category AS "Category",
    p.material_description AS "Material Description",
    p.per_unit_cost AS "Per Unit COST",
    p.uom AS "UOM",
    p.closing_stock_physical AS "Closing Stock Physical as on 4 Nov'24",
    p.average_per_day AS "Average Per Day (Last 30 Days)",
    p.current_doi AS "Current DOI",
    v.pending_qty_from_vendor AS "Pending Qty From Vendor Side",
    v.minimum_order_qty AS "Minimum Order Qty"
FROM 
    packaging_material_data p
LEFT JOIN 
    vendor_orders v
ON 
    p.cc = v.cc
WHERE 
    p.date = '2024-11-04';

```

# Step 2: Connect Power BI to MySQL Database

**To connect Power BI to MySQL Workbench, follow these steps:**
Install MySQL ODBC Driver: Make sure you have the MySQL ODBC connector installed on your computer. You can download it from the official MySQL website.<br>
Connect Power BI to MySQL:<br>
Open Power BI Desktop.<br>
Click on Home > Get Data.<br>
Select MySQL Database.<br>
Enter the server name and database credentials (e.g., host, port, user, password).<br>
Click OK and select the database you want to work with.<br>

# Step 3: Load Data into Power BI
After connecting to MySQL, Power BI will show the list of tables and views available in your MySQL database.<br>
Select the appropriate table(s) or click on Advanced Options to paste your custom SQL query to fetch specific data.<br>
Click Load to import the data into Power BI.<br>

# Step 4: Transform Data (if necessary)
Once the data is loaded, you may need to perform some transformations to clean or reshape the data.

**Click on Transform Data to enter the Power Query Editor.**

**Here, you can:**
Rename columns for clarity.<br>
Filter out unnecessary data.<br>
Change data types.<br>
Combine multiple columns if needed (e.g., concatenate store code and name).<br>
Create new columns or measures, such as Total Pending Qty or Days of Inventory.<br>
Example of creating a new column for "Days of Inventory":<br>

**Formula: Days of Inventory = Closing Stock / Average Per Day**

# Step 5: Create Relationships (if needed)
If your data is coming from multiple tables (e.g., packaging materials and vendor orders), make sure the relationships between tables are correctly set:

**Click on Model to visualize relationships.**
Ensure that fields like store_code or cc are correctly linked between tables.
If relationships are not automatically created, manually create relationships by dragging the relevant fields from one table to another.

# Step 6: Design Power BI Reports and Visuals
Start building your reports using Power BI’s visualizations:

**Add Visualizations:**

Drag and drop fields to create different types of charts: bar charts, line graphs, pie charts, and tables.<br>
**For example, you can create a bar chart to visualize Pending Qty from Vendor by store, or a line chart for Current DOI over time.** <br>
Use card visuals to display key performance indicators (KPIs) like Total Pending Qty<br>
**Use Filters and Slicers:**
Add Slicers to filter by categories like Region, Store, or Material.<br>
For example, use a slicer to show only materials in the "Fnv" category or filter by the Region (e.g., North, South).
**Create KPIs:**

Set up conditional formatting to highlight critical metrics (e.g., if Pending Qty is greater than a threshold, color it red).

# Step 7: Set Up Real-time Dashboards (Optional)
If your data is being updated frequently, set up scheduled refresh to keep your Power BI dashboard up-to-date with the latest data from MySQL:<br>

In Power BI Desktop, click File > Options and settings > Data source settings.<br>
Choose the data source and set up scheduled refresh by connecting your Power BI Desktop to the Power BI Service.<br>
Once published to the Power BI Service, you can configure refresh intervals (e.g., daily, hourly).<br>

# Step 8: Publish to Power BI Service
Once your dashboard is ready, click Publish in Power BI Desktop.<br>
Sign in to your Power BI account and publish the report to your workspace.<br>
From the Power BI Service, you can share your report with stakeholders or create real-time dashboards.<br>

# Step 9: Share and Collaborate

Sharing: Share your Power BI reports and dashboards with stakeholders, making sure they have the right permissions.
Collaboration: Use Power BI workspaces for team collaboration to track material availability
# Key Benefits You Achieve with This Integration:

**Time Savings:** The real-time dashboard automates inventory and delivery management, saving 15+ hours per week compared to manual processes in Google Sheets/Excel.<br>
**Improved Accuracy:** The system provides accurate, up-to-date data, improving operational accuracy by 25%.<br>
Seamless Vendor Coordination: The dashboard ensures smooth vendor coordination by keeping track of pending orders and material availability, which leads to better planning and fewer delays.<br>
# Conclusion:
This integration between MySQL and Power BI allows you to automate the flow of data, optimize your inventory and vendor management processes, and create meaningful visual reports that help in decision-making. It replaces manual tracking systems and saves time, all while improving operational efficiency.
