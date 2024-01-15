# Import necessary libraries
import streamlit as st
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Read the datasets
details_df = pd.read_csv("Details.csv")
orders_df = pd.read_csv("Orders.csv")

# Sidebar - Select analysis options
st.sidebar.header('Business Analysis Options')

# User selects analysis options
selected_analysis = st.sidebar.selectbox('Select Analysis', ['Most Sold Category', 'Most Sold Electronics Products', 'Top Cities and States', 'Monthly Sales'])

# Main content
st.title('Business Analysis App')

# Converting the Order Date column to Date type
orders_df["Order Date"] = pd.to_datetime(orders_df["Order Date"],format="mixed")
orders_df["Year"] = orders_df["Order Date"].dt.year
orders_df["Month"] = orders_df["Order Date"].dt.month

# Merge datasets on 'Order ID'
merged_df = pd.merge(details_df, orders_df, on='Order ID', how='inner')

# Analysis based on user selection
if selected_analysis == 'Most Sold Category':
    st.write('### Most Sold Category')
    # Sales by Category
    category_sales = merged_df.groupby('Category')['Amount'].sum().reset_index()
    print(category_sales)
    plt.figure(figsize=(12, 6))
    sns.barplot(x='Category', y='Amount', data=category_sales)
    plt.title('Total Sales by Category')
    plt.xlabel('Category')
    plt.ylabel('Total Sales')
    plt.xticks(rotation=45)
    plt.show()
    st.write("#### The Electronics Category is the most sold category followed by Clothing.")
        
elif selected_analysis == 'Most Sold Electronics Products':
    st.write('### Most Sold Electronics Products')
    electronics_df = merged_df[merged_df["Category"]=="Electronics"]
    subcategory_sales = electronics_df.groupby("Sub-Category")["Amount"].sum().reset_index()
    most_sold_products = subcategory_sales.sort_values(by="Amount",ascending=False)
    plt.figure(figsize=(12,6))
    sns.barplot(x="Sub-Category",y="Amount",data=most_sold_products)
    plt.title("Total sales by products")
    plt.xlabel("Products")
    plt.ylabel("Total Sales Amount")
    plt.show()
    st.write("####  Printers are the most sold Products in Electronics.")

elif selected_analysis == 'Top Cities and States':
    st.write('### Top Cities and States')
    # Sales by City
    city_sales = merged_df.groupby('City')['Amount'].sum().reset_index().sort_values(by='Amount', ascending=False)
    # Sales by State
    state_sales = merged_df.groupby('State')['Amount'].sum().reset_index().sort_values(by='Amount', ascending=False)
    # Set up the matplotlib figure
    fig, axes = plt.subplots(nrows=2, ncols=1, figsize=(14, 12))
    # Bar chart for Sales by City
    sns.barplot(x='Amount', y='City', data=city_sales.head(10), ax=axes[0], palette='viridis')
    axes[0].set_title('Top 10 Cities by Sales')
    axes[0].set_xlabel('Total Sales')
    axes[0].set_ylabel('City')
    # Bar chart for Sales by State
    sns.barplot(x='Amount', y='State', data=state_sales.head(10), ax=axes[1], palette='viridis')
    axes[1].set_title('Top 10 States by Sales')
    axes[1].set_xlabel('Total Sales')
    axes[1].set_ylabel('State')
    # Adjust layout to prevent overlap
    plt.tight_layout()
    # Show the plots
    plt.show()
    st.write("#### The graphs demonstrates that the states of 'Maharashtra' and 'Madhya Pradesh' are the most profitable states for the company, also the cities of 'Indore' and 'Mumbai' have the most sales compared to the other cities in India.")

elif selected_analysis == 'Monthly Sales':
    st.write('### Monthly Sales')
    monthly_sales = merged_df.groupby("Month")["Amount"].sum().reset_index().sort_values(by="Amount",ascending=False)
    plt.figure(figsize=(14, 6))
    month_names = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
    sns.barplot(x="Month",y="Amount",data = monthly_sales)
    plt.title("Sales amount by month")
    plt.xlabel("Month")
    plt.ylabel("Sales")
    plt.xticks(ticks=range(12),labels=month_names)
    plt.show()
    st.write("####  January is the month to have the most sales, followed by August and October.")
