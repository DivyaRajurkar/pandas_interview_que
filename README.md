# pandas_interview_que
Here is a comprehensive list of **Python Pandas interview questions** with theoretical explanations and coding examples to help you prepare.

---

### **Theoretical Questions**

1. **What is Pandas?**
   - **Answer:** Pandas is a Python library used for data manipulation and analysis. It provides data structures like `Series` and `DataFrame` to work with structured data efficiently.

2. **What are the main data structures in Pandas?**
   - **Answer:** 
     - `Series`: One-dimensional labeled array.
     - `DataFrame`: Two-dimensional labeled data structure with rows and columns.

3. **How is Pandas different from Numpy?**
   - **Answer:** While Numpy provides arrays for numerical computations, Pandas provides labeled data structures (`Series` and `DataFrame`) suitable for data analysis tasks, including handling missing data, indexing, and merging.

4. **What are some common methods in Pandas for handling missing data?**
   - **Answer:**
     - `isnull()` and `notnull()`: Detect missing values.
     - `fillna()`: Replace missing values with a specific value.
     - `dropna()`: Remove rows or columns with missing values.

5. **How can you filter rows in a DataFrame?**
   - **Answer:** Use conditional statements with the DataFrame, e.g., `df[df['Column'] > 10]`.

6. **What are groupby operations in Pandas?**
   - **Answer:** The `groupby` method allows you to group data by one or more columns and perform aggregate functions like `sum`, `mean`, or `count`.

7. **What is the difference between `apply`, `map`, and `applymap`?**
   - **Answer:**
     - `apply`: Used for row/column-wise operations in a DataFrame.
     - `map`: Used for element-wise operations on a Series.
     - `applymap`: Used for element-wise operations on a DataFrame.

8. **What is the difference between `loc` and `iloc`?**
   - **Answer:**
     - `loc`: Label-based indexing (uses row/column labels).
     - `iloc`: Integer-based indexing (uses row/column positions).

---

### **Coding Questions**

#### **1. Create a DataFrame and Perform Basic Operations**
```python
import pandas as pd

# Create a DataFrame
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'Salary': [50000, 60000, 70000]}
df = pd.DataFrame(data)

# Access specific column
print(df['Name'])

# Add a new column
df['Bonus'] = df['Salary'] * 0.1
print(df)

# Filter rows where Age > 25
filtered_df = df[df['Age'] > 25]
print(filtered_df)
```

---

#### **2. Handle Missing Data**
```python
# Create DataFrame with missing values
data = {'Name': ['Alice', 'Bob', None],
        'Age': [25, None, 35],
        'Salary': [50000, 60000, None]}
df = pd.DataFrame(data)

# Check for missing values
print(df.isnull())

# Fill missing values
df['Age'] = df['Age'].fillna(df['Age'].mean())
print(df)

# Drop rows with missing values
df = df.dropna()
print(df)
```

---

#### **3. Groupby and Aggregate Operations**
```python
data = {'Department': ['HR', 'IT', 'HR', 'IT'],
        'Employee': ['Alice', 'Bob', 'Charlie', 'David'],
        'Salary': [50000, 60000, 55000, 65000]}
df = pd.DataFrame(data)

# Group by Department and calculate average salary
grouped = df.groupby('Department')['Salary'].mean()
print(grouped)
```

---

#### **4. Merge Two DataFrames**
```python
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Marks': [85, 90, 75]})

# Merge DataFrames on ID
merged_df = pd.merge(df1, df2, on='ID', how='inner')
print(merged_df)
```

---

#### **5. Pivot Table Example**
```python
data = {'Name': ['Alice', 'Bob', 'Alice', 'Bob'],
        'Month': ['Jan', 'Jan', 'Feb', 'Feb'],
        'Sales': [200, 300, 400, 500]}
df = pd.DataFrame(data)

# Create a pivot table
pivot = df.pivot_table(values='Sales', index='Name', columns='Month', aggfunc='sum')
print(pivot)
```

---

#### **6. Create and Use a Custom Function with `apply`**
```python
# Add a new column with a custom function
df['Tax'] = df['Sales'].apply(lambda x: x * 0.1)
print(df)
```

---

#### **7. Sorting Data**
```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35]}
df = pd.DataFrame(data)

# Sort by Age in descending order
sorted_df = df.sort_values(by='Age', ascending=False)
print(sorted_df)
```

---

### **Tips for Interviews**
1. Practice writing code in a time-constrained environment.
2. Focus on understanding concepts like:
   - Data cleaning and handling missing data.
   - Filtering, grouping, and merging datasets.
   - Working with advanced functions (`apply`, `map`, etc.).
3. Prepare to explain your thought process for each solution.
4. Familiarize yourself with common edge cases, like handling missing or duplicate data.
Let’s explore some of the **Pandas interview questions** in more detail, with explanations and practical examples. We’ll go step-by-step so you can build a solid understanding.

---

### **1. Handling Missing Data**
#### **Scenario**: You are given a dataset with missing values and need to clean it for analysis.

#### **Code Explanation**
```python
import pandas as pd

# Sample DataFrame with missing values
data = {'Name': ['Alice', 'Bob', None],
        'Age': [25, None, 35],
        'Salary': [50000, 60000, None]}
df = pd.DataFrame(data)

print("Original DataFrame:")
print(df)

# Check for missing values
print("\nMissing Values:")
print(df.isnull())

# Fill missing Age with the mean
df['Age'] = df['Age'].fillna(df['Age'].mean())
print("\nAfter Filling Missing Age with Mean:")
print(df)

# Drop rows with missing values
df_cleaned = df.dropna()
print("\nAfter Dropping Rows with Missing Values:")
print(df_cleaned)
```

#### **Key Questions**
1. **Q**: How do you identify missing values in a DataFrame?
   - **A**: Use `isnull()` or `notnull()`.
2. **Q**: How can you handle missing values?
   - **A**: Use `fillna()` to fill missing values or `dropna()` to remove rows/columns.

---

### **2. Grouping and Aggregation**
#### **Scenario**: Calculate average salary for each department in a company.

#### **Code Explanation**
```python
data = {'Department': ['HR', 'IT', 'HR', 'IT'],
        'Employee': ['Alice', 'Bob', 'Charlie', 'David'],
        'Salary': [50000, 60000, 55000, 65000]}
df = pd.DataFrame(data)

# Group by Department and calculate average salary
grouped = df.groupby('Department')['Salary'].mean()
print("Average Salary by Department:")
print(grouped)
```

#### **Key Questions**
1. **Q**: What does `groupby()` do?
   - **A**: It groups data based on a column and allows aggregation functions like `mean()`, `sum()`, etc.
2. **Q**: How do you group by multiple columns?
   - **A**: Use `groupby(['Column1', 'Column2'])`.

---

### **3. Merging DataFrames**
#### **Scenario**: Combine two datasets using a common key.

#### **Code Explanation**
```python
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Marks': [85, 90, 75]})

# Merge DataFrames on ID
merged_df = pd.merge(df1, df2, on='ID', how='inner')
print("Merged DataFrame (Inner Join):")
print(merged_df)

# Perform a left join
left_join_df = pd.merge(df1, df2, on='ID', how='left')
print("\nMerged DataFrame (Left Join):")
print(left_join_df)
```

#### **Key Questions**
1. **Q**: What are the types of joins in Pandas?
   - **A**: `inner`, `left`, `right`, and `outer`.
2. **Q**: What happens if a key is missing in one DataFrame?
   - **A**: It depends on the join type. For example, in an `inner` join, rows with missing keys are excluded.

---

### **4. Pivot Table**
#### **Scenario**: Summarize sales data by product and region.

#### **Code Explanation**
```python
data = {'Product': ['A', 'B', 'A', 'B'],
        'Region': ['North', 'North', 'South', 'South'],
        'Sales': [100, 200, 150, 250]}
df = pd.DataFrame(data)

# Create a pivot table
pivot = df.pivot_table(values='Sales', index='Product', columns='Region', aggfunc='sum')
print("Pivot Table:")
print(pivot)
```

#### **Key Questions**
1. **Q**: What is a pivot table?
   - **A**: A pivot table is used to summarize data based on specific rows and columns with aggregation.
2. **Q**: What does `aggfunc` do?
   - **A**: It specifies the aggregation function, e.g., `sum`, `mean`, etc.

---

### **5. Using Apply with Custom Functions**
#### **Scenario**: Apply a tax rate to calculate net salaries.

#### **Code Explanation**
```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Salary': [50000, 60000, 70000]}
df = pd.DataFrame(data)

# Define a custom function
def calculate_tax(salary):
    return salary * 0.1  # 10% tax

# Apply the custom function to the Salary column
df['Tax'] = df['Salary'].apply(calculate_tax)
print("DataFrame with Tax:")
print(df)
```

#### **Key Questions**
1. **Q**: What is the difference between `apply` and `map`?
   - **A**: `apply` works on DataFrames or Series, while `map` works only on Series.
2. **Q**: Can you use `apply` with a lambda function?
   - **A**: Yes, e.g., `df['Column'].apply(lambda x: x + 1)`.

---

### **6. Sorting Data**
#### **Scenario**: Sort students by their scores in descending order.

#### **Code Explanation**
```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Score': [85, 90, 75]}
df = pd.DataFrame(data)

# Sort by Score in descending order
sorted_df = df.sort_values(by='Score', ascending=False)
print("Sorted DataFrame:")
print(sorted_df)
```

#### **Key Questions**
1. **Q**: How do you sort multiple columns?
   - **A**: Use `sort_values(by=['Col1', 'Col2'])`.
2. **Q**: What does `ascending=False` do?
   - **A**: Sorts the column in descending order.

---

### **Practice Tips**
- Try modifying the examples with your own datasets.
- Experiment with edge cases, like empty DataFrames or DataFrames with all missing values.
- For each function (`groupby`, `merge`, etc.), focus on understanding **parameters** like `how`, `aggfunc`, and others.


