# NumPy & Pandas — AI/ML Practical Notes

> A practical, placement-focused reference for the NumPy and Pandas features most commonly used in AI/ML, data analysis, and preprocessing.

---

# Table of Contents

1. [NumPy](#numpy)
2. [NumPy Arrays](#numpy-arrays)
3. [NumPy Data Types](#numpy-data-types)
4. [Creating Arrays](#creating-arrays)
5. [Indexing and Slicing](#indexing-and-slicing)
6. [Array Shape and Reshaping](#array-shape-and-reshaping)
7. [Array Operations](#array-operations)
8. [Broadcasting](#broadcasting)
9. [Aggregation and Statistics](#aggregation-and-statistics)
10. [Conditional Selection](#conditional-selection)
11. [Sorting and Searching](#sorting-and-searching)
12. [Stacking and Splitting](#stacking-and-splitting)
13. [Linear Algebra](#linear-algebra)
14. [Random Numbers](#random-numbers)
15. [Missing/Invalid Numerical Values](#missinginvalid-numerical-values)
16. [Vectorization](#vectorization)
17. [NumPy for ML](#numpy-for-ml)
18. [Pandas](#pandas)
19. [Series and DataFrame](#series-and-dataframe)
20. [Reading and Writing Data](#reading-and-writing-data)
21. [Inspecting Data](#inspecting-data)
22. [Selecting Rows and Columns](#selecting-rows-and-columns)
23. [Filtering](#filtering)
24. [Adding, Updating and Removing Data](#adding-updating-and-removing-data)
25. [Missing Data](#missing-data)
26. [Duplicates](#duplicates)
27. [Sorting](#sorting)
28. [String Operations](#string-operations)
29. [GroupBy](#groupby)
30. [Merge, Join and Concat](#merge-join-and-concat)
31. [Apply and Map](#apply-and-map)
32. [Dates and Times](#dates-and-times)
33. [Data Type Conversion](#data-type-conversion)
34. [Pandas Statistics](#pandas-statistics)
35. [ML Preprocessing Workflow](#ml-preprocessing-workflow)
36. [NumPy vs Pandas](#numpy-vs-pandas)
37. [Interview Questions](#interview-questions)
38. [Quick Cheat Sheet](#quick-cheat-sheet)

---

# NumPy

## What is NumPy?

**NumPy = Numerical Python**

NumPy is a Python library for numerical computing. Its main object is the **`ndarray`**, an N-dimensional array.

NumPy is heavily used in AI/ML for:

- Numerical calculations
- Vectors and matrices
- Linear algebra
- Statistics
- Random number generation
- Fast array operations
- Data transformation
- Image/pixel manipulation
- Preparing numerical data for ML models

```python
import numpy as np

arr = np.array([10, 20, 30])
print(arr)
```

### Why NumPy instead of normal Python lists?

NumPy arrays provide efficient numerical operations and vectorization. They are designed for homogeneous numerical data and are generally much faster and more memory-efficient for large numerical workloads than repeatedly operating on Python lists.

---

# NumPy Arrays

## 1D Array

```python
import numpy as np

a = np.array([1, 2, 3, 4])
```

## 2D Array

```python
a = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

## 3D Array

```python
a = np.array([
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
])
```

### Important properties

```python
a.shape
a.ndim
a.size
a.dtype
a.itemsize
```

- `shape` → dimensions
- `ndim` → number of dimensions
- `size` → total number of elements
- `dtype` → data type
- `itemsize` → bytes used by one element

---

# NumPy Data Types

Common NumPy data types:

```python
np.int32
np.int64
np.float32
np.float64
np.bool_
np.str_
```

Specify a type:

```python
a = np.array([1, 2, 3], dtype=np.float32)
```

Convert:

```python
a.astype(np.int64)
```

---

# Creating Arrays

## `np.array()`

```python
a = np.array([1, 2, 3])
```

## `np.zeros()`

```python
np.zeros(5)
```

2D:

```python
np.zeros((2, 3))
```

## `np.ones()`

```python
np.ones((2, 3))
```

## `np.full()`

```python
np.full((2, 3), 7)
```

## `np.empty()`

```python
np.empty((2, 3))
```

`empty()` allocates an array without initializing its values to a useful default.

## `np.arange()`

```python
np.arange(0, 10, 2)
```

Result:

```text
[0 2 4 6 8]
```

## `np.linspace()`

Creates evenly spaced values over an interval:

```python
np.linspace(0, 1, 5)
```

Result:

```text
[0.   0.25 0.5  0.75 1.  ]
```

## Identity matrix

```python
np.eye(3)
```

---

# Indexing and Slicing

## 1D

```python
a = np.array([10, 20, 30, 40, 50])

a[0]       # 10
a[-1]      # 50
a[1:4]     # [20 30 40]
a[:3]
a[2:]
a[::2]
```

## 2D

```python
a = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

a[0, 1]    # 20
a[1, 2]    # 60
```

Entire row:

```python
a[0]
```

Entire column:

```python
a[:, 1]
```

---

# Array Shape and Reshaping

```python
a = np.arange(12)

a.reshape(3, 4)
```

Flatten:

```python
a.flatten()
```

Reshape without copying when possible:

```python
a.ravel()
```

Transpose:

```python
a.T
```

Swap axes:

```python
np.swapaxes(a, 0, 1)
```

Add a dimension:

```python
a[np.newaxis, :]
```

Remove dimensions of size 1:

```python
np.squeeze(a)
```

### Important

The number of elements must remain compatible:

```python
np.arange(12).reshape(3, 4)   # valid
np.arange(12).reshape(2, 6)   # valid
np.arange(12).reshape(5, 3)   # invalid
```

---

# Array Operations

NumPy performs element-wise operations.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

a + b
a - b
a * b
a / b
a ** 2
```

Important distinction:

```python
a * b
```

is element-wise multiplication.

For matrix multiplication:

```python
a @ b
```

or:

```python
np.matmul(a, b)
```

---

# Universal Functions (ufuncs)

NumPy provides fast element-wise mathematical functions.

```python
np.sqrt(a)
np.square(a)
np.abs(a)
np.exp(a)
np.log(a)
np.log10(a)
np.sin(a)
np.cos(a)
np.round(a)
np.floor(a)
np.ceil(a)
```

Example:

```python
x = np.array([1, 4, 9])

print(np.sqrt(x))
```

---

# Broadcasting

Broadcasting allows NumPy to perform operations between compatible shapes.

```python
a = np.array([10, 20, 30])

a + 5
```

Result:

```text
[15 25 35]
```

2D example:

```python
a = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

a + np.array([10, 20, 30])
```

Result:

```text
[[11 22 33]
 [14 25 36]]
```

Broadcasting is extremely useful in ML preprocessing.

---

# Aggregation and Statistics

```python
a = np.array([10, 20, 30, 40, 50])

np.sum(a)
np.mean(a)
np.median(a)
np.min(a)
np.max(a)
np.std(a)
np.var(a)
```

Percentiles:

```python
np.percentile(a, 50)
```

Cumulative sum:

```python
np.cumsum(a)
```

Cumulative product:

```python
np.cumprod(a)
```

### Axis

For:

```python
a = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

Column-wise:

```python
np.sum(a, axis=0)
```

Row-wise:

```python
np.sum(a, axis=1)
```

A useful rule:

- `axis=0` → operate down rows, producing one value per column
- `axis=1` → operate across columns, producing one value per row

---

# Conditional Selection

Boolean masking:

```python
a = np.array([10, 25, 30, 5, 40])

a[a > 20]
```

Multiple conditions:

```python
a[(a > 10) & (a < 40)]
```

Use `&`, `|`, and `~` for element-wise boolean operations.

```python
a[(a > 20) | (a < 10)]
```

`np.where()`:

```python
np.where(a > 20, "High", "Low")
```

Find indices:

```python
np.where(a > 20)
```

---

# Sorting and Searching

```python
a = np.array([30, 10, 50, 20])

np.sort(a)
```

Indices that would sort the array:

```python
np.argsort(a)
```

Maximum/minimum index:

```python
np.argmax(a)
np.argmin(a)
```

Unique values:

```python
np.unique(a)
```

Count unique values:

```python
values, counts = np.unique(a, return_counts=True)
```

---

# Stacking and Splitting

## Vertical stacking

```python
a = np.array([1, 2])
b = np.array([3, 4])

np.vstack((a, b))
```

## Horizontal stacking

```python
np.hstack((a, b))
```

## Concatenation

```python
np.concatenate((a, b))
```

## Splitting

```python
a = np.arange(10)

np.split(a, 2)
```

---

# Linear Algebra

Linear algebra is fundamental to machine learning and deep learning.

```python
A = np.array([
    [1, 2],
    [3, 4]
])

B = np.array([
    [5, 6],
    [7, 8]
])
```

Matrix multiplication:

```python
A @ B
```

Dot product:

```python
np.dot(A, B)
```

Transpose:

```python
A.T
```

Determinant:

```python
np.linalg.det(A)
```

Inverse:

```python
np.linalg.inv(A)
```

Solve a linear system:

```python
b = np.array([5, 6])

np.linalg.solve(A, b)
```

Eigenvalues/eigenvectors:

```python
np.linalg.eig(A)
```

Norm:

```python
np.linalg.norm(A)
```

---

# Random Numbers

Modern NumPy code should generally use a random generator:

```python
rng = np.random.default_rng(42)

rng.random(5)
rng.integers(1, 100, size=5)
```

Normal distribution:

```python
rng.normal(loc=0, scale=1, size=5)
```

Shuffle:

```python
arr = np.arange(10)
rng.shuffle(arr)
```

Why random numbers matter in ML:

- Weight initialization
- Sampling
- Data shuffling
- Train/test experiments
- Simulations

### Reproducibility

A fixed seed helps reproduce results:

```python
rng = np.random.default_rng(42)
```

---

# Missing/Invalid Numerical Values

NaN:

```python
a = np.array([1, 2, np.nan, 4])
```

Check NaN:

```python
np.isnan(a)
```

Check infinity:

```python
np.isinf(a)
```

Check finite values:

```python
np.isfinite(a)
```

Replace NaN:

```python
np.nan_to_num(a, nan=0)
```

Statistics that ignore NaN:

```python
np.nanmean(a)
np.nanmedian(a)
np.nansum(a)
```

---

# Vectorization

Vectorization means applying operations to an entire array instead of manually looping over each element.

Python loop:

```python
result = []

for x in data:
    result.append(x * 2)
```

NumPy:

```python
result = data * 2
```

Vectorization usually makes numerical code cleaner and faster.

---

# NumPy for ML

A common workflow:

```text
Raw numerical data
       ↓
   NumPy array
       ↓
Cleaning / transformation
       ↓
Scaling / normalization
       ↓
Feature matrix X
       ↓
ML model
       ↓
Prediction
```

### Min-Max normalization

```python
x = np.array([10, 20, 30, 40, 50])

x_scaled = (x - x.min()) / (x.max() - x.min())
```

### Standardization

```python
x_standardized = (x - x.mean()) / x.std()
```

In production ML, prefer established preprocessing tools such as `sklearn.preprocessing.StandardScaler` when appropriate, especially when the transformation must be learned from training data and reused consistently.

---

# Pandas

## What is Pandas?

**Pandas** is a Python library for working with structured and labeled data.

It is commonly used for:

- Loading datasets
- Data exploration
- Cleaning
- Filtering
- Sorting
- Grouping
- Joining datasets
- Handling missing values
- Feature preparation
- Statistical analysis
- Working with CSV/Excel/JSON data

Import:

```python
import pandas as pd
```

The two core structures are:

- `Series`
- `DataFrame`

---

# Series and DataFrame

## Series

A Series is a one-dimensional labeled data structure.

```python
s = pd.Series([10, 20, 30, 40])
```

With custom index:

```python
s = pd.Series(
    [85, 72, 91],
    index=["Rahul", "Amit", "Priya"]
)
```

Access:

```python
s["Rahul"]
```

---

# DataFrame

A DataFrame is a two-dimensional labeled table.

```python
df = pd.DataFrame({
    "Name": ["Rahul", "Amit", "Priya"],
    "Age": [21, 22, 20],
    "Marks": [85, 72, 91]
})
```

Think:

```text
DataFrame = rows + columns + labels
```

---

# Reading and Writing Data

## CSV

```python
df = pd.read_csv("data.csv")
```

Write:

```python
df.to_csv("output.csv", index=False)
```

## Excel

```python
df = pd.read_excel("data.xlsx")
```

Write:

```python
df.to_excel("output.xlsx", index=False)
```

## JSON

```python
df = pd.read_json("data.json")
```

Write:

```python
df.to_json("output.json", orient="records")
```

---

# Inspecting Data

First rows:

```python
df.head()
```

Last rows:

```python
df.tail()
```

Shape:

```python
df.shape
```

Column names:

```python
df.columns
```

Data types:

```python
df.dtypes
```

Detailed information:

```python
df.info()
```

Statistical summary:

```python
df.describe()
```

Unique values:

```python
df["City"].unique()
```

Number of unique values:

```python
df["City"].nunique()
```

Frequency:

```python
df["City"].value_counts()
```

---

# Selecting Rows and Columns

Column:

```python
df["Marks"]
```

Multiple columns:

```python
df[["Name", "Marks"]]
```

## `loc`

Label-based selection:

```python
df.loc[0]
```

Rows and columns:

```python
df.loc[0:2, ["Name", "Marks"]]
```

Condition:

```python
df.loc[df["Marks"] > 80, ["Name", "Marks"]]
```

## `iloc`

Integer-position based selection:

```python
df.iloc[0]
```

First two rows and first two columns:

```python
df.iloc[0:2, 0:2]
```

### Remember

```text
loc  → labels / conditions
iloc → integer positions
```

---

# Filtering

Example:

```python
df[df["Marks"] > 80]
```

Multiple conditions:

```python
df[(df["Marks"] > 80) & (df["Age"] < 22)]
```

OR:

```python
df[(df["City"] == "Pune") | (df["City"] == "Mumbai")]
```

Membership:

```python
df[df["City"].isin(["Pune", "Mumbai"])]
```

Range:

```python
df[df["Marks"].between(70, 90)]
```

---

# Adding, Updating and Removing Data

Add column:

```python
df["Passed"] = df["Marks"] >= 40
```

Calculated column:

```python
df["BonusMarks"] = df["Marks"] + 5
```

Update values:

```python
df.loc[df["Marks"] < 40, "Passed"] = False
```

Drop column:

```python
df.drop(columns=["BonusMarks"])
```

Drop row by index:

```python
df.drop(index=0)
```

Use `inplace=True` only when you specifically want to mutate the existing object. Often, assigning the result is clearer:

```python
df = df.drop(columns=["BonusMarks"])
```

---

# Missing Data

Detect:

```python
df.isna()
```

Count missing values:

```python
df.isna().sum()
```

Alternative:

```python
df.isnull().sum()
```

Drop rows containing missing values:

```python
df = df.dropna()
```

Drop columns containing missing values:

```python
df = df.dropna(axis=1)
```

Fill with a constant:

```python
df["Age"] = df["Age"].fillna(21)
```

Fill with mean:

```python
df["Marks"] = df["Marks"].fillna(df["Marks"].mean())
```

Forward fill:

```python
df = df.ffill()
```

Backward fill:

```python
df = df.bfill()
```

### ML warning

When filling missing values for a predictive model, calculate statistics such as the mean from the **training data**, not from the full dataset, to avoid data leakage.

---

# Duplicates

Check:

```python
df.duplicated()
```

Count:

```python
df.duplicated().sum()
```

Remove:

```python
df = df.drop_duplicates()
```

Based on selected columns:

```python
df = df.drop_duplicates(subset=["Name"])
```

---

# Sorting

Ascending:

```python
df.sort_values("Marks")
```

Descending:

```python
df.sort_values("Marks", ascending=False)
```

Multiple columns:

```python
df.sort_values(
    ["City", "Marks"],
    ascending=[True, False]
)
```

---

# String Operations

Pandas provides `.str` methods.

```python
df["Name"].str.upper()
df["Name"].str.lower()
df["Name"].str.strip()
```

Contains:

```python
df[df["Name"].str.contains("rah", case=False, na=False)]
```

Starts with:

```python
df["Name"].str.startswith("A", na=False)
```

Replace:

```python
df["Name"].str.replace("Rahul", "R", regex=False)
```

---

# GroupBy

`groupby()` is used to split data into groups and calculate statistics.

Example:

```python
df.groupby("City")["Marks"].mean()
```

Multiple aggregations:

```python
df.groupby("City")["Marks"].agg(["mean", "min", "max", "count"])
```

Multiple columns:

```python
df.groupby("City").agg({
    "Marks": "mean",
    "Age": "mean"
})
```

### Concept

```text
GroupBy
   ↓
Split
   ↓
Apply calculation
   ↓
Combine result
```

---

# Merge, Join and Concat

## `merge()`

Similar to SQL JOIN.

```python
students = pd.DataFrame({
    "ID": [1, 2, 3],
    "Name": ["Rahul", "Amit", "Priya"]
})

marks = pd.DataFrame({
    "ID": [1, 2, 3],
    "Marks": [85, 72, 91]
})

result = pd.merge(students, marks, on="ID")
```

Different join types:

```python
pd.merge(left, right, on="ID", how="inner")
pd.merge(left, right, on="ID", how="left")
pd.merge(left, right, on="ID", how="right")
pd.merge(left, right, on="ID", how="outer")
```

## `concat()`

Stack DataFrames:

```python
pd.concat([df1, df2], axis=0)
```

Side-by-side:

```python
pd.concat([df1, df2], axis=1)
```

### Difference

```text
merge  → combine using matching keys
concat  → append/stack objects
join   → combine using indexes or keys
```

---

# Apply and Map

## `apply()`

Useful for applying a function across rows or columns.

```python
df["Marks"].apply(lambda x: x + 5)
```

Example:

```python
def grade(marks):
    if marks >= 80:
        return "A"
    elif marks >= 60:
        return "B"
    return "C"

df["Grade"] = df["Marks"].apply(grade)
```

For simple vectorized operations, prefer direct Pandas/NumPy operations over `apply()` when possible.

## `map()`

Useful for mapping values in a Series:

```python
mapping = {
    "Pune": "MH",
    "Mumbai": "MH",
    "Delhi": "DL"
}

df["State"] = df["City"].map(mapping)
```

---

# Dates and Times

Convert a column:

```python
df["Date"] = pd.to_datetime(df["Date"])
```

Extract year:

```python
df["Date"].dt.year
```

Month:

```python
df["Date"].dt.month
```

Day:

```python
df["Date"].dt.day
```

Day of week:

```python
df["Date"].dt.day_name()
```

---

# Data Type Conversion

Check:

```python
df.dtypes
```

Convert:

```python
df["Age"] = df["Age"].astype("int64")
```

Numeric conversion:

```python
df["Marks"] = pd.to_numeric(df["Marks"], errors="coerce")
```

Date conversion:

```python
df["Date"] = pd.to_datetime(df["Date"], errors="coerce")
```

`errors="coerce"` converts invalid values to missing values (`NaN`/`NaT`).

---

# Pandas Statistics

```python
df["Marks"].mean()
df["Marks"].median()
df["Marks"].mode()
df["Marks"].min()
df["Marks"].max()
df["Marks"].sum()
df["Marks"].std()
df["Marks"].var()
```

For an overview:

```python
df.describe()
```

Correlation:

```python
df.corr(numeric_only=True)
```

---

# ML Preprocessing Workflow

A realistic beginner ML workflow:

```text
CSV / Database
      ↓
   Pandas
      ↓
Load dataset
      ↓
Explore
      ↓
Clean missing values
      ↓
Remove duplicates
      ↓
Convert data types
      ↓
Filter / transform
      ↓
Select features
      ↓
Train/Test split
      ↓
Scaling / encoding
      ↓
NumPy / ML-compatible arrays
      ↓
Scikit-learn / TensorFlow / PyTorch
      ↓
Model
```

Example:

```python
import pandas as pd

df = pd.read_csv("house_data.csv")

print(df.head())
print(df.info())

df = df.drop_duplicates()

df["area"] = pd.to_numeric(df["area"], errors="coerce")
df["bedrooms"] = pd.to_numeric(df["bedrooms"], errors="coerce")

df = df.dropna(subset=["area", "bedrooms", "price"])

X = df[["area", "bedrooms"]]
y = df["price"]
```

Then an ML library can consume `X` and `y`.

---

# NumPy vs Pandas

| Feature | NumPy | Pandas |
|---|---|---|
| Main purpose | Numerical computing | Data analysis/manipulation |
| Main structure | `ndarray` | `Series`, `DataFrame` |
| Best for | Arrays, vectors, matrices | Tables/datasets |
| Labels | No built-in row/column labels | Yes |
| Missing data | Basic numerical support | Strong missing-data tools |
| CSV/Excel | Not its main purpose | Yes |
| Grouping | Limited/basic | `groupby()` |
| SQL-like joins | No main DataFrame join API | `merge()`, `join()` |
| Linear algebra | Strong | Usually delegated to NumPy |
| ML preprocessing | Numerical transformations | Dataset preparation |
| Typical role | Numerical engine | Data preparation/analysis |

### Easy memory trick

```text
NumPy
  ↓
Numbers + Arrays + Mathematics + Matrices

Pandas
  ↓
Tables + Cleaning + Filtering + Analysis
```

---

# How NumPy and Pandas Work Together

```text
                  Dataset
                     ↓
                Pandas 🐼
                     ↓
          Load + Clean + Analyze
                     ↓
             Select Features
                     ↓
                NumPy 🔢
                     ↓
          Numerical Operations
                     ↓
           ML / Deep Learning
```

In many workflows, you don't manually convert everything to NumPy because modern ML libraries can accept Pandas objects directly. Conversion is useful when an API specifically expects or benefits from NumPy arrays.

Convert DataFrame to NumPy:

```python
X = df[["Age", "Marks"]].to_numpy()
```

Convert NumPy array to DataFrame:

```python
df = pd.DataFrame(X, columns=["Age", "Marks"])
```

---

# Important NumPy Interview Questions

## 1. What is NumPy?

NumPy is a Python library for numerical computing that provides efficient multidimensional arrays and mathematical/linear-algebra operations.

## 2. What is `ndarray`?

`ndarray` is NumPy's multidimensional array object.

## 3. NumPy array vs Python list?

NumPy arrays are designed for efficient homogeneous numerical computation and support vectorized operations.

## 4. What is broadcasting?

Broadcasting is NumPy's mechanism for performing operations between arrays of compatible but different shapes.

## 5. Difference between `*` and `@`?

```python
A * B
```

Element-wise multiplication.

```python
A @ B
```

Matrix multiplication.

## 6. What is vectorization?

Performing operations on entire arrays rather than explicitly looping through individual elements.

## 7. What does `axis=0` mean?

For a 2D array, it performs the operation down rows and produces one result per column.

## 8. What does `reshape()` do?

It changes the shape of an array without changing the number of elements.

---

# Important Pandas Interview Questions

## 1. What is Pandas?

Pandas is a Python library for data manipulation, cleaning, analysis, and working with labeled/tabular data.

## 2. Series vs DataFrame?

```text
Series     → 1D labeled data
DataFrame  → 2D labeled table
```

## 3. `loc` vs `iloc`?

```text
loc   → label/condition based
iloc  → integer-position based
```

## 4. How do you find missing values?

```python
df.isna().sum()
```

## 5. How do you remove missing rows?

```python
df.dropna()
```

## 6. How do you remove duplicates?

```python
df.drop_duplicates()
```

## 7. What is `groupby()`?

It groups records according to one or more keys so that aggregate or other group-wise operations can be performed.

## 8. `merge()` vs `concat()`?

```text
merge  → combine based on matching keys
concat  → stack/append objects along an axis
```

## 9. How do you read CSV?

```python
pd.read_csv("file.csv")
```

## 10. How do you inspect a dataset?

```python
df.head()
df.shape
df.info()
df.describe()
df.dtypes
```

---

# Common Mistakes to Avoid

### Mistake 1: Confusing `loc` and `iloc`

```python
df.loc[0]
df.iloc[0]
```

They can return the same row when the index label is `0`, but they mean different things.

### Mistake 2: Using Python `and` / `or` for Series filtering

Wrong:

```python
df[(df["Age"] > 20) and (df["Marks"] > 80)]
```

Correct:

```python
df[(df["Age"] > 20) & (df["Marks"] > 80)]
```

### Mistake 3: Forgetting parentheses

Correct:

```python
df[(df["Marks"] > 80) & (df["Age"] < 22)]
```

### Mistake 4: Data leakage during preprocessing

Do not calculate preprocessing statistics from the test set and then use them to transform the training process.

Correct general idea:

```text
Training data
     ↓
Learn preprocessing parameters
     ↓
Transform training data
     ↓
Use the SAME learned parameters on validation/test data
```

---

# Quick Cheat Sheet

## NumPy

```python
import numpy as np

np.array()
np.zeros()
np.ones()
np.full()
np.arange()
np.linspace()
np.eye()

arr.shape
arr.ndim
arr.size
arr.dtype

arr.reshape()
arr.flatten()
arr.ravel()
arr.T

np.sum()
np.mean()
np.median()
np.std()
np.var()
np.min()
np.max()
np.percentile()

np.sort()
np.argsort()
np.argmax()
np.argmin()
np.unique()

np.where()

np.concatenate()
np.vstack()
np.hstack()
np.split()

np.dot()
np.matmul()
np.linalg.inv()
np.linalg.det()
np.linalg.solve()
np.linalg.norm()

np.isnan()
np.isinf()
np.isfinite()

np.random.default_rng()
```

## Pandas

```python
import pandas as pd

pd.Series()
pd.DataFrame()

pd.read_csv()
pd.read_excel()
pd.read_json()

df.head()
df.tail()
df.info()
df.describe()
df.shape
df.columns
df.dtypes

df["column"]
df[["col1", "col2"]]

df.loc[]
df.iloc[]

df.sort_values()
df.isna()
df.dropna()
df.fillna()
df.drop_duplicates()

df.groupby()
pd.merge()
pd.concat()

df.apply()
df["column"].map()

df["column"].str.upper()
df["column"].str.contains()

pd.to_datetime()
pd.to_numeric()

df.to_csv()
df.to_excel()
```

---

# What to Learn First for AI/ML

If your goal is **AI/ML + placements**, prioritize these topics.

## NumPy — Priority

```text
⭐⭐⭐ Arrays
⭐⭐⭐ Indexing & slicing
⭐⭐⭐ Shape & reshape
⭐⭐⭐ Broadcasting
⭐⭐⭐ Vectorization
⭐⭐⭐ Mean / std / sum / min / max
⭐⭐⭐ Matrix multiplication
⭐⭐  Linear algebra
⭐⭐  Random numbers
⭐⭐  Boolean masking
```

## Pandas — Priority

```text
⭐⭐⭐ DataFrame / Series
⭐⭐⭐ read_csv()
⭐⭐⭐ head() / info() / describe()
⭐⭐⭐ loc / iloc
⭐⭐⭐ Filtering
⭐⭐⭐ Missing values
⭐⭐⭐ GroupBy
⭐⭐⭐ merge / concat
⭐⭐⭐ Sorting
⭐⭐  apply / map
⭐⭐  String operations
⭐⭐  Date/time
```

---

# Final Mental Model

```text
                 PYTHON
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       NumPy 🧮            Pandas 🐼
          │                   │
    Numerical work       Data work
          │                   │
 Arrays / Matrices       DataFrames
 Vectorization           Cleaning
 Statistics              Filtering
 Linear Algebra          Grouping
 Random numbers          Joining
          │                   │
          └─────────┬─────────┘
                    ↓
             ML PREPROCESSING
                    ↓
             Scikit-learn
                    ↓
               ML MODEL
                    ↓
             Deep Learning
```

**If you remember only one thing:**

> **Pandas helps you understand and prepare the dataset; NumPy helps you perform fast numerical computation on the data.**
