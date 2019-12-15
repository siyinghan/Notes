# 2-5 Bar Charts

`Matplotlib` has support for several kinds of **bar charts**. The most general case, we plot a bar chart by sending in a parameter of the x components, and a parameter of the height of the bar. Let's do this with our linear data. Here I'm going to just create a list of values as long as our linear data list. Then, we'll send this along with the linear data's bar heights, to the bar function. We pass in the width of the bar as 0.3:

```python
import numpy as np
linear_data = np.array([1,2,3,4,5,6,7,8])
exponential_data = linear_data**2

plt.figure()
xvals = range(len(linear_data))
plt.bar(xvals, linear_data, width=0.3)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/057.png' alt='057' width='65%' />

To add a **second bar**, we simply call the bar plot again with new data, keeping in mind that we need to adjust the x component to make up for the first bar we plotted. Of course, we'll throw this bar in as red:

```python

```

