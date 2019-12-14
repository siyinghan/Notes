# 2-6 Indexing Dataframes

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv), [census.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/census.csv)

<br/>

As we've seen, both `Series` and `DataFrames` can have indices applied to them. The index is essentially a row level label, and we know that rows correspond to axis zero. In our Olympics data, we indexed the data frame by the name of the country. Indices can either be inferred, such as when we create a new series without an index, in which case we get numeric values, or they can be set explicitly, like when we use the dictionary object to create the series, or when we loaded data from the CSV file and specified the header.

Another option for setting an index is to use the `set_index` function. This function takes a list of columns and promotes those columns to an index. Set index is a destructive process, it doesn't keep the current index. If you want to keep the current index, you need to manually create a new column and copy into it values from the index attribute.

Let's go back to our **Olympics** DataFrame:

```python
df.head()
```



<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/022.png' alt='022' width='100%' />

Let's say that we don't want to index the DataFrame by countries, but instead want to index by the number of gold medals that were won at summer games. First we need to preserve the country information into a new column. We can do this using the indexing operator or the string that has the column label. Then we can use the `set_index` to set index of the column to summer gold medal wins

```python
df['country'] = df.index
df = df.set_index('Gold')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/028.png' alt='028' width='100%' />

You'll see that when we create a new index from an existing column it appears that a new first row has been added with empty values. This isn't quite what's happening. And we know this in part because an empty value is actually rendered either as a none or an NaN if the data type of the column is numeric. What's actually happened is that the index has a name. Whatever the column name was in the Jupiter notebook has just provided this in the output.

We can get rid of the index completely by calling the function `reset_index`. This promotes the index into a column and creates a default numbered index:

```python
df = df.reset_index()
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/029.png' alt='029' width='100%' />

<br/>

One nice feature of pandas is that it has the option to do multi-level indexing. This is similar to composite keys in relational database systems. To create a multi-level index, we simply call set index and give it a list of columns that we're interested in promoting to an index. Pandas will search through these in order, finding the distinct data and forming composite indices. A good example of this is often found when dealing with geographical data which is sorted by regions or demographics.

Let's change data sets and look at some census data for a better example. This data is stored in the file **census.csv** and comes from the **United States Census Bureau**:

```python
df = pd.read_csv('census.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/030.png' alt='030' width='100%' />

In particular, this is a breakdown of the population level data at the US county level. It's a great example of how different kinds of data sets might be formatted when you're trying to clean them.

For instance, in this data set there are two summarized levels, one that contains summary data for the whole country. And one that contains summary data for each state, and one that contains summary data for each county. I often find that I want to see a list of all the unique values in a given column. In this DataFrame, we see that the possible values for the sum level are using the `unique` function on the DataFrame. This is similar to the SQL distinct operator. Here we can run unique on the sum level of our current DataFrame and see that there are only two different values, 40 and 50:

```python
df['SUMLEV'].unique()
```

```array([40, 50])```

Let's get rid of all of the rows that are summaries at the state level and just keep the county data:

```python
df=df[df['SUMLEV'] == 50]
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/031.png' alt='031' width='100%' />

Also while this data set is interesting for a number of different reasons, let's reduce the data that we're going to look at to just the total population estimates and the total number of births. We can do this by creating a list of column names that we want to keep then project those and assign the resulting DataFrame to our `df` variable:

```python
columns_to_keep = ['STNAME',
                   'CTYNAME',
                   'BIRTHS2010',
                   'BIRTHS2011',
                   'BIRTHS2012',
                   'BIRTHS2013',
                   'BIRTHS2014',
                   'BIRTHS2015',
                   'POPESTIMATE2010',
                   'POPESTIMATE2011',
                   'POPESTIMATE2012',
                   'POPESTIMATE2013',
                   'POPESTIMATE2014',
                   'POPESTIMATE2015']
df = df[columns_to_keep]
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/032.png' alt='032' width='100%' />

The US Census data breaks down estimates of population data by state and county. We can load the data and set the index to be a combination of the state and county values and see how pandas handles it in a DataFrame. We do this by creating a list of the column identifiers we want to have indexed. And then calling `set_index` with this list and assigning the output as appropriate. We see here that we have a *dual index*, first the state name and then the county name:

```python
df = df.set_index(['STNAME', 'CTYNAME'])
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/033.png' alt='033' width='100%' />

An immediate question which comes up is how we can query this DataFrame. For instance, we saw previously that the `loc` attribute of the DataFrame can take multiple arguments. And it could query both the row and the columns. When you use a MultiIndex, you must provide the arguments in order by the level you wish to query. Inside of the index, each column is called a level and the outermost column is level zero. For instance, if we want to see the population results from Washtenaw County, which is where I live, you'd want to the first argument as the *state of Michigan*:

```python
df.loc['Michigan', 'Washtenaw County']
```

```
BIRTHS2010            977
BIRTHS2011           3826
BIRTHS2012           3780
BIRTHS2013           3662
BIRTHS2014           3683
BIRTHS2015           3709
POPESTIMATE2010    345563
POPESTIMATE2011    349048
POPESTIMATE2012    351213
POPESTIMATE2013    354289
POPESTIMATE2014    357029
POPESTIMATE2015    358880
Name: (Michigan, Washtenaw County), dtype: int64
```

You might be interested in just comparing two counties. For instance, Washtenaw where I live and Wayne County which covers Detroit. To do this, we can pass the `loc` method, a list of tuples which describe the indices we wish to query. Since we have a MultiIndex of two values, the state and the county, we need to provide two values as each element of our filtering list:

```python
df.loc[ [('Michigan', 'Washtenaw County'),
         ('Michigan', 'Wayne County')] ]
```

