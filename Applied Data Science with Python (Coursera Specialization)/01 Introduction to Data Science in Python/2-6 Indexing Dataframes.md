# 2-6 Indexing Dataframes

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)

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

