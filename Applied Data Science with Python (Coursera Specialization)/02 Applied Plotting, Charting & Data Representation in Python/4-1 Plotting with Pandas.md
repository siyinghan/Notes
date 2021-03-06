# 4-1 Plotting with Pandas

**Material**: [iris.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Material/iris.csv)

<br/>

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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/100.png' alt='100' width='35%' />

Setting the aspect ratio to equal allows the viewer to easily see that the range of series A is much smaller than series C. Using pandas, we can also easily do **box plots**:

```python
df.plot.box();
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/101.png' alt='101' width='55%' />

**Histograms**:

```python
df.plot.hist(alpha=0.7);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/102.png' alt='102' width='55%' />

And **kernel density estimate plots**:

```python
df.plot.kde();
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/103.png' alt='103' width='55%' />

Which are useful for visualizing an estimate of a variable's probability density function. Kernel density estimation plots come in handy in data science application where you want to derive a smooth continuous function from a given sample.

Pandas also has plotting tools that help with visualizing large amounts of data or high dimensional data. Let's explore a couple of these tools by loading in the **iris** flower data set:

```python
iris = pd.read_csv('iris.csv')
iris.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/104.png' alt='104' width='60%' />

The iris data set is a classic multivariate data set, which includes the sepal length, sepal width, petal length, and petal width for hundreds of samples of three species of the iris flower. pandas has a plotting tool that allows us to create a scatter matrix from a DataFrame. A scatter matrix is a way of comparing each column in a DataFrame to every other column in a pairwise fashion. Let's use it to visualize the iris dataframe and see what insights we can gain from our data:

```python
pd.plotting.scatter_matrix(iris);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/105.png' alt='105' width='70%' />

The scatter matrix creates scatter plots between the different variables and histograms along the diagonals. This allows us to quickly see some of the more obvious patterns in the data set. Looking at the scatter plots, it appears that there are some distinct groupings of the points, which might indicate that there could be some clustering going on. And while this looks impressive and is certainly useful, realize that in the last two weeks you have gained all of the skills to manually build these kinds of plots if you want to. This is nothing more than a four by four grid of subplots, with some plots histograms and the others scatterplots.

Let's look at one more plotting tool in pandas which will help us visualize multivariate data. pandas includes a plotting tool for creating **parallel coordinates plots**. Parallel coordinate plots are a common way of visualizing high dimensional multivariate data:

```python
plt.figure()
pd.plotting.parallel_coordinates(iris, 'Name');
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/106.png' alt='106' width='70%' />

Each variable in the data set corresponds to an equally spaced parallel vertical line. The values of each variable are then connected by lines between for each individual observation. Coloring the lines by class, in this example the species of flower, allows the viewer to more easily see any patterns or clustering. For instance, looking at our iris data set, we can see that the petal length and petal width are two variables that split the different species fairly clearly. With iris virginica having the longest and widest petals. And iris setosa having the shortest and narrowest petals. Well that's it for visualization in pandas.