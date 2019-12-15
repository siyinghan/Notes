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

Now let's see what this data looks like a little more visually to plot this data we can use the plot method on the DataFrame:

```python
df.plot(); # add a semi-colon to the end of the plotting call to suppress unwanted output
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/097.png' alt='097' width='55%' />

The plot method on series and DataFrame is just a simple wrapper around plt.plot. So when we call df.plot, we get a line graph of all the columns in the data frame with labels. Notice how the colors are slightly different from the default matplotlib colors because of the style we used. Also, notice this cool Jupyter Notebook trick. If you add a semicolon to the end of the plotting call, this will suppress unwanted output. And this works with regular matplotlib, too. DataFrame.plot allows us to plot a number of different kinds of plots. We can select which plot we want to use by pressing it into the kind parameter. Let's try and create a scatter plot that takes the A and B columns of df:

```python
df.plot('A','B', kind = 'scatter');
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/098.png' alt='098' width='55%' />

We pass in **scatter** to the kind parameter to change the plot type. This is what we'd get if we called plt.plot on the A and B columns with the point marker parameter. Passing scatter into the kind keyword argument changed the plot to a scatterplot. You can also choose the plot kind by using the methods `dataframe.plot.kind` instead of providing the kind keyword argument.

`kind` :
- `'line'` : line plot (default)
- `'bar'` : vertical bar plot
- `'barh'` : horizontal bar plot
- `'hist'` : histogram
- `'box'` : boxplot
- `'kde'` : Kernel Density Estimation plot
- `'density'` : same as 'kde'
- `'area'` : area plot
- `'pie'` : pie plot
- `'scatter'` : scatter plot
- `'hexbin'` : hexbin plot

Now let's try this and create something a little more complex. This time we want to make a scatterplot with points varying in color and size. We'll use `df.plot.scatter`, pass in columns A and C. And set the color C and size S to change based on the value of column B. Finally, we can choose the color palette used by passing a string into the parameter color map. Here, I'll use viridis, which is particularly pleasing to the eye:

```python
# create a scatter plot of columns 'A' and 'C', with changing color (c) and size (s) based on column 'B'
df.plot.scatter('A', 'C', c='B', s=df['B'], colormap='viridis')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/099.png' alt='099' width='55%' />

Here we can see the A and C columns plotted against one another with the size and color changing based on the values of the B column. Because `df.plot.scatter` returns a matplotlib.axes._subplot, we can perform modification on this object just like objects returned by matplotlib plots. For example, let's see what it looks like when we change the aspect ratio of the `AxesSubplot` to equal:

```python
ax = df.plot.scatter('A', 'C', c='B', s=df['B'], colormap='viridis')
ax.set_aspect('equal')
```

