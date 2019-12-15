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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/084.png' alt='084' width='65%' />

Interesting, we see it starts at a moderate level, spikes up, then drops off much more gradually and does indeed have a very long tail. Let's add this to our box plot. Curiosity and to demonstrate something called inset axes. Recall that we have one figure with one subplot. Since we didn't do anything fancy with subplots, that means we only have one axes object. We can actually overlay an axes on top of another within a figure. Now, this functionality isn't in the basic matplotlib space, but it's in the toolkits, which tend to ship with matplotlib. There are several different toolkits available, and while they tend to be packaged, they aren't considered core. The toolkit that we're going to use is called the axes grid, and we import it from the `mpl_toolkits.axes_grid1.inset_locator`. We create a new figure and we put up our box plot. Then we just call the inset locator and pass it the current axes object we want composition on top of, followed by the size of our new axis. And we can specify this as both a width and a height in percentage from the parent axes. Then we give it a number from the place in which we wanted to drop the new axes:

```python
import mpl_toolkits.axes_grid1.inset_locator as mpl_il

plt.figure()
plt.boxplot([ df['normal'], df['random'], df['gamma'] ], whis='range')
# overlay axis on top of another 
ax2 = mpl_il.inset_axes(plt.gca(), width='60%', height='40%', loc=2)
ax2.hist(df['gamma'], bins=100)
ax2.margins(x=0.5)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/085.png' alt='085' width='65%' />

This isn't quite as flexible as with grid spec where we're essentially trying to connect the plot to one of ten different locations. I'll put in position two here, which will place the axes in the upper left of the figure. Then we just push a histogram to that axes and it behaves as we would expect. We've a little clash on the yaxis but that's easy enough to flip on the inset plot. We just access the yaxis of the plot and call `tick_right`:

```python
# switch the y axis ticks for ax2 to the right side
ax2.yaxis.tick_right()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/086.png' alt='086' width='65%' />

And there we are. An inset plot showing a distribution as a histogram layered on top of a box plot.

Now, the box plot has a few more functions which are worth investigating before we finish this lecture off. First, if you don't supply the whis argument, the whiskers actually only go out to halfway between the interquartile range. You can figure that out through the top of the box minus the bottom of the box and times that value by 1.5.

This is one method of detecting **outliers**. And the points which are plotted beyond the whiskers are called fliers. You can see how this method of outlier detection differs with respect to our three distributions:

```python
# if `whis` argument isn't passed, boxplot defaults to showing 1.5*interquartile (IQR) whiskers with outliers
plt.figure()
_ = plt.boxplot([ df['normal'], df['random'], df['gamma'] ] )
```

