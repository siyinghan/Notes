# 4-2 Seaborn

**Material**: [iris.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Material/iris.csv)

<br/>

Hi, everyone. Today, we'll be looking at `Seaborn`, a Python visualization library based on `matplotlib`. `Seaborn` is really just a wraparound matplotlib. It adds styles to make default data visualizations much more visually appealing and makes creation of specific types of complicated plots much simpler. To get us started, I've imported `seaborn` as `sns`:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib notebook
```

Now, let's set the seed for the random number generator. Which lets us reproduce the data. Next, let's make a panda series v1 that's 1000 numbers drawn from a normal distribution with a mean of 0, and a standard deviation of 10. Let's also make a second pandas series, v2, which is 2 times v1, plus 1,000 numbers drawn from a normal distribution with a mean of 60 and standard deviation of 15:

```python
np.random.seed(1234)

v1 = pd.Series(np.random.normal(0,10,1000), name='v1')
v2 = pd.Series(2*v1 + np.random.normal(60,15,1000), name='v2')
```

Now let's see what the histograms of these two variables look like when we plot them side by side. We can set alpha equal to 0.7 so the histograms don't cover one another up. For the bin parameter, instead of integer denoting the number of bins we want we can also pass in a specific sequence using `np.arange` to specify the specific bins we want to use. This is useful for the one when we want to plot two histograms in the same figure to make sure the bin sizes are equivalent for both histograms. We also add labels so we can see which histogram belongs to which variable using a `legend`:

```python
plt.figure()
plt.hist(v1, alpha=0.7, bins=np.arange(-50,150,5), label='v1');
plt.hist(v2, alpha=0.7, bins=np.arange(-50,150,5), label='v2');
plt.legend();
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/107.png' alt='107' width='65%' />

Looking at the histograms we can quickly see that v1 has a lower mean than v2, and that v2 has a larger spread than v1. Even though up to this point we've only used matplotlib for plotting we see that even importing Seaborn has changed the aesthetics of the plot to a different style from the matplotlib default.

Let's visualize these histograms again but in a different way. First, let's pass in both of the series v1 and v2 in a list. And set the histtype to barstacked. Setting normed to True will normalize the histogram to form a probability density. Next, let's create a variable v3, which is the combination of v1 and v2. We'll use v3 to plot a kernel density estimate plot over the stacked histogram:

```python
# plot a kernel density estimation over a stacked barchart
plt.figure()
plt.hist([v1, v2], histtype='barstacked', density=True);
v3 = np.concatenate((v1,v2))
sns.kdeplot(v3);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/108.png' alt='108' width='65%' />

The kernel density estimation plot estimates the probability density function of the variable v3. Plotting it on top of the stacked histograms of v1 and v2 allows us to see the relationship between these two visualizations.

`Seaborn` provides a convenient function for these type of plots `sns.distplot`. Let's take a look at how it works. We can pass in the variable we want to visualize along with keyword arguments for each of the individual components of the plot. Let's set the histogram color to **teal** and the KDE color to **navy**. Now let's look at an example of one of the types of complex plots that Seborn provides a convenient interface for, the **joint plot**:

```python
plt.figure()
# we can pass keyword arguments for each individual component of the plot
sns.distplot(v3, hist_kws={'color': 'Teal'}, kde_kws={'color': 'Navy'});
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/109.png' alt='109' width='65%' />

The jointplot creates a scatterplot along the histograms for each individual variable on each axis. You've actually seen jointplots in module two and created them manually yourself. To create a jointplot, we just type `sns.jointplot` and pass in the two series, v1 and v2. Setting alpha to 0.4 will help with visualizing overlapping points:

```python
sns.jointplot(v1, v2, alpha=0.4);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/110.png' alt='110' width='65%' />

The jointplot allows us to visualize the distribution of the two variables individually. As well as relationships between the variables. Using `jointplot` we can see that v1 and v2 appear to be normally distributed variables that are positively correlated. Because Seaborn uses matplotlib we can tweak the plots using Matplotlib's tools. Some of the plotting functions in Seaborn return a matplotlib axis object. While others operate on an entire figure and produce plots with several panels, returning a `Seaborn` grid object. In both cases, `matplotlib` can be used to further tweak the plots. For example, `sns.jointplot` returns a `Seaborn` grid object. From this we can plot a map plot axis subplot object using `grid.ax_joint`. Then, we can set the aspect ratio to be equal, using `set_aspect` equal:

```python
grid = sns.jointplot(v1, v2, alpha=0.4);
grid.ax_joint.set_aspect('equal')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/111.png' alt='111' width='65%' />

**Hexbin plots** are the bivariate counterpart to histograms. Hexbin plots show the number of observations that fall within hexagonal bins. `sns.jointplot` includes the **hexbin** style we can use by passing in hex to the `kind` parameter:

```python
sns.jointplot(v1, v2, kind='hex');
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/112.png' alt='112' width='65%' />

The hexbin style of plot works well with relatively large data sets. Another good option for visualizing the distribution of data sets is **kernel density estimations** or **KDE plots**. You can think of two dimensional KDE plots as the continuous version of the hexbin jointplot. First, let's tell Seaborn to use a different style using `sns.set_style('white')`. All of the following charts will have the gray grid turned off. Now we'll create a joint plot just like before, except this time, let's set the kind to **kde**. Finally, let's space to 0, which will plot the marginal distributions directly on the border of the scatter plot:

```python
# set the seaborn style for all the following plots
sns.set_style('white')

sns.jointplot(v1, v2, kind='kde', space=0);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/113.png' alt='113' width='65%' />

We can see that `Seaborn` has some built-in options for easy customization. And provides us with easy to create and beautiful plots for exploring the distributions of your data. For the last part of this tutorial, let's load in the iris dataset, to see how `Seaborn` handles visualizations of categorical data:

```python
iris = pd.read_csv('iris.csv')
iris.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/104.png' alt='104' width='60%' />

Similar to pandas, Seaborn has a built in function that creates a scatterplot matrix. We pass in the iris data of frame. Tell it to map name to different colors using the `hue` parameter. And tell it to use a `kde` along the diagonals instead of the default histograms:

```python
sns.pairplot(iris, hue='Name', diag_kind='kde', size=2);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/114.png' alt='114' width='100%' />

Looking at the pair plot, it's clear there are some clusters in the data set. It looks like peddle length and peddle width are good options for separating the observations, whereas width is not a strong separator. Using pair plot to look at your data frame can be a very useful tool in exploratory data analysis.

One final plot I'd like to show you is called the **violin plot**. You can think of a violin plot as a more informative version of a box plot. To demonstrate, let's plot a violin plot next to a swarm plot, which you can think of as a scatter plot for categorical data. First let's create a new figure and a subplot. Next, we'll create the **swarmplot**, passing in Name and PetalLength, and the data, which is the iris data frame. For the next subplot, we'll create the violinplot, again passing in Name, PetalLength and the iris data frame:

```python
plt.figure(figsize=(8,6))
plt.subplot(121)
sns.swarmplot('Name', 'PetalLength', data=iris);
plt.subplot(122)
sns.violinplot('Name', 'PetalLength', data=iris);
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/115.png' alt='115' width='90%' />

Looking at the swarmplot, each species has its own column and each observation's petal length is shown. With more common values appearing as the wide parts of the cluster, much like a histogram. The **violinplot** is like box plot with a rotated kernel density estimation on each side. Violin plots convey more information than box plots and are able to show particular phenomena within the distribution that box plots are unable to convey such as multi modality.

`Seaborn` is a library that not only adds new styles and visual aspects. But also introduces new functionality such as **joint plots**, scatter **matrix plots**, and **violin plots**. `Seaborn` is being actively developed, and is easy to install, which makes it an indispensible part of a data scientist's toolkit. But keep in mind, this is functionality built on top of matplotlib, and these are largely matplotlib artists being used. So, if you have any ideas for a new statistical visualization, or you've read about one in a publication or journal. You should have the ability to create your own visualization toolkits.