# 2-3 The DataFrame Data Structure

The DataFrame data structure is the heart of the Panda's library. It's a primary object that you'll be working with in *data analysis* and *cleaning tasks*. The DataFrame is conceptually a two-dimensional series object, where there's an index and multiple columns of content, with each column having a label.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/006.png' alt='006' width='65%' />

In fact, the distinction between a column and a row is really only a conceptual distinction. And you can think of the DataFrame itself as simply a two-axes labeled array.

You can create a DataFrame in many different ways, some of which you might expect. For instance, you can use a group of series, where each series represents a row of data. Or you could use a group of dictionaries, where each dictionary represents a row of data.

Let's take a look at an example. I'm going to create three purchase order records as series objects for a sort of fictional store. Each series has a name of a customer, the string which describes the item being purchased, and the cost of the items. Then we'll feed this into the `DataFrame` as the first argument and set index values indicating which store where each purchase was done:
```python
import pandas as pd
purchase_1 = pd.Series({'Name': 'Chris',
                        'Item Purchased': 'Dog Food',
                        'Cost': 22.50})
purchase_2 = pd.Series({'Name': 'Kevyn',
                        'Item Purchased': 'Kitty Litter',
                        'Cost': 2.50})
purchase_3 = pd.Series({'Name': 'Vinod',
                        'Item Purchased': 'Bird Seed',
                        'Cost': 5.00})
df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])
df.head()
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/007.png' alt='007' width='30%' />

You'll see that when we print out a `DataFrame`, the Jupiter notebook's trying to pretty it up a bit, and print it out as a table, which is nice.

<br/>

Similar to the series, we can extract data using the `iloc` and `loc` attributes. Because the `DataFrame` is two-dimensional, passing a single value to the lock indexing operator will return series if there's only one row to return. In this example, if we wanted to select data associated with **Store 2**, we would just query the `loc` attribute with one parameter:
```python
df.loc['Store 2']
```
```
Cost                      5
Item Purchased    Bird Seed
Name                  Vinod
Name: Store 2, dtype: object
type(df.loc['Store 2'])
```

You'll note that the name of the series is returned as the row index value, while the column name is included in the output as well. We can check the data type of the return using the python type function:
```python
type(df.loc['Store 2'])
```
```pandas.core.series.Series```

<br/>

It's important to remember that the indices and column names along either axes, horizontal or vertical, could be non-unique. For instance, in this example, we see two purchase records for **Store 1** as different rows. If we use a single value with the `DataFrame` `loc` attribute, multiple rows of the DataFrame will return, not as a new series, but as a new DataFrame. For instance, if we query for **Store 1** records, we see that Chris and Kevin both shop at the same pets supply store.
```python
df.loc['Store 1']
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/008.png' alt='008' width='30%' />

One of the powers of the Panda's DataFrame is that you can quickly select data based on multiple axes. For instance, if you wanted to just list the costs for **Store 1**, you would supply two parameters to `.loc`, one being the row index and the other being the column name. If we're only interested in **Store 1** costs, we could write this as `df.loc['Store 1', 'Cost']`:
```python
df.loc['Store 1', 'Cost']
```
```
Store 1    22.5
Store 1     2.5
Name: Cost, dtype: float64
```

What if we just wanted to do column selection and just get a list of all of the costs? Well, there's a couple of options. First, you can get a transpose of the DataFrame, using the capital `T` attribute, which swaps all of the columns and rows:
```python
df.T
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/009.png' alt='009' width='35%' />

This essentially turns your column names into indices. And we can then use the `.loc` method. This works, but it's pretty ugly:
```python
df.T.loc['Cost']
```
```
Store 1    22.5
Store 1     2.5
Store 2       5
Name: Cost, dtype: object
```

Since `iloc` and `loc` are used for row selection, the Panda's developers reserved indexing operator directly on the `DataFrame` for column selection. In a Panda's DataFrame, columns always have a name. So this selection is always label based, not as confusing as it was when using the square bracket operator on the series objects. For those familiar with relational databases, this operator is analogous to column projection:
```python
df['Cost']
```
```
Store 1    22.5
Store 1     2.5
Store 2     5.0
Name: Cost, dtype: float64
```

<br/>

Finally, since the result of using the indexing operators, the DataFrame or series, you can chain operations together. For instance, we could have rewritten the query for all Store 1 costs as `df.loc['Store 1']['Cost']`:
```python
df.loc['Store 1']['Cost']
```
```
Store 1    22.5
Store 1     2.5
Name: Cost, dtype: float64
```
This looks pretty reasonable and gets us the result we wanted.

But chaining can come with some costs and is best avoided if you can use another approach. In particular, chaining tends to cause Pandas to return a copy of the DataFrame instead of a view on the DataFrame. For selecting a data, this is not a big deal, though it might be slower than necessary. If you are changing data though, this is an important distinction and can be a source of error.

Here's another method. As we saw, `.loc` does row selection, and it can take two parameters, the row index and the list of column names. `.loc` also supports slicing. If we wanted to select all rows, we can use a column to indicate a full slice from beginning to end. And then add the column name as the second parameter as a string. In fact, if we wanted to include multiply columns, we could do so in a list. And Pandas will bring back only the columns we have asked for.

Here's an example, where we ask for all of the name and cost values for all stores using the `.loc` operator:
```python
df.loc[:,['Name', 'Cost']]
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/010.png' alt='010' width='16.5%' />

So that's selecting and projecting data from a DataFrame based on row and column labels. The key concepts to remember are that the rows and columns are really just for our benefit. Underneath this is just a two axes labeled array, and transposing the columns is easy. Also, consider the issue of chaining carefully, and try to avoid it, it can cause unpredictable results. Where your intent was to obtain a view of the data, but instead Pandas returns to you a copy. In the Panda's world, friends don't let friends chain calls. So if you see it, point it out, and share a less ambiguous solution.

<br/>

Now, before we leave the discussion of accessing data in DataFrames, let's talk about dropping data. It's easy to delete data in series and DataFrames, and we can use the `drop` function to do so. This function takes a single parameter, which is the index or roll label, to drop:
```python
df.drop('Store 1')
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/011.png' alt='011' width='29%' />

This is another tricky place for new users to pad this. The `drop` function doesn't change the DataFrame by default. And instead, returns to you a copy of the DataFrame with the given rows removed. We can see that our original DataFrame is still intact:
```python
df
```
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/012.png' alt='012' width='29%' />

Let's make a copy with the copy method and do a drop on it instead:

```python
copy_df = df.copy()
copy_df = copy_df.drop('Store 1')
copy_df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/013.png' alt='013' width='29%' />

This is a very typical pattern in Pandas, where in place changes to a DataFrame are only done if need be, usually on changes involving indices. So it's important to be aware of.

Drop has two interesting optional parameters. The first is called **inplace**, and if it's set to true, the DataFrame will be updated in place, instead of a copy being returned. The second parameter is the **axes**, which should be dropped. By default, this value is 0, indicating the row axes. But you could change it to 1 if you want to drop a column:

```python
copy_df.drop?
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/014.png' alt='014' width='80%' />

There is a second way to drop a column, however. And that's directly through the use of the indexing operator, using the `del` keyword.

```python 
del copy_df['Name']
copy_df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/015.png' alt='015' width='25%' />

This way of dropping data, however, takes immediate effect on the DataFrame and does not return a view.

<br/>

Finally, adding a new column to the DataFrame is as easy as assigning it to some value. For instance, if we wanted to add a new location as a column with default value of none, we could do so by using the assignment operator after the square brackets:

```python
df['Location'] = None
df
```
































