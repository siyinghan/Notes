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
