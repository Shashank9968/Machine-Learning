
# ML Optimization for Inventory Management

## Overview

* Inventory Optimization: Analyzed and optimized Bibitor, LLC’s inventory processes, reducing excess stock and improving efficiency across multiple locations.

* Reorder Prediction: Developed an ML model to predict optimal reorder quantities, minimizing stockouts and boosting inventory turnover.

* Business Insights: Extracted key insights from sales and purchase data, providing strategic recommendations to enhance profitability and decision-making.

please [click here ](https://www.kaggle.com/code/abdulmelikhmeda/inventory-purchase-sales-analysis-and-optimization/notebook#2.1-Analysis-of-main-inventory-management-parameters) for  more details on the dataset

## Motivation

* My long-standing interest in retail inventory management drove me to explore innovative solutions, leading to the development of advanced ML models aimed at optimizing inventory control.

 * Recognizing the impact of  deadstock on retail operations, i figured machine learning models could help alleviate this shortcoming.

 ## Methodology
 ### 1. Data Cleaning
 From the dataset, it is observed there are areas where some data is missing, inconsistent, incorrect etc. The key points are provided down below.

 Missing Values:
* City Column in Ending Inventory: 1,284 missing values out of 224,489 entries. The missing city name will be assigned based on store location data.
* Size Column in Purchase Table: Few missing values out of 2,372,474 entries. The plan is to fill these with subsequent non-missing values.
* Approval Column in Purchase Invoice Table: Majority of the data in this column is missing.
* Description, Size, and Volume Columns in Purchase Price Table:  In these columns most of the data is there however there ar some areas in which they are missing  and the size columns appears to have inconsistent sizing.

To solve the above problems the following techniques were used :-

Handling Missing Values:-
* In the purchase dataset, the size column had a few missing values, these were filled using the ffill method()
* In the ending inventory data the city column was missing some data. After thorough analysi it was found the misssing city name was ""TYWARDREATH" which is tied to store 46.
* Since the approval column had majority of the data missing, it was excluded from the analysis.

Handling Varying Units of Measurement :-
In the data, it was found that the size column had various units of measurements . For a better analysis all the units were standardized to litres.

### 2. Inventory Analysis 
### a. Lead Time
This refers to the duration between when a warehouse places an order with a supplier and when the goods are received. It's a significant measure for improving inventory management and supply chain processes.
 ### Lead Time = Recieving Date - PO Date

 ![download (16)](https://github.com/user-attachments/assets/c23ea873-a090-4474-ad07-16ddac9f8ed7)

From the histogram it is preety evident that, the avg lead time is about 7 days. there are some days where delivery is much faster takes about 2-3 days , there are also some days where the lead time is > 12 days.

 ### b. Safety stock and Onhand Inventory
   Safety Stock - It is the additional quantity of inventory kept on hand to prevent stockouts caused by uncertainties in demand or supply. It acts as a buffer to ensure that customer orders can be fulfilled even if unexpected changes occur in the supply chain, such as delays or sudden spikes in demand. 

On-Hand Inventory: On-hand inventory refers to the actual quantity of inventory currently available in stock. It represents the goods that are physically present in the warehouse or store and are available for sale or use
 ### Optimal Safety Stock=(Maximum Lead Time−Average Lead Time)×Average Daily Sales of the Product
### Maximum Safety Stock=(Maximum Daily Sales×Maximum Lead Time) -(Average Daily Sales×Average Lead Time)¶

![image](https://github.com/user-attachments/assets/6777e43c-5462-4e6f-b6ef-9d774143c2f0)

The above image displays the required Safety Stock levels of a few products.

 ### c. Reorder Point
 The reorder point is the point at which inventory is replenished to avoid stockouts. It can be calcualted as follows

 ### Reorder Point (RoP)=(Average Sales per Day×Average Lead Time)+Safety Stock
 
![download (18)](https://github.com/user-attachments/assets/542da326-62e7-45a7-a119-76fd927a7ed0)

From the boxplot it is evident that majority of the products have a very small ROP value. While some of them have very high rop values. These could be due to several reasons such as:-

1) High Average Demand: If the average demand for the product is high, the ROP will be higher because more inventory needs to be on hand to cover demand during the lead time.

2) Long Lead Time: A longer lead time increases the ROP because more inventory is needed to cover demand during the extended period before the new stock arrives.

 ### d. ABC Analysis

 This analysis is very useful in inventory manganemnt as it allows stakeholders to segerrage the top perfomring producfts against the poor perofroming products. it is divided into 3 types:-

1.Category A items: These are the most important products for the company, characterized by high sales volumes, high purchasing saless, or both. In terms of sales, these items represent 10%–20% of the sold quantity, accounting for 60%–80% of the annual sales value.

2.Category B items: These are less important items, consisting of 20%–30% of items sold, and accounting for 20%–30% of the annual sales amount.

3.Category C items: These are the least important items in your inventory, comprising 50%–70% of the inventory sold and accounting for 5%–15% of the annual sales value.

![download (20)](https://github.com/user-attachments/assets/a8195b98-1ba8-40d8-a45d-eb0111b0a30f)

From the distribution, it is evident that there is a lrage % of Category C items & least amount of Category A items.

### e. Business Insights

1. Top 10 products with large onhand inventory and thier ABC categories


![download (21)](https://github.com/user-attachments/assets/abee34cb-8f83-4a79-9d05-6239a858aef3)

2.  Products having large inventory count but less sales

![download (22)](https://github.com/user-attachments/assets/fc596af7-6baa-4c7c-98c7-fb86e63a035a)

3.Products requiring immediate re-order

![Screenshot 2024-09-11 162143](https://github.com/user-attachments/assets/1eb578f7-04dd-4eaf-960f-5a0eca515005)


### 3.  Predicting Optimal Reorder Quantity

Involves developing a machine learning model to predict optimal reorder quantities based on historical inventory data. The goal is to improve inventory management by accurately forecasting reorder quantities to maintain stock levels and avoid shortages.

### Key ComponentsKey Components:-

* a.  Data Preparation:

  Data Merging: Combined datasets containing beginning inventory, ending inventory, and    purchase information.

  Feature Engineering: Created features such as StockChange, LeadTimeDemand to capture historical demand patterns and stock changes.

* b.  Data Cleaning: Handled missing values and aligned data to ensure consistency.

* c.  Model Training:
  Chose relevant features for predicting reorder quantity.
  Used Random Forest Regressor Algorithm for predicting the reorder quantity: Trained the model with hyperparameters such as n_estimators=100 and max_depth=10.

  ![download (17)](https://github.com/user-attachments/assets/ce0acfa5-3f15-4123-aaf4-f22b63cb837b)

From the diagram we can see that the model is doing a good job in predicting the values.

* d. Evaluation:
Metrics: Assessd the  model performance using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R² score.

