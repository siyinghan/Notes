# 4-1 Plotting with Pandas

`pandas` uses `matplotlib` under the hood, and provides some convenient functions for **visualizing data**. Before we dive into visualization in pandas, lets take a look at the matplotlib's style package. Matplotlib comes with a number of predefined styles, which we can choose from, to change the default look of our plots. Because pandas is using matplotlib under the hood, this will change the default style of our pandas graphs as well. We can use `plt.style.available` to see the predefined styles provided:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

%matplotlib notebook
```

```python
# see the pre-defined styles provided.
plt.style.available
```

```
['seaborn-dark',
 'seaborn-darkgrid',
 'seaborn-ticks',
 'fivethirtyeight',
 'seaborn-whitegrid',
 'classic',
 '_classic_test',
 'fast',
 'seaborn-talk',
 'seaborn-dark-palette',
 'seaborn-bright',
 'seaborn-pastel',
 'grayscale',
 'seaborn-notebook',
 'ggplot',
 'seaborn-colorblind',
 'seaborn-muted',
 'seaborn',
 'Solarize_Light2',
 'seaborn-paper',
 'bmh',
 'tableau-colorblind10',
 'seaborn-white',
 'dark_background',
 'seaborn-poster',
 'seaborn-deep']
```

Let's use the **seaborn-colorblind style**, which will change the default colors of our plots to use a color palette that is more color vision deficiency friendly:

```python
# use the 'seaborn-colorblind' style
plt.style.use('seaborn-colorblind')
```

Now, where the built-in visualization of pandas really shines is in helping with fast and easy plotting of series and DataFrames that can help us explore the data.

Let's make a DataFrame. First, we'll set the` seed` for the **random number generator**, which will allow us to reproduce the data. Next, let's add three columns of random time series data. We can generate the random data by cumulatively summing up random numbers. numpi has a great function for this called cumsum, which cumulatively sums an array Let's do this for three columns, A, B and C. And also offset the B column by + 20 and the C column by - 20. Using date_range, we can set the index to be everyday in 2017:

```python
np.random.seed(123)

df = pd.DataFrame({'A': np.random.randn(365).cumsum(0), 
                   'B': np.random.randn(365).cumsum(0) + 20,
                   'C': np.random.randn(365).cumsum(0) - 20}, 
                  index=pd.date_range('1/1/2017', periods=365))
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/096.png' alt='096' width='45%' />

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/094.png' alt='094' width='35%' />