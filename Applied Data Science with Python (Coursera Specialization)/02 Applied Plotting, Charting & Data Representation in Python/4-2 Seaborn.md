# 4-2 Seaborn

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

