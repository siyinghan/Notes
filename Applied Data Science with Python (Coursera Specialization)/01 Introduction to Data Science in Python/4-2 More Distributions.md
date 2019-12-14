# 4-2 More Distributions

Many of the distributions you use in data science are not discrete binomial, and instead are continues where the value of the given observation isn't a category like heads or tails, but can be represented by a real number. It's common to then graph these distributions when talking about them, where the **x axis is the value of the observation** and the **y axis represents the probability** that a given observation will occur.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/079.png' alt='0789' width='60%' />

If all numbers are equally likely to be drawn when you sample from it, this should be graphed as a flat horizontal line. And this flat line is actually called the **uniform distribution**:

```python
np.random.uniform(0, 1)
```

```0.3697821493147051```

There are few other distributions that get a lot more interesting. Let's take the **normal distribution** which is also called **Gaussian Distribution** or sometimes, a **Bell Curve**. This distribution looks like a hump where the number which has the highest probability of being drawn is a zero, and there are two decreasing curves on either side of the X axis. One of the properties of this distribution is that the mean is zero, not the two curves on either side are symmetric.