# Dask-Working-with-Large-Dataset
# Working with Large Datasets Using Dask

This repository demonstrates how to handle and analyze large datasets efficiently using **Dask**, a parallel computing library in Python designed to scale from small tasks to large, distributed systems.

## **Overview**
Dask provides a high-level interface for processing large datasets using familiar Python tools like pandas and NumPy. It enables out-of-core computation and parallel processing, making it ideal for tasks that exceed the limits of a single machine's memory.

## **Features**
- Process large datasets efficiently.
- Perform operations like filtering, grouping, and aggregations.
- Visualize results using libraries like Matplotlib and Seaborn.
- Handle data processing tasks seamlessly, even on limited resources.

## **Dataset**
The example dataset used contains the following fields:

| Column      | Description                              |
|-------------|------------------------------------------|
| OrderID     | Unique identifier for each order         |
| CustomerID  | Unique identifier for each customer      |
| ProductID   | Unique identifier for each product       |
| Category    | Product category (e.g., Electronics)     |
| Quantity    | Number of units purchased                |
| Price       | Price per unit                           |
| Date        | Date of the order                        |
| City        | City where the order was placed          |

## **Prerequisites**

Ensure you have the following installed:
- Python 3.7+
- Dask
- Pandas
- Matplotlib

Install required packages using pip:
```bash
pip install dask pandas matplotlib
```

## **Getting Started**

### **1. Load the Dataset**
```python
import dask.dataframe as dd

# Load the dataset
file_path = 'sales_data.csv'
dask_df = dd.read_csv(file_path)

# Preview the dataset
print(dask_df.head())
```

### **2. Perform Data Operations**

#### **Create a New Column**
Add a `TotalSales` column:
```python
dask_df['TotalSales'] = dask_df['Quantity'] * dask_df['Price']
```

#### **Filter Data**
Filter rows where Category is "Electronics" and Quantity > 2:
```python
filtered_df = dask_df[(dask_df['Category'] == 'Electronics') & (dask_df['Quantity'] > 2)]
print(filtered_df.compute())
```

#### **Group and Aggregate**
Group by City and calculate total sales:
```python
total_sales_by_city = dask_df.groupby('City')['TotalSales'].sum()
print(total_sales_by_city.compute())
```

### **3. Visualize Results**
Use Matplotlib for visualizing results:

#### **Example: Total Sales by City**
```python
import matplotlib.pyplot as plt

# Compute and plot
sales = total_sales_by_city.compute()
sales.plot(kind='bar', color='skyblue')
plt.title('Total Sales by City')
plt.xlabel('City')
plt.ylabel('Total Sales')
plt.show()
```

## **Advanced Features**
- Use Dask with distributed systems for massive datasets.
- Combine Dask with other big data tools like Hadoop or Spark.
- Optimize computations using Dask’s partitioning and task graphs.

## **Benefits of Dask**
- Scales from a single laptop to a large cluster.
- Integrates seamlessly with pandas, NumPy, and scikit-learn.
- Supports parallel, out-of-core computation.


