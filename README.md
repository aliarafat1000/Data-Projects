# Coffee Sales Dashboard

## Introduction

In the competitive coffee industry, understanding sales patterns and customer preferences is crucial for maximizing profits and improving customer satisfaction. This project leverages Excel to analyze coffee sales data, offering insights into various sales metrics, including coffee types, sizes, sales trends, and customer behavior.


![Screenshot 2025-01-23 152055](https://github.com/user-attachments/assets/b1435692-0690-4ed6-9f8e-cf94c9eebe9a)


### Key Questions

This analysis aims to answer the following key questions:
1. **What are the sales trends over time?**
2. **Which coffee types and sizes are most popular?**
3. **How do sales vary by region?**
4. **Who are the top customers contributing to sales?**
5. **What impact do loyalty programs have on coffee sales?**
6. **How does roast type affect sales?**

![coffeeDashboard](https://github.com/user-attachments/assets/0cd8ef28-0c1a-4843-b120-d63373bcf7d7)



---

## Tools & Excel Features

This project makes use of various Excel tools and functions to provide insights:
- **📊 PivotTables**: To summarize data across multiple dimensions, such as coffee types, sizes, and regions.
- **📈 PivotCharts**: For visual representation of sales data.
- **🎛️ Slicers**: To filter data interactively by timeline, coffee size, and other categories.
- **🧮 Excel Functions**:
    - **XLOOKUP**: To retrieve customer information (e.g., loyalty card status, customer name, and country) and product details.
    - **INDEX & MATCH**: For quicker lookups to pull relevant product information based on order ID.
    - **Nested IFs**: To categorize coffee types (Arabica, Excelsa, Liberica, Robusta).

---

## Coffee Sales Dataset

The dataset used in this project contains key information on:
- **☕ Coffee Types**: Arabica, Excelsa, Liberica, Robusta.
- **🌱 Roast Types**: Dark, Medium, Light.
- **📦 Coffee Sizes**: Small, Medium, Large.
- **📍 Country**: The region or country of the sale.
- **💳 Loyalty Program**: Whether the sale was made using a loyalty card.
- **👤 Customer ID & Details**: Including customer names and country.
- **⏳ Date/Time**: Sales transaction timeline.

---

## Dashboard Features

### 1️⃣ **Sales Trends Over Time**
- Sales trends are analyzed over time using timeline slicers, providing insights into seasonality and growth patterns.
- Users can select time periods interactively to explore trends.

---

### 2️⃣ **Coffee Type & Size Analysis**
- PivotCharts summarize coffee sales by type (Arabica, Excelsa, Liberica, Robusta) and size (Small, Medium, Large).
- This analysis identifies the most popular coffee types and sizes, helping businesses optimize product offerings.

---

### 3️⃣ **Regional Sales Insights**
- Using country-level data, the dashboard provides insights into regional sales performance.
- A bar chart visualizes the top regions driving sales.

---

### 4️⃣ **Top Customers**
- The top 5 customers based on sales volume and revenue are highlighted.
- Insights into customer behavior, including loyalty program participation, are derived from this analysis.

---

### 5️⃣ **Loyalty Program Impact**
- Sales data is compared between loyalty program members and non-members.
- The dashboard helps identify the effect of loyalty programs on repeat purchases and average order value.

---

### 6️⃣ **Roast Type and Coffee Type Breakdown**
- The dashboard includes a breakdown of sales by roast type (Dark, Medium, Light) and coffee type (Arabica, Excelsa, Liberica, Robusta).
- Visualizations allow businesses to see which roast and coffee types are most in-demand.

---

## Excel Functions Used

### **Nested IF Formula**
- Used to categorize coffee types based on customer preferences or order details.
    ```
    =IF(I2="Rob","Robusta",IF(I2="Exc","Excelsa",IF(I2="Ara","Arabica",IF(I2="Lib","Liberica","No Data"))))
    ```

### **XLOOKUP**
- Retrieves customer details such as loyalty status, customer name, and country.
    ```
    =XLOOKUP([@[Customer ID]],customers!$A$2:$A$1001,customers!$I$2:$I$1001,,0)
    ```

### **INDEX & MATCH**
- Used for quicker lookups to fetch product details based on order ID.
    ```
    =INDEX(products!$A$2:$G$49,MATCH(orders!$D2,products!$A$2:$A$49,0),MATCH(orders!I$1,products!$A$1:$G$1,0))
    ```

---

## Insights

### 💡 Key Findings
1. **Seasonality**: Sales trends show increased demand during winter, with certain coffee types (e.g., Arabica) seeing seasonal spikes.
2. **Popular Products**: Light roast being the most popular roast type.
3. **Regional Insights**: Sales are strongest in America.
4. **Customer Loyalty**: Loyalty program members contribute a significant portion of revenue, demonstrating the effectiveness of rewards programs.
5. **Roast Preferences**: Light roast coffee dominates sales, but Medium and Light roasts are growing in popularity.

### 🤔 So What?
- These insights are useful for coffee shop owners and managers looking to optimize their product offerings, improve customer retention through loyalty programs, and plan targeted marketing campaigns based on seasonal trends.

---

## Conclusion

The coffee sales dashboard provides an in-depth look into key factors driving sales in the coffee industry. Using Excel’s powerful functions like XLOOKUP, INDEX, MATCH, and PivotTables, this project uncovers insights into coffee preferences, customer loyalty, and regional trends. This analysis helps businesses make data-driven decisions to increase sales, enhance customer satisfaction, and optimize inventory.
