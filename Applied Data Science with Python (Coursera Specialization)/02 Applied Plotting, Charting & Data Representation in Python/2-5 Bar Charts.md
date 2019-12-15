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

