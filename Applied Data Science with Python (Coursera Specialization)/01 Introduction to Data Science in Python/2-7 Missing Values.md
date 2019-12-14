# 2-7 Missing Values

**Material**: [log.txt](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/log.txt)

<br/>We're going to end this week of lecture with a quick discussion of *missing values*. We've seen a preview of how Pandas handles missing values using the `None` type and `NumPy` `NaN` values. Missing values are pretty common in data cleaning activities.

There are couple of caveats and discussion points which we should address. First, the built in loading from delimited files provides control for missing values in a few ways. The most germane of these, is the `na_values` list, to indicate other strings which could refer to missing values. Some of my sociologist colleagues for instance, regularly use the value of 99 in binary categories to indicate that there's no value. So this comes in handy. You can also use the `na_filter` option to turn off white space filtering, if white space is an actual value of interest. But in practice, this is pretty rare. In addition to rules controlling how missing values might be loaded, it's sometimes useful to consider missing values as actually having information. I'll give an example from my own research. I often deal with logs from online learning systems. In particular, I've done a couple of projects looking at video use in lecture capture systems. In these systems it's common for the player for have a heartbeat functionality where playback statistics are sent to the server every so often, maybe every 30 seconds. These heartbeats can get big as they can carry the whole state of the playback system, such as where the video play head is at, where the video size is, which video is being rendered to the screen, how loud the volume is, etc.

If we load the data file **log.txt**, we can see an example of what this might look like:

```python
df = pd.read_csv('log.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/035.png' alt='035' width='55%' />

In this data the first column is a timestamp in the Unix epoch format. The next column is the user name followed by a web page they're visiting and the video that they're playing. Each row of the DataFrame has a playback position. And we can see that as the playback position increases by one, the time stamp increases by about 30 seconds. Except for user Bob. It turns out that Bob has paused his playback so as time increases the playback position doesn't change.

Note too how difficult it is for us to try and derive this knowledge from the data, because it's not sorted by time stamp as one might expect. This is actually not uncommon on systems which have a high degree of parallelism. There are a lot of missing values in the paused and volume columns. It's not efficient to send this information across the network if it hasn't changed. So this particular system just inserts null values into the database if there's no changes.

One of the handy functions that Pandas has for working with missing values is the filling function, `fillna`. This function takes a number or parameters, for instance, you could pass in a single value which is called a *scalar value* to change all of the missing data to one value. This isn't really applicable in this case, but it's a pretty common use case. Next up though is the *method parameter*. The two common fill values are `ffill` and `bfill`. ffill is for forward filling and it updates an na value for a particular cell with the value from the previous row. It's important to note that your data needs to be sorted in order for this to have the effect you might want. Data that comes from traditional database management systems usually has no order guarantee, just like this data. So be careful.

```python
df.fillna?
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/036.png' alt='036' width='100%' />

In Pandas we can *sort* either by index or by values. Here we'll just promote the time stamp to an index then sort on the index:

```python
df = df.set_index('time')
df = df.sort_index()
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/037.png' alt='037' width='55%' />

If we look closely at the output though we'll notice that the index isn't really unique. Two users seem to be able to use the system at the same time. Again, a very common case.

Let's reset the index, and use some multi-level indexing instead, and promote the user name to a second level of the index to deal with that issue:

```python
df = df.reset_index()
df = df.set_index(['time', 'user'])
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/038.png' alt='038' width='55%' />

Now that we have the data indexed and sorted appropriately, we can fill the missing datas using `ffill`:

```python
df = df.fillna(method='ffill')
df.head()
```

