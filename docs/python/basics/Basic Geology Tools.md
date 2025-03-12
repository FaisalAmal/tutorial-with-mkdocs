## Introduction
Geologists often work with large datasets containing information about rock formations, mineral deposits, geochemical compositions, and elevation data. Before applying any analysis, it’s essential to properly read, clean, and manipulate the data.

![Geological Tool](../../extra/assets/images/ST-12(2).jpg)

#### In this phase, we will focus on:
✅ Loading geological datasets (CSV, Excel, JSON).
✅ Performing basic data cleaning and manipulation using Pandas.
✅ Conducting numerical operations with NumPy for geological computations.

##### 📖 Step 1: Installing the Required Libraries
Before working with Pandas and NumPy, make sure they are installed in your Python environment.

```python
pip install pandas numpy

import pandas as pd
import numpy as np
```

##### 📖 Step 2: Loading Geological Datasets
Most geological data comes in the form of CSV (Comma-Separated Values), Excel, or JSON files. Here’s how to read them:

🔹 Loading a CSV File (Example: Rock Composition Data)

Note: This command loads a CSV file into a Pandas DataFrame and displays the first five rows.

```python
df = pd.read_csv("geological_data.csv")
print(df.head())  # Display the first 5 rows
```

🔹 Loading an Excel File (Example: Mineral Deposits Data)

Note: If the Excel file contains multiple sheets, specify the sheet_name parameter.

```python
df = pd.read_excel("mineral_deposits.xlsx", sheet_name="Sheet1")
print(df.head())
```

🔹 Loading a JSON File (Example: Geological Site Data)

Note: JSON files are often used for spatial data and can be converted into GeoDataFrames for GIS applications.

```python
df = pd.read_json("geological_sites.json")
print(df.head())
```

##### 📖 Step 3: Understanding the Dataset
After loading the dataset, it's important to inspect it:

🔹 This step helps in understanding the structure of the dataset before processing it.

```python
print(df.info())   # Summary of the dataset (columns, data types, null values)
print(df.describe())  # Statistical summary (mean, min, max, etc.)
print(df.columns)  # List of column names
print(df.shape)  # Number of rows and columns
```

##### 📖 Step 4: Cleaning the Data
🔹 Handling Missing Values
Sometimes, geological datasets have missing values (e.g., unrecorded mineral concentrations).

```python
df = df.dropna()  # Remove rows with missing values
# OR fill missing values with a default value
df = df.fillna(0)
```

🔹 Renaming Columns for Better Understanding

```python
df = df.rename(columns={"SiO2": "Silicon Dioxide", "Fe2O3": "Iron Oxide"})
```

🔹 Filtering Data (Example: Extracting Data for Specific Rock Types)

```python
sandstone_df = df[df["Rock_Type"] == "Sandstone"]
print(sandstone_df)
```

##### 📖 Step 5: Basic Data Manipulation with Pandas
🔹 Selecting Specific Columns

```python
selected_columns = df[["Rock_Type", "SiO2", "Fe2O3"]]
print(selected_columns.head())
```

🔹 Sorting the Data by Mineral Concentration

```python
df_sorted = df.sort_values(by="SiO2", ascending=False)
print(df_sorted.head())
```

🔹 Creating New Columns (Example: Calculating Mineral Ratios)

```python
df["SiO2_Fe2O3_Ratio"] = df["SiO2"] / df["Fe2O3"]
print(df.head())
```

##### 📖 Step 6: Numerical Computations with NumPy
🔹 Convert a Column to a NumPy Array

```python
siO2_array = df["SiO2"].values
print(siO2_array)
```

🔹 Compute Basic Statistics (Mean, Median, Standard Deviation)

```python
mean_sio2 = np.mean(siO2_array)
median_sio2 = np.median(siO2_array)
std_sio2 = np.std(siO2_array)

print(f"Mean SiO2: {mean_sio2}, Median SiO2: {median_sio2}, Std Dev SiO2: {std_sio2}")
```

🔹 Perform Mathematical Operations on an Entire Column

🔹 This normalizes the SiO2 values between 0 and 1, useful for machine learning applications.

```python
df["Normalized_SiO2"] = (df["SiO2"] - np.min(df["SiO2"])) / (np.max(df["SiO2"]) - np.min(df["SiO2"]))
print(df.head())
```

##### 📖 Step 7: Exporting Processed Data
After cleaning and processing, the data can be saved back to a file for further analysis.

```python
df.to_csv("processed_geological_data.csv", index=False)
df.to_excel("processed_geological_data.xlsx", index=False)
df.to_json("processed_geological_data.json")
```
