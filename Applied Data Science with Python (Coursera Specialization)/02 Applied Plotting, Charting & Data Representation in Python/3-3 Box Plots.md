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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/081.png' alt='081' width='45%' />

Each row has 10,000 entries. The mean values and standard deviation vary heavily. The minimal and maximum values are showing, and there's three different percentage values. These percentage values make up what's called the **interquartile range**. There are four different quarters of the data. The first is between the minimal value and the first 25% of the data. And this value of 25% is called the first quartile. The second quarter of data is between the 25% mark and the 50% of the data. The third between 50 and 75% of the data. And 75% mark is called the third quartile. And the final piece of data is between the 75% and the maximum of the data. Like standard deviation, the **interquartile range** is a measure of variability of data. And it's common to plot this using a box plot.

In a box plot, the **mean**, or the **median**, of the data is plotted as a straight line. Two boxes are formed, one above, which represents the 50% to 75% data group, and one below, which represents the 25% to 50% data group. Thin lines which are capped are then drawn out to the minimum and maximum values. Here's an example. We'll create a new figure. Then we call plt.boxplot, and we pass in the column that we want to visualize. In matplotlib, data needs to conform to NumPy arrays. But pandas is built on top of NumPy data points, so this is as easy as projecting the column that we're interested in. Finally, we set the whis parameter to be the range. This tells the box plot to set the whisker values all the way out to the minimum and maximum values. Also, I am going to assign the output of the box plot function to a variable, which is just an underscore:

```python
plt.figure()
# create a boxplot of the normal data, assign the output to a variable to supress output
_ = plt.boxplot(df['normal'], whis='range')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/082.png' alt='082' width='65%' />

Now this is either horrendous or beautiful, depending on who you are. You see, *underscore* is actually a legal name for a variable on `Python`. But it's also completely uninformative. It's common practice by some to use an underscore when unpacking values which you don't care about and won't use later. I am using it here because if we don't assign the return value of plotting function to a variable, the Jupiter Notebook will assume that we wanted to print that output. Since plotting functions return a list of all of the artists plotted, this would really muddy up our display. It's up to you whether you want to use this underscore pattern or not in your own code.

Great, this gives us a basic box plot. Now let's add the other two samples to it. Unfortunately we can't just pass a whole pandas data frame to matplotlib. Instead we need to pull out each column and send them in as a list of values:

```python
# clear the current figure
plt.clf()
# plot boxplots for all three of df's columns
_ = plt.boxplot([ df['normal'], df['random'], df['gamma'] ], whis='range')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/083.png' alt='083' width='65%' />

All right, that gives us our **three distributions**. Now, we didn't normalize the scale, so that's a little wonky. But if we look at the gamma distribution, for instance, we see the tail of it is very, very long. So the maximum values are very far out. Let's take a look at this by itself in a histogram:

```python
plt.figure()
_ = plt.hist(df['gamma'], bins=100)
```

