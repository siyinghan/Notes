# 3-2 Pandas Idioms

**Material**: [census.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/census.csv)

<br/>

Python programmers will often suggest that there many ways the language can be used to solve a particular problem. But that some are more appropriate than others. The best solutions are celebrated as *Idiomatic Python* and there are lots of great examples of this on stack overflow and websites. An idiomatic solution is often one which has both high performance and high readability. This isn't necessarily true. A sort of sub-language within Python, Pandas has its own set of idioms. We've alluded to some of these already, such as using vectorization whenever possible, and not using iterative loops if you don't need to. Several developers and users within the Panda's community have used the term *pandorable* for these idioms. I think it's a great term. So, I wanted to share with you a couple of key features of how you can make your code pandorable.

The first of these is called *method chaining*. Now we saw that previously, you could chain pandas calls together when you're querying DataFrames. For, instance if you wanted to select rows based on index like county name. Then you wanted to only project certain columns like the total population, you can write a query, like `df.loc['Washtenaw']['Total Population']` This is a form of chaining, called *chain indexing*:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/053.png' alt='053' width='70%' />

And it's generally a bad practice. Because it's possible that pandas could be returning a copy or a view of the DataFrame depending upon the underlying `NumPy` library. In his descriptions of idiomatic Pandas patterns developer Tom Osberger described a rule of thumb for this. If you see back to back square brackets, then you should think carefully if you want to be doing chain indexing. I think this is great as a sort of code smell or anti pattern.

Method chaining though, little bit different. The general idea behind method chaining is that every method on an object returns a reference to that object. The beauty of this is that you can condense many different operations on a DataFrame, for instance, into one line or at least one statement of code:

```python
import pandas as pd
df = pd.read_csv('census.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/054.png' alt='054' width='100%' />

Here's an example of two pieces of code in pandas using our census data. The first is the *pandorable* way to write the code with *method chaining*. In this code, there's no `inplace` flag being used and you can see that when we first run a `where` query, then a `dropna`, then a `set_index`, and then a `rename`:

```python
(df.where(df['SUMLEV']==50)
    .dropna()
    .set_index(['STNAME','CTYNAME'])
    .rename(columns={'ESTIMATESBASE2010': 'Estimates Base 2010'}))
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/055.png' alt='055' width='100%' />

You might wonder why the whole statement is enclosed in parentheses and that's just to make the statement more readable. In Python, if you begin with an open parentheses, you can span a statement over multiple lines and things read a little bit nicer.

The second example is a more traditional way of writing code. There's nothing wrong with this code in the functional sense, you might even be able to understand it better as a new person to the language. It's just not as *pandorable* as the first example:

```python
df = df[df['SUMLEV']==50]
df.set_index(['STNAME','CTYNAME'], inplace=True)
df.rename(columns={'ESTIMATESBASE2010': 'Estimates Base 2010'})
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/056.png' alt='056' width='100%' />

Now, the key with any good idiom is to understand when it isn't helping you. In this case, you can actually time both methods and see that the latter method is faster. So, this is a particular example of a classic time readability trade off. You'll see lots of examples on stock overflow and in documentation of people using method chaining in their pandas. And so, I think being able to read and understand the syntax is really worth your time.

Here's another pandas idiom. Python has a wonderful function called `map`, which is sort of a basis for functional programming in the language. When you want to use map in Python, you pass it some function you want called, and some iterable, like *a list*, that you want the function to be applied to. The results are that the function is called against each item in the list, and there's a resulting list of all of the evaluations of that function. Python has a similar function called `applymap`. In `applymap`, you provide some function which should operate on each cell of a DataFrame, and the return set is itself a DataFrame. Now I think applymap is fine, but I actually rarely use it. Instead, I find myself often wanting to map across all of the rows in a DataFrame. And pandas has a function that I use heavily there, called `apply`. Let's look at an example.

Let's take our census DataFrame. In this DataFrame, we have five columns for population estimates. Each column corresponding with one year of estimates. It's quite reasonable to want to create some new columns for minimum or maximum values, and the `apply` function is an easy way to do this. First, we need to write a function which takes in a particular row of data, finds a minimum and maximum values, and returns a new row of data. We'll call this function `min_max`, this is pretty straight forward. We can create some small slice of a row by projecting the population columns. Then use the `NumPy` `min` and `max` functions, and create a new series with a label values represent the new values we want to apply:

```python
import numpy as np
def min_max(row):
    data = row[['POPESTIMATE2010',
                'POPESTIMATE2011',
                'POPESTIMATE2012',
                'POPESTIMATE2013',
                'POPESTIMATE2014',
                'POPESTIMATE2015']]
    return pd.Series({'min': np.min(data), 'max': np.max(data)})
```

Then we just need to call `apply` on the DataFrame. Apply takes the function and the axis on which to operate as parameters. Now, we have to be a bit careful, we've talked about axis zero being the rows of the DataFrame in the past. But this parameter is really the parameter of the index to use. So, to apply across all rows, you pass axis equal to one:

```python
df.apply(min_max, axis=1).head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/057.png' alt='057' width='40%' />

Of course there's no need to limit yourself to returning a new series object. If you're doing this as part of data cleaning your likely to find yourself wanting to add new data to the existing DataFrame. In that case you just take the row values and add in new columns indicating the max and minimum scores. This is a regular part of my workflow when bringing in data and building summary or descriptive statistics. And is often used heavily with the merging of DataFrames:

```python
import numpy as np
def min_max(row):
    data = row[['POPESTIMATE2010',
                'POPESTIMATE2011',
                'POPESTIMATE2012',
                'POPESTIMATE2013',
                'POPESTIMATE2014',
                'POPESTIMATE2015']]
    row['max'] = np.max(data)
    row['min'] = np.min(data)
    return row
df.apply(min_max, axis=1)
```

