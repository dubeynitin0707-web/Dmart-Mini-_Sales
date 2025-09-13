# D-Mart Sales Analysis (Mini Version)

This repository contains a smaller version of my sales analysis project for D-Mart.  
The original project had a very large dataset that could not be uploaded to GitHub,  
so this version uses a smaller dataset but demonstrates the same analysis process.

## 📌 Project Overview
- Analyze sales data of D-Mart using *Python* and *MySQL*
- Perform queries to extract useful insights
- Use *Pandas, NumPy, and Matplotlib* for data analysis and visualization
- Understand customer buying patterns and sales performance

## 🛠️ Tech Stack
- *Python* 🐍  
- *MySQL* 🗄️  
- *Pandas, NumPy, Matplotlib* 📊  

🔹 Example Code Snippe 
# Import Libraries
# ===============================
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as mtick

# ===============================
# Load Data
# ===============================
df = pd.read_csv("/Users/nitindubey/Desktop/Dmart-Mini/DMartSalesdataMini2024.csv")
df['Date'] = pd.to_datetime(df['Date'], format='mixed', dayfirst=True, errors='coerce')
colors = ["red", "orange", "gold", "green", "deepskyblue", "blue", "purple", "magenta", "cyan", "brown"]

# ===============================
# Daily Sales Trend
# ===============================
daily_sales = df.groupby('Date')['GrandTotal'].sum()
ax = daily_sales.plot(figsize=(10, 5), title="Daily Sales Trend", color=colors)
ax.yaxis.set_major_formatter(mtick.StrMethodFormatter('₹{x:,.0f}'))
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Sales by Weekday
# ===============================
weekday_order = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
weekday_sales = df.groupby('days')['GrandTotal'].sum().reindex(weekday_order)

ax = weekday_sales.plot(kind='bar', title="Sales by Weekday", color=colors)
ax.yaxis.set_major_formatter(mtick.StrMethodFormatter('₹{x:,.0f}'))
for i, v in enumerate(weekday_sales):
    ax.text(i, v, f'{v:.0f}', ha='center', va='bottom')
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Sales by Time of Day
# ===============================
df.groupby("time_of_day")["GrandTotal"].sum().plot(
    kind="pie", title="Sales by Time of Day", autopct='%1.1f%%', color=colors)
plt.ylabel("")
plt.show()

# ===============================
# Revenue by Customer Type
# ===============================
df.groupby('CustomerType')['GrandTotal'].sum().plot(kind='bar', title="Revenue by Customer Type", color=colors)
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Sales by City
# ===============================
df.groupby('StoreCity')['GrandTotal'].sum().plot(kind='bar', title="Sales by City", color=colors)
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Sales by Branch
# ===============================
df.groupby('Branch')['GrandTotal'].sum().plot( kind='bar', title="Sales by Branch", color=colors)
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Payment Methods
# ===============================
df.groupby('PaymentMode')['GrandTotal'].sum().plot(kind='bar', title="Payment Method", color=colors)
plt.ylabel("Sales Amount (in ₹)")
plt.show()

# ===============================
# Festival Sales
# ===============================
df.groupby('Festival')['GrandTotal'].sum().plot(kind='pie', title="Festival Sales", autopct='%1.1f%%', color=colors)
plt.ylabel("Sales on Festivals")
plt.show()

# ===============================
# Extra Analysis - A
# ===============================
df.groupby('Date')['GrandTotal'].sum().plot(kind='bar',title="G-wise Sales",color=colors)
plt.ylabel("Data by date")

plt.show()


#===============================
# Extra Analysis - B
#===============================

df.groupby('Time')['GrandTotal'].sum().plot(kind='pie', title="Time of same ", autopct='%1.1f%%', color=colors)
plt.ylabel("Sales on Which time")
plt.show()
