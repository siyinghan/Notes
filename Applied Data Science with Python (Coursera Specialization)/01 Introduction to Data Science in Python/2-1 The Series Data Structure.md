# 2-1 The Series Data Structure

The `series` is one of the core data structures in `pandas`. You think of it a cross between a `list` and a `dictionary`. The items are all stored in an order and there's labels with which you can retrieve them.

An easy way to visualize this is two columns of data. The first is the special index, a lot like the dictionary keys. While the second is your actual data. It's important to note that the data column has a label of its own and can be retrieved using the `.name` attribute.

<img src="https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/002.png" alt="001" width="60%"/>

This is different than with dictionaries and is useful when it comes to merging multiple columns of data.

You can create a series by passing in a list of values. When you do this, `Pandas` automatically assigns an index starting with zero and sets the name of the series to None.

Let's see an example of this. First, I'll start off by importing the `pandas` library as `pd`, then let's take a look at the series object.
```python
import pandas as pd
pd.Series?
```

Here you could see the documentation indicates that you can pass in some data, an index and a name. The data can be anything, that's array-like, like a list.

<img src="https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/003.png" alt="001" width="70%"/>
