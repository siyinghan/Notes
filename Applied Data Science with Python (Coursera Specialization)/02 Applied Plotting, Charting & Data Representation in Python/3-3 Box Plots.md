# 3-3 Box Plots

A **box plot**. Sometimes called a **box-and-whisker plot** is a method of showing aggregate statistics of various samples in a concise matter. The box plot simultaneously shows, for each sample, the median of each value, the minimum and maximum of the samples, and the interquartile range. Let's create three different samplings from `NumPy`. One for the **normal distribution**. One for **random**. And one from a **gamma distribution**. Next, let's put those in a `pandas` `DataFrame`. After all, much of the data we would actually process would come from pandas or another data manipulation toolkit and not from `NumPy` distribution functions:

```python
import pandas as pd
normal_sample = np.random.normal(loc=0.0, scale=1.0, size=10000)
random_sample = np.random.random(size=10000)
gamma_sample = np.random.gamma(2, size=10000)

df = pd.DataFrame({'normal': normal_sample, 
                   'random': random_sample, 
                   'gamma': gamma_sample})
```

Now we can use the `pandas.describe` function to see some summary statistics about our data frame:

```python
df.describe()
```

