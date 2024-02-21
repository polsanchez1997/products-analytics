EDA and Analysis of Orders Data

Overview

This project involves the exploratory data analysis (EDA) of a dataset containing information about orders. The dataset was loaded and cleaned using a provided function, and various analyses were performed to answer specific questions.

Data Cleaning

The data cleaning process included renaming columns for clarity and dropping duplicate rows.

Questions and Analysis

1. Percentage of Under-Authorized Orders

To determine the percentage of under-authorized orders, a new DataFrame was created by iterating over the rows and applying the condition.


# Percentage of Under-Authorized Orders

df_under_authorized = df[df['products_total'] < df['purchase_total_price']]

percentage_under_authorized = (df_under_authorized.shape[0] / df.shape[0]) * 100

2. Percentage of Correctly Authorized Orders with Incremental Authorization

A new column was created by multiplying the products_total by 1.2, representing a 20% increase. The percentage of correctly authorized orders was then calculated.


# Percentage of Correctly Authorized Orders with Incremental Authorization

df["products_total_checkout"] = df["products_total"] * 1.2

df_correctly_authorized_checkout = df[df['products_total_checkout'] >= df['purchase_total_price']]

percentage_good_with_checkout = (df_correctly_authorized_checkout.shape[0] / df.shape[0]) * 100

3. Analysis by Country

The dataset was split by country, and value counts were calculated for total orders, authorized orders, and under-authorized orders. A bar graph was created to visualize the number of under-authorized orders by country.


# Analysis by Country

4. Remaining Amount for Under-Authorized Orders

A new column, remaining_amount, was created to calculate the difference between purchase_total_price and products_total for under-authorized orders.


# Remaining Amount for Under-Authorized Orders
df_under_authorized["remaining_amount"] = df_under_authorized["purchase_total_price"] - df_under_authorized["products_total"]

5. Problematic Stores by Orders and Monetary Value

Boolean columns were added to indicate whether an order was authorized or not. Problematic stores were then analyzed in terms of the number of under-authorized orders and monetary value.


# Problematic Stores by Orders and Monetary Value
df['under_authorized'] = df.apply(under_authorized, axis=1)

monetary_value = df.groupby('store_address')['purchase_total_price'].sum().sort_values(ascending=False)

orders_value = df.groupby('store_address')['under_authorized'].sum().sort_values(ascending=False)

6. Correlation between Price Difference and Order Cancellation

A new column, remaining_amount, was created to represent the difference in prices. A scatter plot was generated to visualize the correlation between the remaining amount and the order's final status.


# Correlation between Price Difference and Order Cancellation

df["remaining_amount"] = df["purchase_total_price"] - df["products_total"]

Conclusion
The exploratory data analysis provides insights into various aspects of the orders dataset, including the percentage of under-authorized orders, the impact of incremental authorization, country-wise analysis, problematic stores, and the correlation between price difference and order cancellation. The findings can be used to make informed decisions and improvements in the order processing system.

Note: The provided code snippets are part of a larger analysis, and adjustments may be needed based on the specific structure and requirements of the dataset.