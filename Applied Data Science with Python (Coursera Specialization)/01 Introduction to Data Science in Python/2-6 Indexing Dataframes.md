# 2-6 Indexing Dataframes

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)
[census.csv]([https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/census.csv](https://github.com/siyinghan/Notes/blob/master/Applied Data Science with Python (Coursera Specialization)/01 Introduction to Data Science in Python/Material/census.csv))

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

