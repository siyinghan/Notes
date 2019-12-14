# 2-7 Missing Values

**Material**: [log.txt](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/log.txt)

<br/>We're going to end this week of lecture with a quick discussion of *missing values*. We've seen a preview of how Pandas handles missing values using the `None` type and `NumPy` `NaN` values. Missing values are pretty common in data cleaning activities.

There are couple of caveats and discussion points which we should address. First, the built in loading from delimited files provides control for missing values in a few ways. The most germane of these, is the `na_values` list, to indicate other strings which could refer to missing values. Some of my sociologist colleagues for instance, regularly use the value of 99 in binary categories to indicate that there's no value. So this comes in handy. You can also use the `na_filter` option to turn off white space filtering, if white space is an actual value of interest. But in practice, this is pretty rare. In addition to rules controlling how missing values might be loaded, it's sometimes useful to consider missing values as actually having information. I'll give an example from my own research. I often deal with logs from online learning systems. In particular, I've done a couple of projects looking at video use in lecture capture systems. In these systems it's common for the player for have a heartbeat functionality where playback statistics are sent to the server every so often, maybe every 30 seconds. These heartbeats can get big as they can carry the whole state of the playback system, such as where the video play head is at, where the video size is, which video is being rendered to the screen, how loud the volume is, etc.

If we load the data file **log.txt**, we can see an example of what this might look like:

```python
df = pd.read_csv('log.csv')
df.head()
```

