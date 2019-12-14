# 2-4 DataFrame Indexing and Loading

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

