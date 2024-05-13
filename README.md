# Optimizing Sales Performance at Northwind Traders.

## Problem Statement

Northwind Traders, a renowned supplier of gourmet foods and beverages, seeks to optimize its sales performance through strategic analysis of its comprehensive sales dataset. This README delineates the challenges faced by Northwind Traders, insights derived from data analysis, recommendations for enhancing customer relationship management (CRM) and sales strategies, and acknowledgment of limitations in the analysis. 

###Questions
Calculate Month-over-Month (MoM) and Year-over-Year (YoY) revenue growth percentages.
-Determine the difference in the number of customers ordering between last year and this year.
Calculate the average Other Value between the order and the shipping date.
Analyze the On-Time delivery  of orders.

### Steps followed 

- Step 1 : Loaded Northwind trader's data into Power BI Desktop, the dataset is a CSV file.
- Step 2 : Open the power query editor & in the view tab under the Data Preview section, and check the "column distribution", "column quality" & "column profile" options. 
           The data was fairly clean but  I had to do further transformation and cleaning.
- Step 3 : By default, the profile opened only for 1000 rows so I needed to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors, however, I created my dimension and fact tables from the large dataset.
- Step 5 : The dimension table was divided into 6 i.e. Categories, Customers, employees, orders, products, and shippers while the fact table is order_details.
- Step 6 : A new table was created named Calender table to allow for time intelligence calculation using the Calender = CALENDARAUTO() function.
- Step 7 : To aid my visualization and ability to gain insight from the data I calculated columns like (Sales = order_details[unitPrice]*order_details[Quantity]*(1-order_details[discount]) and measures i.e (Revenue = SUM(order_details[Sales]),(Shipping Cost = SUM(orders[freight]), Shipping Cost MoM% = 
VAR CurrentShipAOV = [Shipping Cost]
VAR PrevShipAOV = CALCULATE(
    [Shipping Cost],
DATEADD(Calender[Date],-1,MONTH))

 RETURN
DIVIDE(CurrentShipAOV - PrevShipAOV,PrevShipAOV,0).

- Step 8 : Visual filters (Slicers) were added for two fields named "Year", and "Month".
- Step 9 : Four card visuals Revenue, Average Other Value(AOV), Shipping Cost, On-Time Delivery.
           Using visual Slicer from the pane, basic filtering of April 2015 was used. 
           However, by default, while calculating the average, blank values are ignored.
- Step 10 : A line chart of Revenues and Years was plotted to see the Trends across years. Low and High Point were acknowledged using markers.
- Step 11 : The Bar Chart was plotted using On Time Delivery% = DIVIDE(
    COUNTROWS(
        FILTER(orders,orders[shippedDate]<='orders'[requiredDate])),
        COUNTROWS('orders')) Vs Freight companies.
- Step 12 : A table that includes ProductName, Revenue, and Quantity was plotted.
-Step 13  : The top 3 performing products by Revenue were added to see the highest revenue-generating product.
-Step 14  : A donut chart of the proportion of Revenue generated to Quantity Sold was added.

for creating new measures following DAX expression was written;
       
        Revenue MoM% = 
VAR CurrentMonthRev = [Revenue]
VAR PreMonthRev = CALCULATE(
    [Revenue],
DATEADD(Calender[Date],-1,MONTH))

 RETURN
DIVIDE(CurrentMonthRev - PreMonthRev,PreMonthRev,0)

        
Snap of the new calculated column, calculated Revenue using the DAX Expression Revenue = SUM(order_details[Sales])

<img width="209" alt="Screenshot 2024-05-13 231921" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/6071767b-c38f-4787-8c80-6b5fc5a3181b">

        
- Step 15 : A new measure was created to find the Average Other Value(AOV) 

The following DAX expression was written for the same,
        
        AOV = DIVIDE([Revenue],COUNT(orders[orderID]))
        


<img width="196" alt="Screenshot 2024-05-13 232043" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/b9bb82aa-459f-42fe-ad2e-396c2a429c64">

        
 - Step 16 : A new measure was created to find  On-time Delivery: 
 
 Following DAX expression was written to find % of on-time delivery,
 
        On-Time Delivery% = DIVIDE(
    COUNTROWS(
        FILTER(orders,orders[shippedDate]<='orders'[requiredDate])),
        COUNTROWS('orders'))
 A card visual was used to represent this percentage.
 
 
 A card visual was used to represent shipping costs.
with : Shipping Cost = SUM(orders[freight])
 
 <img width="212" alt="Screenshot 2024-05-13 232156" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/779cb4c2-7429-49fc-98b0-c4aa0bcb7bec">

 
 - Step 17 : A new measure was created to calculate sales over time & a line graph was used to represent total distance.
 
 Following Revenue was plotted against categorical data of year and months to find trends,
 
         Snap of % of Delivery
    
 A bar chart visual was used to represent on-time delivery by the companies.
 
 
<img width="198" alt="Screenshot 2024-05-13 232220" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/98ae9508-9344-43ba-86a9-7afeca957259">
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![Publish_Message]<img width="426" alt="Screenshot 2024-05-13 232329" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/9970528e-b00c-42e6-99d7-19a0f665e05c">

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo]<img width="431" alt="Screenshot 2024-05-13 232352" src="https://github.com/roshadah/We-rate-dogs-analysis/assets/98277448/67647289-6c85-4c4e-bc98-02de28ab5dc8">
  
## Insights

A single-page report was created on Power BI Desktop & it was then published to Power BI Service.

The following inferences can be drawn from the dashboard;

### Insights from the Northwind Traders dataset:

Identified top-selling products and customer segments for targeted marketing.
Optimize the effect of shipping cost in timely delivery.
Assesses delivery company to identify training needs and improve effectiveness.
Determine popular product categories to guide product offerings and marketing campaigns.

### Limitations
Data Quality: The analysis is largely dependent on the quality and accuracy of the provided dataset.
Scope: The provided dataset may not encompass all relevant factors influencing sales performance.
Assumptions: Certain assumptions might have been made during the analysis, impacting the validity of conclusions.
###Conclusion
By leveraging insights from sales data and implementing strategic recommendations, Northwind Traders can enhance sales performance, improve customer relationships, and drive overall revenue growth. However, it's imperative to acknowledge the limitations inherent in the analysis and continuously refine strategies based on evolving market dynamics.

