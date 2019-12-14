# 2-2 Querying a Series

A `panda.Series` can be queried, either by the index position or the index label. As we saw, if you don't give an index to the series, the position and the label are effectively the same values. To query by numeric location, starting at zero, use the iloc attribute. To query by the index label, you can use the `loc` attribute.

Here's an example using national sporting event data from Wikipedia. Let's say we want to have a list of all of the sports in our index and a list of countries as values. You might keep these in a dictionary and create a series as we discussed:
```python
sports = {'Archery': 'Bhutan',
          'Golf': 'Scotland',
          'Sumo': 'Japan',
          'Taekwondo': 'South Korea'}
s = pd.Series(sports)
s
```
```
Archery           Bhutan
Golf            Scotland
Sumo               Japan
Taekwondo    South Korea
dtype: object
```

If you wanted to see the fourth country on this, we would use the `iloc` attribute with the parameter 3:
```python
s.iloc[3]
```
```'South Korea'```

If you wanted to see which country has golf as its national sport, we would use the `loc` attribute with parameter **Golf**:
```python
s.loc['Golf']
```
```'Scotland'```

Keep in mind that `iloc` and `loc` are not methods, they are attributes. So you don't use **parentheses** `()` to query them, but **square brackets** `[]` instead, which we'll call the indexing operator. Though in Python, this calls get and set an item methods depending on the context of its use.


Pandas tries to make our code a bit more readable and provides a sort of smart syntax using the indexing operator directly on the series itself. For instance, if you pass in an integer parameter, the operator will behave as if you want it to query via the `iloc` attribute. If you pass in an object, it will query as if you wanted to use the label based `loc` attribute:

```python
s[3]
```
```'South Korea'```
```python
s['Golf']
```
```'Scotland'```

<br/>

So what happens if your index is a list of integers? This is a bit complicated, and `pandas` can't determine automatically whether you're intending to query by index position or index label. So you need to be careful when using the indexing operator on the series itself. And the safer option is to be more explicit and use the `iloc` or `loc` attributes directly. 

Here's an example using some new sports data, where countries are indexed by integer:
```python
sports = {99: 'Bhutan',
          100: 'Scotland',
          101: 'Japan',
          102: 'South Korea'}
s = pd.Series(sports)
s
```
```
99          Bhutan
100       Scotland
101          Japan
102    South Korea
dtype: object
```

If we try and call s sub zero, we get a key error, because there's no item in the sports list with an index of zero:
```python
s[0] #This won't call s.iloc[0] as one might expect, it generates an error instead
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/005.png' alt='005' width='90%' />

Instead we have to call `iloc` explicitly if we want the first item.

<br/>

Okay, so now we know how to get data out of the series. Let's talk about working with the data. A common task is to want to consider all of the values inside of a series and want to do some sort of operation. This could be trying to find a certain number, summarizing data or transforming the data in some way. A typical programmatic approach to this would be to iterate over all the items in the series, and invoke the operation one is interested in.

For instance, we could create a data frame of floating point values. Let's think of these as prices for different products. We could write a little routine which iterates over all of the items in the series and adds them together to get a total:
```python
s = pd.Series([100.00, 120.00, 101.00, 3.00])
s
```
```
0    100.0
1    120.0
2    101.0
3      3.0
dtype: float64
```
```python
total = 0
for item in s:
    total+=item
print(total)
```
```324.0```

This works, but it's slow. Modern computers can do many tasks simultaneously, especially, but not only, tasks involving mathematics. `pandas` and the underlying `numpy` libraries support a method of computation called vectorization. Vectorization works with most of the functions in the NumPy library, including the `sum` function.

Here's how we would really write the code using the `numpy` `sum` method. First we need to import the `numpy` module, and then we just call `np.sum` and pass in an iterable item. In this case, our panda series:
```python
import numpy as np

total = np.sum(s)
print(total)
```
```324.0```

Now both of these methods create the same value, but is one actually faster? The Jupyter Notebook has a magic function which can help. First, let's create a big series of random numbers. You'll see this used a lot when demonstrating techniques with Pandas. Note that I've just used the `head` method, which reduces the amount of data printed out by the series to the first five elements:
```python
#this creates a big series of random numbers
s = pd.Series(np.random.randint(0,1000,10000))
s.head()
```
```
0    588
1    782
2    188
3    790
4    367
dtype: int64
```

We can actually verify that length of the series is correct using the `len` function:
```python
len(s)
```
```10000```

<br/>

Magic functions begin with a percentage sign. If we type this sign and then hit the Tab key, we can see a list of the available magic functions. You could write your own magic functions too, but that's a little bit outside of the scope of this course.

We're actually going to use what's called a cellular magic function. These start with two percentage signs and modify a raptor code in the current Jupyter cell. The function we're going to use is called `timeit`. And as you may have guessed from the name, this function will run our code a few times to determine, on average, how long it takes.

Let's run `timeit` with our original iterative code. You can give timeit the number of loops that you would like to run. By default, we'll use 1,000 loops. I'll ask timeit here to use 100 runs because we're recording this:
```python
%%timeit -n 100
summary = 0
for item in s:
    summary+=item
```
```2.25 ms ± 260 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)```

Not bad. `timeit` ran this code and it doesn't seem like it takes very long at all. Now let's try with vectorization:
```python
%%timeit -n 100
summary = np.sum(s)
```
```218 µs ± 185 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)```

Wow! This is a pretty shocking difference in the speed and demonstrates why data scientists need to be aware of parallel computing features and start thinking in functional programming terms.

Related feature in `pandas` and `numpy` is called *broadcasting*. With broadcasting, you can apply an operation to every value in the series, changing the series. For instance, if we wanted to increase every random variable by 2, we could do so quickly using the `+=` operator directly on the series object:
```python
s+=2 #adds two to each item in s using broadcasting
s.head()
```
```
0    590
1    784
2    190
3    792
4    369
dtype: int64
```

Here I'll just use the `head` operator to just print out the top five rows in the series. The procedural way of doing this would be to iterate through all of the items in the series and increase the values directly:
```python
for label, value in s.iteritems():
    s.set_value(label, value+2)
s.head()
```
```
0    592
1    786
2    192
3    794
4    371
dtype: int64
```

A quick aside here. `pandas` does support iterating through a series much like a dictionary, allowing you to unpack values easily. But if you find yourself iterating through a series, you should question whether you're doing things in the best possible way. Here's how we would do this using the series set value method. Let's try and time the two approaches:
```python
%%timeit -n 10
s = pd.Series(np.random.randint(0,1000,10000))
for label, value in s.iteritems():
    s.loc[label]= value+2
```
```1.4 s ± 8.68 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)```
```python
%%timeit -n 10
s = pd.Series(np.random.randint(0,1000,10000))
s+=2
```
```The slowest run took 31.96 times longer than the fastest. This could mean that an intermediate result is being cached. 1.45 ms ± 2.88 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)```

Amazing. Not only is it significantly faster, but it's more concise and maybe even easier to read too. The typical mathematical operations you would expect are vectorized, and the NumPy documentation outlines what it takes to create vectorized functions of your own.

<br/>

One last note on using the indexing operators to access series data. The .loc attribute lets you not only modify data in place, but also add new data as well. If the value you pass in as the index doesn't exist, then a new entry is added. And keep in mind, indices can have mixed types. While it's important to be aware of the typing going on underneath, Pandas will automatically change the underlying NumPy types as appropriate.

Here's an example using a series of a few numbers. We could add some new value, maybe an animal, as you know, I like bears. Just by calling the `.loc` indexing operator. We see that mixed types for data values or index labels are no problem for Pandas:
```python
s = pd.Series([1, 2, 3])
s.loc['Animal'] = 'Bears'
s
```
```
0             1
1             2
2             3
Animal    Bears
dtype: object
```

<br/>

Up until now I've shown only examples of a series where the index values were unique. I want to end this lecture by showing an example where index values are not unique, and this makes data frames different, conceptually, that a relational database might be.























