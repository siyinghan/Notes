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
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/009.png' alt='009' width='30%' />



















