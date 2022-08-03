# Introduction-to-Pandas
A guide of Pandas - The Python library for data manipulation and analysis

## About Pandas

For this introduction I will be using the population age structure as a dataset. The dataset was created in 2018 and contains the estimated population age structure in thousands in 5 year increments. Please see below:

![Data](images/data.png)

To access the data you first need to import pandas and load in the csv file to a DataFrame.

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
 ``` 
 
 From there, there are various inspections that can be done to explore the dataset and see what it contains.

| Function | Description |
| :-: | :-: | 
| .head() | Returns the first 5 rows of the DataFrame. |
| .info() | Displays information for each column (data type and number of missing values). | 
| .shape | Returns the number of rows and columns of the DataFrame. | 
| .describe() | Calculates a few summary statistics for each column (count and unique values).| 
| .values | Used to get a Numpy representation of the DataFrame.| 
| .columns | Returns the column labels of the DataFrame.| 
| .index | Return the index information of the DataFrame.| 

The results with the polulation age structure can be seen below:

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.head())
 ``` 
 ![Head](images/head.png)
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.info())
 ``` 
![Info](images/info.png)
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.shape)
 ``` 
![Shape](images/shape.png)
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.describe())
 ``` 
![Describe](images/describe.png)

  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.values)
 ```
![Values](images/values.png)

```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.columns)
 ```
 ![Columns](images/columns.png)
 
```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
print(df.index)
```

 ![Index](images/index.png)
 
 ### Sorting
 
 You can sort columns by there values ising the sort_values() function.:
 
 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values("All ages")
print(df.head())
```

 ![Sort-All-Ages](images/sort_all_ages_ascending.png)
 
 The ordering can be either ascending or descending with ascending = True being the default.

 ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values("All ages", ascending = False)
print(df.head())
```

 ![Sort-All-Ages-Descending](images/sort_all_ages_descending.png)
 
 Multiple columns can be sorted depending on their argument order. The type of sort can then be controlled by inputting a boolean list  
 
  ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df.sort_values(["0-4", "95-99"] ascending = [True, False])
print(df.head())
```
 ![Sort-Multiple-Columns](images/sort_multiple_columns.png)
 
 ### Subsetting Data
 
 #### Subsetting Columns
 
 Different columns can be selected by using the code below:
 
   ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df_over_hundred = df["100 & over"]
print(df_over_hundred.head())
```

 ![Subset-Over-Hundred](images/subset_column_hundred.png)
 
Multiple columns can be subset as shown:

   ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df[["100 & over", "All ages"]]
print(df.head())
```
 ![Subset-Multiple](images/subset_columns_multiple.png)
 
 
 #### Subsetting Rows
 
 The DataFrame can be filtered by using a relational operator to return True or False for each row and pass that inside quare brackets as shown.

   ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")
df = df[(df["100 & over"] > 200) & (df["5-9"] < 3000)]
print(df.head())
```

 ![Subset-Rows](images/subset_rows.png)

##### Subsetting Rows by Categorical Variables

Instead of using the "or" operator (|) to select multple rows. The isin() method allows only one condition to be writen instead of multiple.

   ```python
import pandas as pd

df = pd.read_csv("datafeed/population_age_structure_uk.csv")

next_five_years = [2023, 2023, 2024, 2025, 2026]

df = df[df["Ages"].isin(next_five_years)]
print(df)
```
 ![Subset-Categorical](images/subset_categorical.png)
