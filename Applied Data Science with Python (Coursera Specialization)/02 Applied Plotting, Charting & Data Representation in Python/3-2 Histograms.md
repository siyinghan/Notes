# 3-2 Histograms

A histogram is a bar chart which shows the frequency of a given phenomena. A great example are probability distributions. For instance, in the first course in this specialization, we touched on the difference between the random, uniform, normal, and chi squared distributions. Probability function can be visualized as a curve, where the y-axis holds the probability a given value would occur, and the x-axis is the value itself. This is called a probability density function. The y-axis values are limited to between zero and one, where zero means there's no chance of a given value occurring and one means that the value will always occur. The x-axis values are labeled in terms of the distribution function. In the case of the normal distribution, this is usually in terms of standard deviations. So a histogram is just a bar chart where the x-axis is a given observation and the y-axis is the frequency with which that observation occurs. So we should be able to plot a given probability distribution by sampling from it. Now, recall that sampling means that we just pick a number out of the distribution, like rolling a die or pulling a single card out of a deck. As we do this over and over again, we get a more accurate description of the distribution.

Let's pull some samples from the normal distribution and plot four different histograms as subplots. First I'll create our 2 x 2 grade of axis objects. In this case, we don't want to share the y-axis between the plots since we're intentionally looking at a number of different sizes of samples. We're mostly interested in how uniform the distribution looks. Then we can iterate through a list of four different values, 10, 100, 1,000 and 10,000. And we'll pull samples from the NumPy. Remember that the normal function of random just creates a list of numbers based on the underlying normal distribution. We can then plot these to a given axis object using the hist function. And set the title as appropriate:

```python
# create 2x2 grid of axis subplots
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, sharex=True)
axs = [ax1,ax2,ax3,ax4]

# draw n = 10, 100, 1000, and 10000 samples from the normal distribution and plot corresponding histograms
for n in range(0,len(axs)):
    sample_size = 10**(n+1)
    sample = np.random.normal(loc=0.0, scale=1.0, size=sample_size)
    axs[n].hist(sample)
    axs[n].set_title('n={}'.format(sample_size))
```

