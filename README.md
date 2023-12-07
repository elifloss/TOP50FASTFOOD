# Fast-Food Chains Dataset

## Overview

This dataset provides comprehensive information on various fast-food chains in the United States, focusing on key financial and operational metrics. It includes data on U.S. systemwide sales, average sales per unit, the number of franchised and company-owned stores, 2021 total units, and the total change in units from 2020. This dataset is valuable for researchers, analysts, and enthusiasts looking to understand the financial and operational dynamics of fast-food chains in the USA.

## Content

The dataset encompasses the following key attributes for each fast-food chain:

1. **Fast-Food Chain Name:** The name of the fast-food chain.

2. **U.S. Systemwide Sales (Millions - U.S. Dollars):** The total sales across all units of the chain in the United States, represented in millions of U.S. dollars.

3. **Average Sales per Unit (Thousands - U.S. Dollars):** The average sales generated per unit (store) of the chain, represented in thousands of U.S. dollars.

4. **Franchised Stores:** The number of stores operated by franchisees.

5. **Company Stores:** The number of stores owned and operated by the company.

6. **2021 Total Units:** The total count of units (stores) in the year 2021.

7. **Total Change in Units from 2020:** The net change in the number of units (stores) from the year 2020.

# Fast-Food Chains Dataset

## Overview

This dataset provides comprehensive information on various fast-food chains in the United States, focusing on key financial and operational metrics. It includes data on U.S. systemwide sales, average sales per unit, the number of franchised and company-owned stores, 2021 total units, and the total change in units from 2020. This dataset is valuable for researchers, analysts, and enthusiasts looking to understand the financial and operational dynamics of fast-food chains in the USA.

## Data Loading and Exploration

To work with the dataset, you can use the `datascience` library to create a Table and then convert it into a Pandas DataFrame for more extensive analysis:

```python
# Load dataset into a datascience Table
fastfood_table = Table.read_table('Fastfood_USA.csv')

# Convert the Table to a Pandas DataFrame
fastfood_df = fastfood_table.to_df()

# Check for missing values using isnull() in Pandas DataFrame
missing_values = fastfood_df.isnull().sum()
print(missing_values)
# Find the fast-food chain with the highest systemwide sales in 2021
highest_sales_chain = fastfood_df.loc[fastfood_df['U.S. Systemwide Sales (Millions - U.S Dollars)'].idxmax()]

# Display the fast-food chain with the highest systemwide sales in 2021
print("Fast-Food Chain with the Highest Systemwide Sales in 2021:")
print(highest_sales_chain[['Fast-Food Chains', 'U.S. Systemwide Sales (Millions - U.S Dollars)']])

# Sort by U.S. Systemwide Sales to identify chains with the least sales
bottom_sales_chains = fastfood_table.sort('U.S. Systemwide Sales (Millions - U.S Dollars)').take[:10]

print("Chains with the least U.S. Systemwide Sales:")
print(bottom_sales_chains.select(['Fast-Food Chains', 'U.S. Systemwide Sales (Millions - U.S Dollars)']))

# Sort by U.S. Systemwide Sales to identify the top-performing chains
top_sales_chains = fastfood_table.sort('U.S. Systemwide Sales (Millions - U.S Dollars)', descending=True).take[:10]

print("Top-performing chains based on U.S. Systemwide Sales:")
print(top_sales_chains)

# Sort by Average Sales per Unit to identify top-performing chains
top_avg_sales_chains = fastfood_table.sort('Average Sales per Unit (Thousands - U.S Dollars)', descending=True).take[:10]

print("\nTop-performing chains based on Average Sales per Unit:")
print(top_avg_sales_chains)

# Calculate correlation between U.S. Systemwide Sales and Average Sales per Unit
sales_correlation = fastfood_df['U.S. Systemwide Sales (Millions - U.S Dollars)'].corr(
    fastfood_df['Average Sales per Unit (Thousands - U.S Dollars)']
)

print("Correlation between U.S. Systemwide Sales and Average Sales per Unit:", sales_correlation)

# Filter for chains with a low number of franchised stores (e.g., less than 50)
low_franchise_threshold = 50
low_franchise_chains = fastfood_df[fastfood_df['Franchised Stores'] < low_franchise_threshold]

# Calculate average sales per unit for these chains
low_franchise_chains['Sales per Unit'] = low_franchise_chains['U.S. Systemwide Sales (Millions - U.S Dollars)'] / low_franchise_chains['2021 Total Units']

# Find the chain with the highest average sales per unit among these low franchised stores chains
highest_avg_sales_chain = low_franchise_chains.loc[low_franchise_chains['Sales per Unit'].idxmax()]

# Display the chain with the highest average sales per unit and low franchised stores
print("Chain with the highest average sales per unit and low franchised stores:")
print(highest_avg_sales_chain[['Fast-Food Chains', 'Average Sales per Unit (Thousands - U.S Dollars)', 'Franchised Stores']])

# Calculate the total number of fast-food franchises in the U.S.
total_franchises = fastfood_table['Franchised Stores'].sum()
print("Total number of fast-food franchises open in the U.S.: ", total_franchises)

# Find the fast-food chain with the most growth from 2020 to 2021
most_growth_chain = fastfood_df.loc[fastfood_df['Total Change in Units from 2020'].idxmax()]
print("Fast-food chain with the most growth from 2020 to 2021:")
print(most_growth_chain[['Fast-Food Chains', 'Total Change in Units from 2020']])

# Calculate growth rate
fastfood_df['Growth Rate'] = (fastfood_df['U.S. Systemwide Sales (Millions - U.S Dollars)'] / (fastfood_df['Total Change in Units from 2020'] + 1)) - 1

# Get the top 3 performing chains in terms of growth rate
top_3_growth_chains = fastfood_df.nlargest(3, 'Growth Rate')[['Fast-Food Chains', 'Growth Rate']]

print("Top 3 performing chains in terms of U.S. Systemwide Sales Growth Rate from 2020 to 2021:")
print(top_3_growth_chains)

# Calculate the total number of fast-food franchises in the U.S.
total_franchises = fastfood_table['Franchised Stores'].sum()
print("Total number of fast-food franchises open in the U.S.: ", total_franchises)

# Find the fast-food chain with the most growth from 2020 to 2021
most_growth_chain = fastfood_df.loc[fastfood_df['Total Change in Units from 2020'].idxmax()]
print("Fast-food chain with the most growth from 2020 to 2021:")
print(most_growth_chain[['Fast-Food Chains', 'Total Change in Units from 2020']])

# Calculate growth rate
fastfood_df['Growth Rate'] = (fastfood_df['U.S. Systemwide Sales (Millions - U.S Dollars)'] / (fastfood_df['Total Change in Units from 2020'] + 1)) - 1

# Get the top 3 performing chains in terms of growth rate
top_3_growth_chains = fastfood_df.nlargest(3, 'Growth Rate')[['Fast-Food Chains', 'Growth Rate']]

print("Top 3 performing chains in terms of U.S. Systemwide Sales Growth Rate from 2020 to 2021:")
print(top_3_growth_chains)
