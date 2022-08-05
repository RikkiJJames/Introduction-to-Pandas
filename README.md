# Introduction-to-Pandas
A guide of Pandas - The Python library for data manipulation and analysis

* [Section 1 - About Pandas](#section-1---about-pandas)
* [Section 2 - Importing Data](#section-2---importing-data)
* [Section 3 - Inspecting Data](#section-3---inspecting-data)
  * [Head](#head)
  * [Info](#info)
  * [Shape](#shape)
  * [Describe](#describe)
  * [Values](#values)
  * [Columns](#columns)
  * [Index](#index)
* [Section 4 - Sorting Data](#section-4---sorting-data)
  * [Ascending](#ascending)
  * [Descending](#descending)
  * [Sorting Multiple Columns](#sorting-multiple-columns)
* [Section 5 - Subsetting Data](#section-5---subsetting-data)
  * [Subsetting Columns](#subsetting-columns)
    * [By Key](#by-key)
    * [By Variables](#by-variables)
    * [Subsetting Multiple Columns (By Name)](#subsetting-multiple-columns-by-name)
    * * [Subsetting Multiple Columns (By Index)](#subsetting-multiple-columns-by-index)
    * [Using Relational Operators](#using-relational-operators)
      * [Using isin](#using-isin)
    * [Relational Operators By Variables](#relational-operators-by-variables)
  * [Subsetting Rows](#subsetting-rows)
    * [By Row Number](#by-row-number)
    * [Subsetting Multiple Rows](#subsetting-multiple-rows)
  * [Resetting Indexes](#resetting-indexes)
    * [Resetting Indexes Inplace](#resetting-indexes-inplace)
* [Section 6 - Modifying DataFrames](#section-6---modifying-dataframes)
  * [Manual Column Creation](#manual-column-creation)
  * [Blanket Column Creation](#blanket-column-creation)
  * [Using Existing Data](#using-existing-data)
  * [Column Operations (apply)](#column-operations-apply)
  * [Lambda Functions](#lambda-functions)
    * [Lambda Functions On Rows](#lambda-functions-on-rows)
  * [Renaming Columns](#renaming-columns)
    * [Using The rename Function](#using-the-rename-function)
* [Section 7 - Aggregates](#section-7---aggregates)
  * [Group By](#group-by)
    * [Group By (Using Lambdas)](#group-by-using-lambdas)
    * [Group By (Multiple Columns)](#group-by-multiple-columns)
  * [Pivot Tables](#pivot-tables)
* [Section 8 - Multiple DataFrames](#section-8---multiple-dataframes)
 
  
## Section 1 - About Pandas


For this introduction I will be using the population age structure as a dataset. The dataset was created in 2018 and contains the estimated population age structure in thousands in 5 year increments. Please see below:

![Data](images/data.png)

## Section 2 - Importing Data

To access the data you first need to import pandas and load in the csv file to a DataFrame.

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
 ``` 

## Section 3 - Inspecting Data
 
 From there, there are various inspections that can be done to explore the dataset and see what it contains.

| Function | Description |
| :-: | :-: | 
| .head(x) | Returns the first x rows of the DataFrame. Defaults as 5 rows |
| .info() | Displays information for each column (data type and number of missing values). | 
| .shape | Returns the number of rows and columns of the DataFrame. | 
| .describe() | Calculates a few summary statistics for each column (count and unique values).| 
| .values | Used to get a Numpy representation of the DataFrame.| 
| .columns | Returns the column labels of the DataFrame.| 
| .index | Return the index information of the DataFrame.| 

The results with the polulation age structure can be seen below:

### Head

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.head())
 ``` 
 ![Head](images/head.png)
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.head(3))
 ``` 
 ![Head-X](images/head_3.png)
 
 ### Info
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.info())
 ``` 
![Info](images/info.png)
 
 ### Shape
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.shape)
 ``` 
 
![Shape](images/shape.png)
 
 ### Describe
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.describe())
 ``` 
![Describe](images/describe.png)

 ### Values
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.values)
 ```
![Values](images/values.png)

 ### Columns

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.columns)
 ```
 ![Columns](images/columns.png)
 
### Index
 
```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.index)
```

 ![Index](images/index.png)
 
 ## Section 4 - Sorting Data
 
 ### Ascending
 
 You can sort columns by their values ising the sort_values() function.:
 
 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values("All ages")
print(df.head())
```

 ![Sort-All-Ages](images/sort_all_ages_ascending.png)
 
 ### Descending
 
 The ordering can be either ascending or descending with ascending = True being the default.

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values("All ages", ascending = False)
print(df.head())
```

 ![Sort-All-Ages-Descending](images/sort_all_ages_descending.png)
 
  ### Sorting Multiple Columns
  
 Multiple columns can be sorted depending on their argument order. Ensure to use the double brackets or the comma won't work. The type of sort can then be controlled by inputting a boolean list  
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values(["0-4", "95-99"] ascending = [True, False])
print(df.head())
```
 ![Sort-Multiple-Columns](images/sort_multiple_columns.png)
 
 ## Section 5 - Subsetting Data
 
 ### Subsetting Columns
 
 #### By Key
 Different columns can be selected by using the code below:
 
```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df_over_hundred = df["100 & over"]
print(df_over_hundred.head())
```
 ![Subset-Over-Hundred](images/subset_column_hundred.png)
 
#### By Variables

If the heading of the columns follow the basic python variable naming rules. The columns can also be accessed as a variable.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.all_ages
print(df)
```

![Subset-Columns-Variable](images/subset_columns_variable.png)

#### Subsetting Multiple Columns (By Name)

Multiple columns can be subset as shown:

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df[["100 & over", "All ages"]]
print(df.head())
```

![Subset-Multiple](images/subset_columns_multiple.png)

#### Subsetting Multiple Columns (By Index)

Columns can also be selected using the index location method and list slicing:

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.iloc[:,0:3]
print(df.head())
```

![Subset-Multiple](images/subset_columns_multiple_index.png)
 
 #### Using Relational Operators
  
 The DataFrame can be filtered by using a relational operator to return True or False for each row and pass that inside square brackets as shown.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df[(df["100 & over"] > 200) & (df["5-9"] < 3000)]
print(df.head())
```

![Subset-Columns-Relational](images/subset_columns_relational.png)

##### Using isin

Instead of using the "or" operator (|) to select multple rows. The isin() method allows only one condition to be writen instead of multiple.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

next_five_years = [2023, 2023, 2024, 2025, 2026]

df = df[df["Ages"].isin(next_five_years)]
print(df)
```

 ![Subset-Categorical](images/subset_categorical.png)
 
#### Relational Operators by Variables

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df[(df.all_ages > 65000) & (df.years >2070)]
print(df)
```

![Subset-Columns-Relational-Variable](images/subset_columns_relational_variable.png)

 
 ### Subsetting Rows
 
 #### By Row Number
 
 You can select a single row using iloc.
 
```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
current_year = df.iloc[4]
print(current_year.head())
```

 ![Subset-Rows](images/subset_rows.png)
 
  #### Subsetting Multiple Rows
  
  You can select multiple rows through list splicing.
  
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
past_to_current_year = df.iloc[:4]
print(past_to_current_year.head())
```

 ![Subset-Multiple-Rows](images/subset_multiple_rows.png)
  
 
 ### Resetting Indexes
 
 When different rows are being selected the indexes can be out of order. To reset the indices use the reset_index() function.
 
```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.iloc[[2, 4, 6]]
print(df)
df = df.reset_index()
print(df)
```

 ![Reset-Index](images/reset_index.png)
 
 #### Resetting Indexes Inplace
 
The inplace and drop arguments can also be used to reorder and remove all other data from the DataFrame itself without needing to assign the result.

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.iloc[[2, 4, 6]]
print(df)
df.reset_index(inplace = True, drop = True)
print(df)
```

![Reset-Index-Inplace](images/reset_index_inplace.png)
 
## Section 6 - Modifying DataFrames

### Manual Column Creation

A new column can be added to the DataFrame by inserting a new list with matching length to the existing dataframe

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.head(2)

df["New Column"] = ["New", "New"]
print(df)
```

![Manual-Column-Creation](images/manual_column_creation.png)

### Blanket Column Creation

When a list is not used. All values in the new column will be equal to the value on the right.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df["Valid"] = True
print(df)
```

![Blanket-Column-Creation](images/blanket_column_creation.png)

### Using Existing Data

Often the values in the new table will be based on data in existing columns

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df["All Ages (in millions)"] = df["All ages"] * 1000
print(df.head())
```

![Existing-Data-Column-Creation](images/existing_data_column_creation.png)

### Column Operations (apply)

The apply function can be used to modify all entries in a DataFrame or Series. It applies any function to the values. For instance it can take a column entries as shown below:

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df["New Column] = "Yes
print(df.head())
```

![Column-Operations-Apply-Upper](images/column_operations_apply_upper.png)

and use the str.lower function to make them lowercase.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df["New Column] = "df[New Column"].apply(str.lower
print(df.head())
```

![Column-Operations-Apply-Lower](images/column_operations_apply_lower.png)


### Lambda Functions

Lambda functions are small anonymous function with one expression. They can be used to apply different rules to the data within the DataFrame. In general the syntax for an "if" statement in a lambda function is: lambda x: [OUTCOME IF TRUE] if [CONDITIONAL] else [OUTCOME IF FALSE].

Examples can be seen below

#### Lambda Functions On Columns

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df["Predictions"] = df.["years"].apply(lambda x True if x > 2022 else False)
print(df.head(10))
```

![Lambda-Columns](images/lambda_columns.png)

#### Lambda Functions On Rows

Lambda expressions can also be used to evaluate rows using the axis = 1 argument when applying the lambda

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

#Lambda Expression On Columns
df["check"] = df["0-4"].apply(lambda x: True if x > 3600 else False)

#Row Lambda Expression
under_twenty = lambda row: (row["0-4"] + row["5-9"] + row["10-14"] + row["15-19"]) if row["check"] == True else None

#Applying Row Lambda Expression to create new column
df["under_twenty"] = df.apply(under_twenty, axis = 1)

#Printing Columns Affected 
df2 = df.iloc[:, 0:5]
df2["under_twenty"] = df["under_twenty"]
```

![Lambda-Rows](images/lambda_rows.png)

### Renaming Columns

When obtaining data from other sources, sometimes it will be good to change the column names. For example, to reference the columns using variable rules such that "df.column_name" can be used instead of df["column_name"]. All columns can be changed at once by setting the column property to another list. However, this isn't recommended as its easy to mislabel.

See below:

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

df = df.iloc[:,:3] 
df.columns = ["Years", "Baby", "Young Child"]
print(df)
```

![Renaming-Columns](images/renaming_columns.png)

#### Using The rename Function

The better way to rename is to use the rename function which uses a dictionary with the original column name as the key, and the new one as the value. That way if the current name isn't exact. Nothing will be changed.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

df = df.iloc[:,:3] 
df.rename(columns = {"years": "Year", inplace = True)
print(df)
```

![Renaming-Columns-With-Function](images/renaming_columns_with_function.png)


## Section 7 - Aggregates

Aggregate functions summarize many data points (i.e., a column of a dataframe) into a smaller set of values. They follow the syntax "df.column_name.command()". See the table below for examples.

| Function | Description |
| :-: | :-: | 
| .mean() | Average of all values in column |
| .std() | Standard Deviation | 
| .median() | Median | 
| .max() | Maximum value in column| 
| .min() | Minimum value in column| 
| .count() | Number of values in column| 
| .nunique() | Number of unique values in column| 
| .unique() | List of unique values in column| 

See below for usage.

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

print(df["0-4"].max())
```

![Aggregates-Max](images/aggregates_max.png)

### Group By

The groupby operation involves some combination of splitting the object, applying a function, and combining the results. This can be used to group large amounts of data and compute operations on these groups.

This next section will interrogate the data shown below 

![Data-Grades](images/data_grades.png)

To calculate the mean score of each student the following code can be used:

```python
import pandas as pd

df = pd.read_csv("datafeed/grades.csv")

averages = df.groupby("student").score.mean()
print(averages)
print(type(averages))
```

![Average-Grade-Score](images/average_student_score.png)

The result of the code above is a Series. To keep it as a DataFrame - use the reset_index() function. The name of each column could also be used to keep each column up to data.

```python
import pandas as pd

df = pd.read_csv("datafeed/grades.csv")

averages = df.groupby("student").score.mean().reset_index()
averages.rename(columns = {"score": "average_score"}, inplace = True)
print(averages)
print(type(averages))
```

![Average-Grade-Score-DataFrame](images/average_student_score_df.png)


#### Group By (Using Lambdas)

Grouping can also be done with customisable lambda expressions

```python
import pandas as pd
import numpy as np

df = pd.read_csv("datafeed/grades.csv")

#Calculates 75 percentile
high_grade = df.groupby("student").score.apply(lambda x: np.percentile(x,75)).reset_index()
print(high_grade)
```

![Aggregates-Lambda](images/aggregates_lambda.png)

#### Group By (Multiple Columns)

Multiple columns can be grouped using a list as an argument in the groupby function.

```python
import pandas as pd


df = pd.read_csv("datafeed/grades.csv")

subjects = df.groupby(["assignment","student"]).score.mean().reset_index()
print(subjects)
```

![Aggregates-Multiple-Columns](images/aggregates_multiple_columns.png)

### Pivot Tables

In Pandas, tables output can be modified to change the layout using pivot tables.

```python
import pandas as pd


df = pd.read_csv("datafeed/grades.csv")

subjects = df.groupby(["assignment","student"]).score.mean().reset_index()
subjects_pivot = subjects.pivot(columns = "assignment", index = "student", values = "score").reset_index()
print(subjects_pivot)
```

![Aggregates-Pivot](images/aggregates_pivot.png)


## Section 8 - Multiple DataFrames
