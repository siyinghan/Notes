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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/068.png' alt='068' width='20%' />

Looking at the index we can see that it's pretty messy and the dates are all in different formats. Using pandas `to_datetime`, pandas will try to convert these to `Datetime` and put them in a standard format:

```python
ts3.index = pd.to_datetime(ts3.index)
ts3
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/069.png' alt='069' width='20%' />

`to_datetime` also has options to change the date parse order. For example, we can pass in the argument `dayfirst = True` to parse the date in **European date format*:

```python
pd.to_datetime('4.7.12', dayfirst=True)
```

```Timestamp('2012-07-04 00:00:00')```

<br/>

`Timedeltas` are differences in times. We can see that when we take the difference between September 3rd and September 1st, we get a `Timedelta` of two days:

```python
pd.Timestamp('9/3/2016')-pd.Timestamp('9/1/2016')
```

```Timedelta('2 days 00:00:00')```

We can also do something like find what the date and time is for 12 days and three hours past September 2nd, at 8:10 AM:

```python
pd.Timestamp('9/2/2016 8:10AM') + pd.Timedelta('12D 3H')
```

```Timestamp('2016-09-14 11:10:00')```

<br/>
Next, let's look at a few tricks for working with dates in a DataFrame. Suppose we want to look at nine measurements, taken bi-weekly, every Sunday, starting in October 2016. Using `date_range`, we can create this `DatetimeIndex`:

```python
dates = pd.date_range('10-01-2016', periods=9, freq='2W-SUN')
dates
```

```
DatetimeIndex(['2016-10-02', '2016-10-16', '2016-10-30', '2016-11-13',
               '2016-11-27', '2016-12-11', '2016-12-25', '2017-01-08',
               '2017-01-22'],
              dtype='datetime64[ns]', freq='2W-SUN')
```

Now, let's create a `DataFrame` using these dates, and some random data, and see what we can do with it:

```python
df = pd.DataFrame({'Count 1': 100 + np.random.randint(-5, 10, 9).cumsum(),
                  'Count 2': 120 + np.random.randint(-5, 10, 9)}, index=dates)
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/070.png' alt='070' width='28%' />

First, we can check what day of the week a specific date is. For example, here we can see that all the dates in our `index` are on a Sunday:

```python
df.index.weekday_name
```

```
array(['Sunday', 'Sunday', 'Sunday', 'Sunday', 'Sunday', 'Sunday',
       'Sunday', 'Sunday', 'Sunday'], dtype=object)
```

We can use `diff` to find the difference between each date's value:

```python
df.diff()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/071.png' alt='071' width='28%' />

Suppose we wanted to know what the mean count is for each month in our DataFrame. We can do this using `resample`:

```python
df.resample('M').mean()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/072.png' alt='072' width='31%' />

We can use partial string indexing to find values from a particular year:

```python
df['2017']
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/073.png' alt='073' width='27%' />

or from a particular month:

```python
df['2016-12']
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/074.png' alt='074' width='27%' />

or we can even slice on a range of dates. For example, here we only want the values from December 2016 onwards:

```python
df['2016-12':]
```
