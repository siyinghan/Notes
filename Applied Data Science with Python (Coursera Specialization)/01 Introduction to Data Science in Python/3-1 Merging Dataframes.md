# 3-1 Merging Dataframes

Last week, we were introduced to the pandas data manipulation and analysis library. We saw that there is really *two-core data structures* which are very similar, the *one-dimensional series object* and the *two-dimensional DataFrame object*. Querying these two data structures is done in a few different ways, such as using the `iloc` or `loc` attributes for row-based querying, or using the square brackets on the object itself for column-based querying. Most importantly, we saw that one can query the DataFrame and Series objects through **Boolean masking**. And Boolean masking is a powerful filtering method which allows us to use broadcasting to determine what data should be kept in our analysis.

In this week's lecture, we're going to go into more detail on how to manipulate DataFrame, in particular. We're going to explore how to reduce and process data using `GroupBy` and `Apply`, and how to join data sets from multiple files together into one. We'll also talk about some features that pandas has which are useful for both traditional statistical analyses and machine learning.

Let's start with how to merge data sets. We've already seen how we add new data to an existing DataFrame. We simply use the square bracket operator with the new column name, and the data is added as long as an index is shared. If there is no shared index and a scalar value is passed in, which remember a scalar value is just a single value like an integer or a string. The new value column is added with the scalar value as the default value. What if we wanted to assign a different value for every row? Well, it gets trickier. If we could hardcode the values into a list, then pandas will unpack them and assign them to the rows. But if the list we have isn't long enough, then we can't do this, since Pandas doesn't know where the missing values should go. Here's an example. We used the DataFrame of store purchases from one of our previous lectures, where the index is a list of stores and the columns store purchase data:

```python
import pandas as pd

df = pd.DataFrame([{'Name': 'Chris', 'Item Purchased': 'Sponge', 'Cost': 22.50},
                   {'Name': 'Kevyn', 'Item Purchased': 'Kitty Litter', 'Cost': 2.50},
                   {'Name': 'Filip', 'Item Purchased': 'Spoon', 'Cost': 5.00}],
                  index=['Store 1', 'Store 1', 'Store 2'])
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/040.png' alt='040' width='30%' />

If we want to add some new column called *Date* to the DataFrame, that's fine. We just use the square bracket operator directly on the DataFrame, as long as the column is as long as the rest of the records:

```python
df['Date'] = ['December 1', 'January 1', 'mid-May']
df
```

