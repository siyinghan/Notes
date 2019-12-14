# 3-3 Group by

**Material**: [census.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/census.csv)

We've seen that even though PANDAS allows us to iterate over every row in a data frame this is generally a slow way to accomplish a given task and it's not very pandorable. For instance, if we wanted to write some code to iterate over all the of the states and generate a list of the average census population numbers. We could do so *using a loop in the `unique` function*.

 Another option is to use the dataframe group by function. This function takes some column name or names and splits the dataframe up into chunks based on those names, it returns a dataframe group by object. Which can be iterated upon, and then returns a tuple where the first item is the group condition, and the second item is the data frame reduced by that grouping. Since it's made up of two values, you can unpack this, and project just the column that you're interested in, to calculate the average. 

Here's some examples of both methods in action. Let's first load the census data, then exclude the state level summarizations, which had a **SUM level** value of 40:

```python
import pandas as pd
import numpy as np
df = pd.read_csv('census.csv')
df = df[df['SUMLEV']==50]
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/059.png' alt='059' width='100%' />

In the first we used the `census.csv` date. We get a list of the unique states. Then for each state we reduce the data frame and calculate the average:

```python
%%timeit -n 10
for state in df['STNAME'].unique():
    avg = np.average(df.where(df['STNAME']==state).dropna()['CENSUS2010POP'])
    print('Counties in state ' + state + ' have an average population of ' + str(avg))
```

