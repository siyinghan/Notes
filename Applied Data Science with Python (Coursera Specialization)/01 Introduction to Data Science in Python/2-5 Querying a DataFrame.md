# 2-5 Querying a DataFrame

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)

<br/>

**Boolean masking** is the heart of fast and efficient querying in `NumPy`. It's analogous a bit to masking used in other computational areas. A Boolean mask is an array which can be of one dimension like a series, or two dimensions like a data frame, where each of the values in the array are either true or false. This array is essentially overlaid on top of the data structure that we're querying. And any cell aligned with the true value will be admitted into our final result, and any sign aligned with a false value will not. **Boolean masking** is powerful conceptually and is the cornerstone of efficient `NumPy` and `Pandas` querying. This technique is well used in other areas of computer science, for instance, in graphics. But it doesn't really have an analogue in other traditional relational databases, so I think it's worth pointing out here.

Boolean masks are created by applying operators directly to the pandas series or DataFrame objects. For instance, in our Olympics data set, you might be interested in seeing only those countries who have achieved a gold medal at the summer Olympics. To build a Boolean mask for this query, we project the gold column using the indexing operator and apply the greater than operator with a comparison value of zero:

```python
df['Gold'] > 0
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/023.png' alt='023' width='50%' />

This is essentially broadcasting a comparison operator, greater than, with the results being returned as a Boolean series. The resultant series is indexed where the value of each cell is either true or false depending on whether a country has won at least one gold medal, and the index is the country name. 

So this builds us the Boolean mask, which is half the battle. What we want to do next is overlay that mask on the data frame. We can do this using the `where` function. The where function takes a Boolean mask as a condition, applies it to the data frame or series, and returns a new data frame or series of the same shape.

Let's apply this Boolean mask to our **Olympics** data and create a data frame of only those countries who have won a gold at a summer games:

```python
only_gold = df.where(df['Gold'] > 0)
only_gold.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/024.png' alt='024' width='100%' />

We see that the resulting data frame keeps the original indexed values, and only data from countries that met the condition are retained. All of the countries which did not meet the condition have `NaN` data instead. This is okay. Most statistical functions built into the data frame object ignore values of `NaN`.

For instance, if we call the df.count on the only_gold data frame, we see that there are 100 countries which have had gold medals awarded at the summer games, while if we call count on the original data frame, we see that there are 147 countries total:

```python
only_gold['Gold'].count()
```

```100```

```python
df['Gold'].count()
```

```147```

Often we want to drop those rows which have no data. To do this, we can use the `dropna` function. You can optionally provide dropna the axes it should be considering:

```python
only_gold = only_gold.dropna()
only_gold.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/025.png' alt='025' width='100%' />

Remember that the axes is just an indicator for the columns or rows and that the default is zero, which means rows.

<br/>

When you find yourself talking about pandas and saying phrases like, often I want to, it's quite likely the developers have included a shortcut for this common operation. For instance, in this example, we don't actually have to use the `where` function explicitly. The pandas developers allow the indexing operator to take a Boolean mask as a value instead of just a list of column names. The syntax might look a little messy, especially if you're not used to programming languages with overloaded operators, but the result is that you're able to filter and reduce data frames relatively quickly.

Here's a more concise example of how we could query this data frame. You'll notice that there are no NaNs when you query the data frame in this manner. pandas automatically filters out the rows with now values:

```python
only_gold = df[df['Gold'] > 0]
only_gold.head()
```

