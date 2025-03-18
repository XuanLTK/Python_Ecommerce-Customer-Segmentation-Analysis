# Project Title: [Python] E-commerce Customer Segmentation Analysis  
Author: [Xuan Luong]  

Date: 2024 

Tools Used: Python  

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
3. [⚒ Main Process](#-main-process) 
4. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview

### SuperStore Company Overview 🎉  

SuperStore is a global retail company 🌎, which means it has a large number of customers.   

On the occasion of Christmas and New Year 🎄🎆, the Marketing Department wants to run marketing campaigns to show appreciation to customers who have supported the company throughout the year. They also aim to tap into potential customers who could become loyal patrons.  

However, the Marketing Department has not yet segmented this year’s customers because the dataset is too large to process manually as in previous years. Therefore, they have requested the Data Analytics Department for support in implementing a customer segmentation classification problem to deploy tailored marketing programs for each customer group.  

The Marketing Director also proposed using the RFM model. However, in the past, when the company was smaller, the team could classify and calculate using Excel. Now, with a significant amount of data, they hope the Data Department will develop a process for evaluating segmentation using Python programming. 🐍  

### Objective:
  This project uses Python to analyze retail sale data from e-commerce to:
  
✔️ Segment customers by using the RFM model to enhance marketing strategies for E-commerce Retail Company

✔️ Suggest marketing ideas through precise segmentation of customers.

### 👤 Who is this project for?  

✔️ Marketing manager

✔️ R&D manager


---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.	

**Data filename:** ecommerce_retail.xlsx								
The Excel file contains 2 sheets

**Sheet 1: ecommerce_detail**
  
  Include 8 columns:
  - InvoiceNo: Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'C', it indicates a cancellation.									
  - StockCode: Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.									
  - Description: Product (item) name. Nominal.									
  - Quantity: The quantities of each product (item) per transaction. Numeric.									
  - InvoiceDate: Invoice Date and time. Numeric, the day and time when each transaction was generated.									
  - UnitPrice: Unit price. Numeric, Product price per unit in sterling.									
  - CustomerID: Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.
  - Country: Country name. Nominal, the name of the country where each customer resides.

**Sheet 2: Segmentation**

Include 2 columns, containing customer group classification information

---
## ⚒ Main Process

## **Part 1: Computational Thinking**

### I. Decomposition  

To enhance the effectiveness of the marketing strategy and drive customer engagement, we identify two critical issues that need to be addressed:  

### 1. Classifying Customer Segments Based on the RFM Model  

The RFM model (Recency, Frequency, Monetary) serves as a cornerstone for understanding customer behavior and enhancing retention strategies.   

- **Recency (R)**: This metric measures how recently a customer has made a purchase. Customers who have made a purchase recently are more likely to respond to marketing efforts. The goal is to identify customers who have not purchased in a while (high recency) and implement strategies to re-engage them.  
  
- **Frequency (F)**: This indicates how often a customer purchases within a defined period. A higher frequency suggests stronger customer loyalty and can guide marketing teams in targeting these customers with loyalty programs or exclusive offers.  
  
- **Monetary (M)**: This assesses how much money a customer has spent over time. Customers who contribute significantly to revenue should be prioritized for high-value promotions and appreciation campaigns.  

To achieve effective segmentation, we will analyze the customer data to derive R, F, and M scores for each customer. This classification will help us to group customers into segments such as “Champions,” “Loyal,” and “At Risk,” and identify which segments require immediate attention.  

### 2. Making Appropriate Marketing Program Recommendations Based on Each Customer File  

Once customer segments have been defined, the next step is to develop targeted marketing recommendations tailored to each segment. This includes:  

- **Specific Marketing Strategies**: Tailoring messages and offers to fit each segment’s characteristics (e.g., promotional offers for “At Risk” customers to encourage return visits).  
  
- **Personalization**: Utilizing customer data to create personalized marketing experiences can strengthen customer relationships and drive repeat business.  

- **Performance Metrics**: Establishing key performance indicators (KPIs) to measure the success of the marketing initiatives and adjust strategies accordingly. Metrics could include increased purchase frequency, higher average order values, and reduced churn rates.  

Through effective segmentation and tailored marketing strategies, we aim to boost customer engagement and loyalty, ultimately enhancing the overall profitability of the Superstore.   

### II. Pattern Recognition  

Currently, there is an Excel file containing 2 sheets:  

1. **Sheet “e-commerce retail”**:  
    - This sheet contains purchase information for each customer, showing the list of products in each order ⇒ there is no total revenue displayed for each customer.  
    - A customer can have one or more orders, and one order can have multiple products with different quantities and unit prices.  
    - There are missing values in the description and customerID columns ⇒ replace them with NaN.  
    - There are negative values.  

2. **Sheet “Segmentation”** contains scores for classifying customers:  
    - This sheet contains information that allows customer classification.  
    - There are no missing values and no duplicates.  

### III. Abstraction  

1. Load dataset.  
2. EDA → clean data.  
3. Classifying customer segments based on the RFM model:  
    - Calculate Recency, Frequency, and Monetary scores for each customer:  
        - **Recency**: Calculate the number of days from the last order occurrence to the present (as of 31/12/2011).  
        - **Frequency**: Calculate the total number of orders that each customer has made.  
        - **Monetary**: Calculate the total revenue generated by each customer.  
    - Allocate R, F, and M scores to each customer on a scale from 1 to 5.  
    - Create a combined R-F-M score.  
    - Merge with the “Segmentation” sheet to classify customers based on the combined RFM score.  
4. Based on each customer file, make recommendations for appropriate marketing programs:  
    - Create visualizations showing the distribution of customer segments according to the RFM metrics.  
    - For each segment mentioned above, evaluate the current situation of the company (quantity, location, preferred products) and how it is performing within that segment.  
    - Propose suitable marketing programs based on the current situation.  
    - Suggest to the Marketing and Sales team which of the three metrics R, F, or M should be prioritized in the Superstore's retail model.  

### IV. Algorithm Design  

- Create a DataFrame containing the following columns:  
    - For each score:  
        - **R**: R = now - last_transac_date ⇒ quantile value in the column quantile(0.2, 0.4, 0.6, 0.8, else) ← [5, 4, 3, 2, 1]  
        - **F**: F = count total “InvoiceNo” by each CustomerID (used groupby) ⇒ quantile value in the column quantile(0.2, 0.4, 0.6, 0.8, else) ← [1, 2, 3, 4, 5]  
        - **M**: M = total “revenue” (Revenue = Quantity * UnitPrice) by each CustomerID ⇒ quantile value in the column quantile(0.2, 0.4, 0.6, 0.8, else) ← [1, 2, 3, 4, 5]  
    - Combine RFM scores ⇒ concat “R” + “F” + “M”.  
    - Merge customer segments (after merging with Segmentation).  

- Create visualizations comparing the segments:  
    - Number of customers.  
    - Number of orders.  
    - Number of purchases.  
    - Total revenue.  
    - Locations.  
    - Best-selling products in each segment.

## **Part 2: Create Python script**
[Analysis Results]([Python]_Retail_Industry_Customer_Segmentation_project.ipynb)

---


## 🔎 Final Conclusion & Recommendations

### **1. Recency, Frequency, and Monetary Value of Superstore:**  

- As a retailer, Superstore may prioritize Recency and Frequency over their Monetary since their most loyal shoppers may make many purchases throughout the year at lower Average Transaction Sizes. However, Superstore's Recency and Frequency do not have many positive signs.  
- The mean of Frequency is **6 times**, which is low for a retail company. This means customer loyalty is not high.  
- The mean of Recency is approximately **166 days**, while the median is **83 days**. This represents a lot of high Recency values. The larger this index, the higher the customer's tendency to leave.  

  => Those are some warnings for Superstore to focus more on Recency and Frequency performance.  

### **2. Segments of Superstore:**  

- The two segments with the highest proportion of customers are **Potential Loyalist (14.29%)** and **At Risk (12.14%)**.  
- Negative segments such as **Hibernating** and **Lost** accounted for a high proportion of customers, **11.38%** and **10.49%**, respectively. However, these two groups account for less than **8%** of revenue.  
- The two most positive segments account for less than **17%** of the proportion of customers (**Champions, 8.98%**, and **Loyal, 7.84%**).  
- Potential Loyalist (the ideal segment) has the highest proportion of customers (*14.29%*), but its revenue proportion is only *9.02%*. Meanwhile, the negative segment, At Risk, accounts for *18.24%* of revenue.  

  ⇒ In this Christmas - New Year marketing campaign, Superstore needs to prioritize its efforts to promote the Potential Loyalist group to become Loyal and Champions members and then find ways to reconnect with customers in the At Risk group.  

### Recommendations

For the retail model of Superstore, there are several suggestions as follows:

- The Marketing Team should focus on the Recency metric and implement campaigns to attract customer interest and brand awareness. Besides the top champions group, marketing should pay attention to launching campaigns targeted at the Hibernating and Lost customer groups. These two customer groups represent the second and third largest proportions of the total customer segments and have a high risk of being lost, which could lead to significant customer loss.

- The Sales Team should prioritize both the Frequency and Monetary metrics. It is important to maintain contact with Loyal customers to quickly introduce them to the latest products, creating potential revenue growth for the company. Additionally, they should also reach out and build relationships with new customers, the At-risk group, and the Potential Loyalist group. These customer groups have an average proportion and a lot of potential to become loyal and committed customers of the company.

