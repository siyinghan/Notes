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

```1.9 s ± 34.4 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)```

```python
%%timeit -n 10
for group, frame in df.groupby('STNAME'):
    avg = np.average(frame['CENSUS2010POP'])
    print('Counties in state ' + group + ' have an average population of ' + str(avg))
```

```52.6 ms ± 5.88 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)```

Now, 99% of the time, you'll use `groupby` on one or more columns. But you can actually provide a function to group by as well and use that to segment your data. This is a bit of a fabricated example but lets say that you have a big batch job with lots of processing and you want to work on only a third or so of the states at a given time. We could create some function which returns a number between zero and two based on the first character of the state name. Then we can tell group by to use this function to split up our data frame. It's important to note that in order to do this you need to set the index of the data frame to be the column that you want to group by first.

Here's an example. We'll create some new function called `fun` and if the first letter of the parameter is a capital M we'll return a 0. If it's a capital Q we'll return a 1 and otherwise we'll return a 2. Then we'll pass this function to the data frame reply, and see that the data frame is segmented by the calculated group number. This kind of technique, which is sort of a light weight hashing, is commonly used to distribute tasks across multiple workers. Whether they are cores in a processor, nodes in a supercomputer, or disks in a database:

```python
df = df.set_index('STNAME')

def fun(item):
    if item[0]<'M':
        return 0
    if item[0]<'Q':
        return 1
    return 2

for group, frame in df.groupby(fun):
    print('There are ' + str(len(frame)) + ' records in group ' + str(group) + ' for processing.')
```

```
There are 1177 records in group 0 for processing.
There are 1134 records in group 1 for processing.
There are 831 records in group 2 for processing.
```

A common work flow with group bias that you split your data, you apply some function, then you combine the results. This is called split apply combine pattern. And we've seen the splitting method, but what about apply? Certainly iterative methods as we've seen can do this, but the groupby object also has a method called `agg` which is short for aggregate. This method applies a function to the column or columns of data in the group, and returns the results. With agg, you simply pass in a dictionary of the column names that you're interested in, and the function that you want to apply. For instance to build a summary data frame for the average populations per state, we could just give `agg` a dictionary with the **CENSUS2010POP** key and the `numpy.average` function:

```python
df = pd.read_csv('census.csv')
df = df[df['SUMLEV']==50]
df.groupby('STNAME').agg({'CENSUS2010POP': np.average}).head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/060.png' alt='060' width='25%' />

Now, I want to flag a potential issue and using the `aggregate` method of `groupby` objects. You see, when you pass in a dictionary it can be used to either to identify the columns to apply a function on or to name an output column if there's multiple functions to be run. The difference depends on the keys that you pass in from the dictionary and how they're named. In short, while much of the documentation and examples will talk about a single groupby object, there's really two different objects. The data frame groupby and the series groupby. And these objects behave a little bit differently with aggregate.

For instance, we take our census data and convert it into a series with the state names as the index and only columns as the census2010population. And then we can group this by index using the level parameter. Then we call the agg method where the dictionary that has both the numpie average and the numpie sum functions. PANDAS applies those functions to the series object and, since there's only one column of data It apples both functions to that column and prints out the output:

```python
print(type(df.groupby(level=0)['POPESTIMATE2010','POPESTIMATE2011']))
print(type(df.groupby(level=0)['POPESTIMATE2010']))
```

```
<class 'pandas.core.groupby.DataFrameGroupBy'>
<class 'pandas.core.groupby.SeriesGroupBy'>
```

```python
(df.set_index('STNAME').groupby(level=0)['CENSUS2010POP']
    .agg({'avg': np.average, 'sum': np.sum})).head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/061.png' alt='061' width='30%' />

We can do the same thing with a data frame instead of a series. We set the index to be the state name, we group by the index, and we project two columns. The population estimate in 2010, the population estimate in 2011. When we call aggregate with two parameters, it builds a nice hierarchical column space and all of our functions are applied:

```python
(df.set_index('STNAME').groupby(level=0)['POPESTIMATE2010','POPESTIMATE2011']
    .agg({'avg': np.average, 'sum': np.sum})).head()
```

