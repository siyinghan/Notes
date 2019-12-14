# 4-2 More Distributions

Many of the distributions you use in data science are not discrete binomial, and instead are continues where the value of the given observation isn't a category like heads or tails, but can be represented by a real number. It's common to then graph these distributions when talking about them, where the **x axis is the value of the observation** and the **y axis represents the probability** that a given observation will occur.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/079.png' alt='079' width='60%' />

If all numbers are equally likely to be drawn when you sample from it, this should be graphed as a flat horizontal line. And this flat line is actually called the **uniform distribution**:

```python
np.random.uniform(0, 1)
```

```0.3697821493147051```

There are few other distributions that get a lot more interesting. Let's take the **normal distribution** which is also called **Gaussian Distribution** or sometimes, a **Bell Curve**. This distribution looks like a hump where the number which has the highest probability of being drawn is a zero, and there are two decreasing curves on either side of the X axis. One of the properties of this distribution is that the mean is zero, not the two curves on either side are symmetric.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/080.png' alt='080' width='60%' />

```python
np.random.normal(0.75)
```

```-2.5144533823813173```

I want to introduce you to the term **expected value**. I think that most of us are familiar with the mean is the sum of all the values divided by the total number of values. Calculating a mean values are computational process, and it takes place by looking at samples from distribution. For instance rolling a die three times might give you 1, 2 and 6, the mean value is then 4.5. The **expected value** is the probability from the underlying distribution is what would be the mean of a die roll if we did an infinite number of rolls. The result is 3.5 since each face of the die is equally likely to appear. Thus the expected value is 3.5, while the mean value depends upon the samples that we've taken, and converges to the expected value given a sufficiently large sample set. We'll talk more about expected values in course three.

A second property is that the **variance** of the distribution can be described in a certain way. Variance is a measure of how broadly values of samples are spread out from the mean.

Let's get a little bit more formal about **five different characteristics** of distributions. First, we can talk about the **distribution central tendency**, and the measures we would use for this are `mode`, `median`, or `mean`. This characteristic is really about where the bulk of probability is in the distribution. We can also talk about the **variability** in the distribution. There are a couple of ways we can speak of this. The standard deviation is one, the interquartile range is another. The **standard deviation** is simply a measure of how different each item, in our sample, is from the mean. Here's the formula for **standard deviation**:



 