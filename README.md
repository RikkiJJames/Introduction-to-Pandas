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
| .head() | Returns the first 5 rows of the DataFrame |
| .info() | Displays information for each column (data type and number of missing values). | 
| .shape | Returns the number of rows and columns of the DataFrame. | 
| .describe() | Calculates a few summary statistics for each column (count and unique values| 

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
