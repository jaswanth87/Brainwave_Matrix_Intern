import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("supermarket_sales.csv")

# Convert 'Date' to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Summary calculations
total_revenue = df['Total'].sum()
total_transactions = df.shape[0]
avg_sale = df['Total'].mean()
top_products = df['Product'].value_counts().head(5)
sales_by_city = df.groupby('City')['Total'].sum()

# Print summary
print(f"Total Revenue: ₹{total_revenue:.2f}")
print(f"Total Transactions: {total_transactions}")
print(f"Average Sale per Transaction: ₹{avg_sale:.2f}")
print("\nTop 5 Products:")
print(top_products)
print("\nSales by City:")
print(sales_by_city)

# Visualizations
# Sales by City
plt.figure(figsize=(6, 4))
sns.barplot(x='City', y='Total', data=df, estimator=sum)
plt.title('Total Sales by City')
plt.ylabel('Sales Amount')
plt.tight_layout()
plt.savefig("sales_by_city.png")
plt.close()

# Top Products
plt.figure(figsize=(6, 4))
top_products.plot(kind='bar', color='skyblue')
plt.title('Top 5 Sold Products')
plt.ylabel('Units Sold')
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig("top_products.png")
plt.close()

# Payment Methods
plt.figure(figsize=(6, 4))
sns.countplot(x='Payment Method', data=df)
plt.title('Payment Method Distribution')
plt.tight_layout()
plt.savefig("payment_methods.png")
plt.close()
