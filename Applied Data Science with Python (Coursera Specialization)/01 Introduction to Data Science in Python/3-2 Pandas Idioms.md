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
df
```

