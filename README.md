# Power BI Sales Performance Dashboard For Northwind Traders.

## Problem Statement

Northwind Traders, a renowned supplier of gourmet foods and beverages, seeks to optimize its sales performance through strategic analysis of its comprehensive sales dataset. This README delineates the challenges faced by Northwind Traders, insights derived from data analysis, recommendations for enhancing customer relationship management (CRM) and sales strategies, and acknowledgment of limitations in the analysis. 

### Questions
-Calculate Month-over-Month (MoM) and Year-over-Year (YoY) revenue growth percentages.

-Could you determine the difference in the number of customers ordering between last year and this year?

-Calculate the average Other Value between the order and the shipping date.

-Analyze the On-Time delivery  of orders.

### Steps followed 

- Step 1: Loaded Northwind trader's data into Power BI Desktop, the dataset is a CSV file.
- Step 2: Open the power query editor & in the view tab under the Data Preview section, and check the "column 
  distribution", "column quality" & "column profile" options. 
  The data was fairly clean but  I had to do further transformation and cleaning.
- Step 3: By default, the profile opened only for 1000 rows so I needed to select "column profiling based on entire 
   dataset".
- Step 4: It was observed that in none of the columns errors, however, I created my dimension and fact tables from the 
   large dataset.
- Step 5: The dimension table was divided into 6 i.e. Categories, Customers, employees, orders, products, and shippers 
   while the fact table is order_details.
- Step 6: A new table was created named Calender table to allow for time intelligence calculation using the Calender = 
  CALENDARAUTO() function.
  
-  Step 6b. The table was modeled using a star scheme like this
  <img width="196" alt="Screenshot 2024-05-13 232043" src="https://github.com/roshadah/Power-Bi-Project- 
   2/assets/98277448/4e48cd40-d4cf-475e-ad7d-9332e9cd11c4">

- Step 7: To aid my visualization and ability to gain insight from the data I calculated columns like (Sales = order_details[unitPrice]*order_details[Quantity]*(1- 
   order_details[discount]) and measures i.e (Revenue = SUM(order_details[Sales]),(Shipping Cost = SUM(orders[freight]), 
  Shipping Cost MoM% = 
   VAR CurrentShipAOV = [Shipping Cost]
   VAR PrevShipAOV = CALCULATE(
    [Shipping Cost],
   DATEADD(Calender[Date],-1,MONTH))

   RETURN
   DIVIDE(CurrentShipAOV - PrevShipAOV,PrevShipAOV,0).

- Step 8: Visual filters (Slicers) were added for two fields named "Year", and "Month".
- Step 9: Four card visuals Revenue, Average Other Value(AOV), Shipping Cost, On-Time Delivery.
           Using visual Slicer from the pane, basic filtering of April 2015 was used. 
           However, by default, while calculating the average, blank values are ignored.
- Step 10: A line chart of Revenues and Years was plotted to see the Trends across years. Low and High Point were 
  acknowledged using markers.
- Step 11: The Bar Chart was plotted using On Time Delivery% = DIVIDE(
    COUNTROWS(
        FILTER(orders,orders[shippedDate]<='orders'[requiredDate])),
        COUNTROWS('orders')) Vs Freight companies.
- Step 12: A table that includes ProductName, Revenue, and Quantity was plotted.
- Step 13: The top 3 performing products by Revenue were added to see the highest revenue-generating product.
- Step 14: A donut chart of the proportion of Revenue generated to Quantity Sold was added.


    for creating new measures following DAX expression was written;
   Revenue MoM% =  VAR CurrentMonthRev = [Revenue]
   VAR PreMonthRev = CALCULATE(
    [Revenue],
  DATEADD(Calender[Date],-1,MONTH))

  RETURN
  DIVIDE(CurrentMonthRev - PreMonthRev,PreMonthRev,0)


        
Snap of the new measure, calculated Revenue using the DAX Expression Revenue = SUM(order_details[Sales])

<img width="209" alt="Screenshot 2024-05-13 231921" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/145c8d02-d708-4996-95f9-b229d7a4acab">

        
- Step 15: A new measure was created to find the Average Other Value(AOV) 

The following DAX expression was written for the same,
        
        Average Other Value = DIVIDE([Revenue],COUNT(orders[orderID]))
        


<img width="196" alt="Screenshot 2024-05-13 232043" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/4e48cd40-d4cf-475e-ad7d-9332e9cd11c4">

        
 - Step 16: A new measure was created to find  On-time Delivery: 
 
 A card visual was used to represent shipping costs.
with : Shipping Cost = SUM(orders[freight])
 
<img width="212" alt="Screenshot 2024-05-13 232156" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/7c516fe6-baaf-4c72-acef-3fff793a63a5">

Following DAX expression was written to find % of on-time delivery,
 
        On-Time Delivery% = DIVIDE(
    COUNTROWS(
        FILTER(orders,orders[shippedDate]<='orders'[requiredDate])),
        COUNTROWS('orders'))
 A card visual was used to represent this percentage.
 
 <img width="198" alt="Screenshot 2024-05-13 232220" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/e5c4a628-a442-45b5-9cad-e176e6e27d4a">

 
 - Step 17: A new measure was created to calculate sales over time & a line graph was used to represent total distance.
 
 Following Revenue was plotted against categorical data of year and months to find trends,
 
         Snap of % of Delivery
    
 A bar chart visual was used to represent on-time delivery by the company.
 
 
<img width="426" alt="Screenshot 2024-05-13 232329" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/a1509b15-6eca-4be0-97d6-a65bdf9506c6">
 
 - Step 18: The report was then published to Power BI Service.
 
  - Step 17: A new measure was created for On-Time Delivery by the company.

<img width="431" alt="Screenshot 2024-05-13 232352" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/aa3bbfb5-c8c8-4fd5-bfd8-a622f8e4581d">

# Snapshot of Dashboard (Power BI Service)
<img width="430" alt="Screenshot 2024-05-14 005945" src="https://github.com/roshadah/Power-Bi-Project-2/assets/98277448/64d1ec2a-a478-4f6e-b268-b1416224cce5">  
## Insight

A single-page report was created on Power BI Desktop & it was then published to Power BI Service.

The following inferences can be drawn from the dashboard;

### Insights from the Northwind Traders dataset:

We identified top-selling products and customer segments for targeted marketing.
Optimize the effect of shipping cost in timely delivery.
Assesses delivery company to identify training needs and improve effectiveness.
Determine popular product categories to guide product offerings and marketing campaigns.

### Limitations
#### Data Quality: The analysis largely depends on the provided dataset's quality and accuracy.

##### Scope: The provided dataset may not encompass all relevant factors influencing sales performance.

##### Assumptions: Certain assumptions might have been made during the analysis, impacting the validity of conclusions.

### Conclusion
By leveraging insights from sales data and implementing strategic recommendations, Northwind Traders can enhance sales performance, improve customer relationships, and drive overall revenue growth. However, it's imperative to acknowledge the limitations inherent in the analysis and continuously refine strategies based on evolving market dynamics.

