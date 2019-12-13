# 1-2 Dates and Times

In Python, you can get the current time since the epoch using the `time` module:
```python
import datetime as dt
import time as tm
```

<br/>

Time returns the current time in seconds since the `Epoch` (January 1st, 1970):
```python
tm.time()
```
```1576251816.63```

<br/>

You can then create a `timestamp` using the `fromtimestamp` function on the `datetime` object:
```python
dtnow = dt.datetime.fromtimestamp(tm.time())
dtnow
```
```datetime.datetime(2019, 12, 13, 15, 44, 34, 320508)```
