# 3-6 Date Functionality (time series)

Welcome to today's tutorial, where we'll be looking at the **time series** and **date functionally** in pandas. Pandas has four main time related classes. `Timestamp`, `DatetimeIndex`, `Period`, and `PeriodIndex`.

First, let's look at `Timestamp`. `Timestamp` represents a single timestamp and associates values with points in time. For example, let's create a timestamp using a string 9/1/2016 10:05AM, and here we have our timestamp:

```python
pd.Timestamp('9/1/2016 10:05AM')
```

```Timestamp('2016-09-01 10:05:00')```

`Timestamp` is interchangeable with Python's datetime in most cases.

<br/>

Suppose we weren't interested in a specific point in time, and instead wanted a span of time. This is where `Period` comes into play. Period represents a single time span, such as a specific day or month. Here we are creating a period that is January 2016, and here's an example of a period that is March 5th, 2016:

```python
pd.Period('1/2016')
```

```Period('2016-01', 'M')```

```python
pd.Period('3/5/2016')
```

```Period('2016-03-05', 'D')```

<br/>

The index of a timestamp is `DatetimeIndex`. Let's look at a quick example. First, let's create our example series t1, we'll use the Timestamp of September 1st, 2nd and 3rd of 2016:

```python
t1 = pd.Series(list('abc'), [pd.Timestamp('2016-09-01'), pd.Timestamp('2016-09-02'), pd.Timestamp('2016-09-03')])
t1
```

```
2016-09-01    a
2016-09-02    b
2016-09-03    c
dtype: object
```

When we look at the series, each `Timestamp` is the index and has a value associated with it, in this case, **a**, **b** and **c**. Looking at the type of our series index, we see that it's `DatetimeIndex`:

```python
type(t1.index)
```

```pandas.tseries.index.DatetimeIndex```

<br/>
Similarly, the index of period is `PeriodIndex`. Let's create another example series t2. This time, we'll use the values d, e, and f and match them with the period September, October and November 2016:

```python
t2 = pd.Series(list('def'), [pd.Period('2016-09'), pd.Period('2016-10'), pd.Period('2016-11')])
t2
```

```
2016-09    d
2016-10    e
2016-11    f
Freq: M, dtype: object
```

Looking at the type of the `ts2.index`, we can see that it's `PeriodIndex`:

```python
type(t2.index)
```

```pandas.tseries.period.PeriodIndex```

<br/>

Now, let's look into how to *convert to Datetime*. Suppose we have a list of dates as strings. If we create a DataFrame using these dates as the index. And some randomly generated data, this is the DataFrame we get:

```python
d1 = ['2 June 2013', 'Aug 29, 2014', '2015-06-26', '7/12/16']
ts3 = pd.DataFrame(np.random.randint(10, 100, (4,2)), index=d1, columns=list('ab'))
ts3
```

