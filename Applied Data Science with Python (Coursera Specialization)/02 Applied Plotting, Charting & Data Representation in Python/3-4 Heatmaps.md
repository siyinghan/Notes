# 3-4 Heatmaps

**Heatmaps** are a way to visualize three-dimensional data and to take advantage of spatial proximity of those dimensions. Now, I honestly didn't think I would include heatmaps in this course. I've seen enough bad heatmaps to last me a lifetime. The problem is heatmaps are really quite powerful when you have the right data. Weather data is a great example. You have two dimensions, latitude and longitude, and then we can overlay on top of this a third dimension, say, temperature or rainfall amounts and use color to indicate its intensity.

Here's another good example.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/088.png' alt='088' width='100%' />

This time from the Australian Transportation Safety Bureau. And actually on the Wikipedia page for Heatmaps, it shows the path of an airline, Malaysian Airlines 370, which went missing in 2014. On top of the flight path is a heatmap showing the probability of the plane if it had crashed. This probability is also displayed as a continuous value, with cool colors, blues, being used for low probabilities and hot or warm colors, reds, being used for high probability. So heatmaps aren't all bad. But where they break down is when there's no continuous relationship between dimensions. Using a heatmap for categorical data, for instance, is just plain wrong. It misleads the viewer into looking for patterns and ordering through spatial proximity. And any such patterns would be purely spurious.

Okay, now you've have the lecture, let's talk about the techniques. In matplotlib, a heatmap is simply a **two-dimensional histogram** where the x and the y values indicate potential points and the color plotted is the frequency of the observation. Earlier, we talked about different statistical distributions and they work well for this demonstration. In fact, let's redo our subplots where we showed a scatter plot and two histograms, one for each dimension.

In that we define Y values to come from the normal distribution and X values to come from a random distribution. To plot this as a two-dimensional histogram, we just pass it to the `hist2d` function:

```python
plt.figure()

Y = np.random.normal(loc=0.0, scale=1.0, size=10000)
X = np.random.random(size=10000)
_ = plt.hist2d(X, Y, bins=25)

plt.colorbar()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/089.png' alt='089' width='65%' />