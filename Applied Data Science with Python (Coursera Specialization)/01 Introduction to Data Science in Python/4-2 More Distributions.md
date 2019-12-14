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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/081.png' alt='081' width='20%' />

 

It might look a little more intimidating than it actually is. Let's just walk through how we would write this up. Let's draw 1,000 samples from a normal distribution with an *expected value of 0.75* and a *standard deviation* of 1. Then we calculate the actual mean using NumPy's mean feature. The part inside the summation says xi- x bar. Xi is the current item in the list and x bar is the mean. So we calculate the difference, then we square the result, then we sum all of these:

```python
distribution = np.random.normal(0.75,size=1000)

np.sqrt(np.sum((np.mean(distribution)-distribution)**2)/len(distribution))
```

```0.98604288862247846```

This might be a reasonable place to use a map and apply a lambda to calculate the differences between the mean and the measured value. Then to convert this back to a list, so `NumPy` can use it.

Now we just have to *square each value*, *sum them together*, and *take the square root*. So that's the size of our standard deviation. It covers roughly 68% of the area around the mean, split evenly around the side of the mean. Now we don't normally have to do all this work ourselves, but I wanted to show you how you can sample from the distribution, create a precise programmatic description of a formula, and apply it to your data. But for standard deviation, which is just one particular measure of variability, `NumPy` has a built-in function that you can apply, called `std`:

```python
np.std(distribution)
```

```0.98604288862247846```

There's a couple more measures of distribution that are interesting to talk about. One of these is the shape of the tales of the distribution and this is called the **kurtosis**. We can measure the kurtosis using the statistics functions in the `SciPy` package:

```python
import scipy.stats as stats
stats.kurtosis(distribution)
```

```0.1385017635908934```

A negative value means the curve is slightly more flat than a normal distribution, and a positive value means the curve is slightly more peaky than a normal distribution. Remember that we aren't measuring the kurtosis of the distribution per se, but of the thousand values which we sampled out of the distribution. This is a subtle but important distinction.

We could also move out of the normal distributions and push the peak of the curve one way or the other. And this is called the `skew`:

```python
stats.skew(distribution)
```

```0.016351268208579166```

<br/>

If we test our current sample data, we see that there isn't much of a skew. Let's switch distributions and take a look at a distribution called the **Chi Squared distribution**, which is also quite commonly used in statistic.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/082.png' alt='082' width='60%' />

The Chi Squared Distribution has only one parameter called the **degrees of freedom**. The degrees of freedom is closely related to the number of samples that you take from a normal population. It's important for **significance testing**. But what I would like you to observe, is that as the degrees of freedom increases, the shape of the Chi Squared distribution changes. In particular, the skew to the left begins to move towards the center.

We can observe this through simulation. First we'll sample 1,000 values from a Chi Squared distribution with **degrees of freedom** 2:

```python
chi_squared_df2 = np.random.chisquare(2, size=10000)
stats.skew(chi_squared_df2)
```

```2.005342690090858```

Now we can see that the skew is quite large. Now if we re-sample changing **degrees of freedom** to 5:

```python
chi_squared_df5 = np.random.chisquare(5, size=10000)
stats.skew(chi_squared_df5)
```

```1.2630838950584582```

I'm not going to talk much about the library we're using here for plotting, because that's the topic of the next course. But you can see a histogram with our plot with the two degrees of freedom is skewed much further to the left, while our plot with the five degrees of freedom is not as highly skewed:

```python
%matplotlib inline
import matplotlib
import matplotlib.pyplot as plt

output = plt.hist([chi_squared_df2,chi_squared_df5], bins=50, histtype='step', 
                  label=['2 degrees of freedom','5 degrees of freedom'])
plt.legend(loc='upper right')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/083.png' alt='083' width='55%' />

I could encourage you as always to play with this notebook and change the parameters and see how the degrees of freedom changes the skew of the distribution.

<br/>

The last aspect of distributions that I want to talk about is the **modality**. So far, all of the distributions I've shown have a single high point, a peak. But what if we have multiple peaks? This distribution has two high points, so we call it bimodal.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/084.png' alt='084' width='60%' />

Well, this has been a long lecture but I think it can be tough to chop up a discussion of distributions and still get the main points across. Remember that a distribution is just a shape that describes the probability of a value being pulled when we sample a population. And `NumPy` and `SciPy` each have a number of different distributions built in for us to be able to sample from. The last point I want to leave you with here is a reference. If you find this way of exploring statistics interesting. Alan Downey wrote a nice book called **Think Stats** by the publisher O'Reilly.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/085.png' alt='085' width='60%' />

I think he does a really nice job of teaching how to think about statistics from a programming perspective. One where you write the functions behind the statistical methods. It's not really a reference book, but it's an interesting way to approach learning the fundamentals of statistics. Allen even has a free copy of this book available on his website in PDF format and, of course, all of the code is done in Python.