# 2-4 DataFrame Indexing and Loading

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)

<br/>

The common work flow is to read your data into a DataFrame then reduce this DataFrame to the particular columns or rows that you're interested in working with. As you've seen, the Panda's toolkit tries to give you views on a `DataFrame`. This is much faster than copying data and much more memory efficient too. But it does mean that if you're manipulating the data you have to be aware that any changes to the DataFrame you're working on may have an impact on the base data frame you used originally.

Here's an example using our same purchasing DataFrame from earlier. We can create a series based on just the cost category using the square brackets `[]`:

```python
costs = df['Cost']
costs
```

```
Store 1    22.5
Store 1     2.5
Store 2     5.0
Name: Cost, dtype: float64
```

Then we can increase the cost in this series using broadcasting:

```python
costs+=2
costs
```

```
Store 1    24.5
Store 1     4.5
Store 2     7.0
Name: Cost, dtype: float64
```

Now if we look at our original DataFrame, we see those costs have risen as well:

```python
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/017.png' alt='017' width='36%' />

This is an important consideration to watch out for. If you want to explicitly use a copy, then you should consider calling the `copy` method on the DataFrame for it first.

<br/>

In this course, we'll be largely using smaller, moderate-sized datasets. As I mentioned, a common workflow is to read the dataset in, usually from some external file. We saw previously how you can do this using Python, and lists, and dictionaries. You can imagine how you might use those dictionaries to create a Pandas DataFrame. Thankfully, Pandas has built-in support for delimited files such as CSV files as well as a variety of other data formats including relational databases, Excel, and HTML tables. I've saved a CSV file called **olympics.csv**, which has data from Wikipedia that contains a summary list of the medal various countries have won at the Olympics.

We can take a look at this file using the shell command cat. Which we can invoke directly using the exclamation point:

```python
!cat olympics.csv
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/018.png' alt='018' width='70%' />

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/017.png' alt='017' width='36%' />