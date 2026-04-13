# Overview
Python module providing data structure for data analysis
### Use
```python
import pandas as pd
```
### Installation
`conda install -c conda-forge pandas`
# Best Practices
### Text Data
Use StringDtype
- better to have dedicated dtype
- string methods
```python
pd.Series(["a", "b", "c"], dtype="string")
```
# Technical
### Series
A one-dimensional labeled array holding data of any type
```python
""" Creation
	data can be dict, ndarray, or scalar value
"""
s = pd.Series(data, index=index)
s["a"] = 12  # update by label (like a dict)
"b" in s  # index in dict
```
### DataFrame
A two-dimensional data structure that holds data like a two-dimension array or a table with rows and columns
```python
""" Creation
	dict of 1D ndarrays, dicts, lists, or Series
	2D ndarrays
	A Series
	Another DataFrame
"""
df = pd.DataFrame(data)
del df[column_name]  # remove column
three = df.pop("three")
df["foo"]

```
### Common
```python
# Common
df = pd.DataFrame(mydict)  # create df
df.head()  # view top rows
df.tail()  # view bottom rows
df.dtypes  # column data types
df.index  # row labels
df.columns  # column labels
df.to_numpy()  # df to numpy array without labels
df.describe()  #  statistics summary of data
df.T  # transpose of df
df.sort_values(by=column_name)  # sort rows by specified column
df[column_name]  # get rows of column as Series
df.loc[:, [col1, col2]]  # get df with only specified columns
df.iloc[3]  # get 3rd row
df[df[column_name] > 0]  # boolean indexing
df.dropna(how="any")  # drop rows with missing data
df.fillna(value=5)  # fill rows with missing data
df.mean()  # mean for each column
df = pd.merge(left, right, on=column_name)  # join two dfs
df.groupby(column_name).sum()  # group by
```
### IO
```python
# excel
df = pd.read_excel("path_to_file.xlsx", sheet_name=None, converters={"MyBools": bool})


# csv
import pandas as pd
from io import StringIO
data = "col1,col2,col3\na,b,1\na,b,2\nc,d,3"
pd.read_csv(StringIO(data), usecols=lambda x: x.upper() in ["COL1", "COL3"])


# json
json = df.to_json()
```
### Time Series
Date times: a specific data and time (datetime.datetime)
Time deltas: an absolute time duration (datetime.timedelta)
Time spans: a span of time defined by a point in time and its associated frequency
Date offsets: a relative time duration that respects calendar arithmetic
```python
# date converter
dti = pd.to_datetime(
	["1/1/2018", np.datetime64("2018-01-01"), datetime.datetime(2018, 1, 1)]
)

# sequence of fixed-frequency dates and time spans
dti = pd.date_range("2018-01-01", periods=3, freq="h")

# convert timezone
dti = dti.tz_localize("UTC")
```

### Plotting
```python
import matplotlib.pyplot as plt

np.random.seed(123456)
ts = pd.Series(np.random.randn(1000), index=pd.date_range("1/1/2000", periods=1000))
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index, columns=list("ABCD"))
df = df.cumsum()
plt.figure();
df.plot()  # a wrapper around plt.plot()
```
