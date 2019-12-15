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
new_xvals = []

# plot another set of bars, adjusting the new xvals to make up for the first set of bars plotted
for item in xvals:
    new_xvals.append(item+0.3)

plt.bar(new_xvals, exponential_data, width = 0.3 ,color='red')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/058.png' alt='058' width='65%' />

So the plot looks okay, but not great. All of the x labels are to the far left of the items being described, and not centered. Now, we can center them with a given bar, using the align parameter, but it's a bit frustrating when you have to make multiple bars, and you have to calculate it yourself. And it's a pain to go through and add a new data series manually. And this gets worse, we actually have to manually iterate through and add in dates if we want them. Because otherwise we couldn't set the bar left location appropriately. I'll be honest, bar charts are one of my least favorite things to create in matplotlib. I feel like the foundation is there, but some of the ways I would want to use the API, such as plotting several series of data in groups across time, are sadly missing.

There are some other nice features of bar charts, though. For instance, you can add error bars to each bar as well, using the y-error parameter. For example, each of our pieces of data in the linear data might actually be a mean value, computed from many different observations. So we could just create a list of error values. I'll import from a random function which can generate some random integers, and then I'll use a list comprehension to generate this new list. Then we could just call `plt.bar` again, and see our new data appear:

```python
from random import randint
linear_err = [randint(0,15) for x in range(len(linear_data))] 

# This will plot a new set of bars with errorbars using the list of random error values
plt.bar(xvals, linear_data, width = 0.3, yerr=linear_err)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/059.png' alt='059' width='65%' />

We can also do stacked bar charts as well. For instance, if we wanted to show cumulative values while also keeping the series independent, we could do this by setting the bottom parameter and our second plot to be equal to first set of data to plot:

```python
# stacked bar charts are also possible
plt.figure()
xvals = range(len(linear_data))
plt.bar(xvals, linear_data, width = 0.3, color='b')
plt.bar(xvals, exponential_data, width = 0.3, bottom=linear_data, color='r')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/060.png' alt='060' width='65%' />

Finally, we can pivot this bar graph into a horizontal bar graph by calling the `barh` function instead. But note that we have to change the bottom to a left and the width to a height:

```python
# or use barh for horizontal bar charts
plt.figure()
xvals = range(len(linear_data))
plt.barh(xvals, linear_data, height = 0.3, color='b')
plt.barh(xvals, exponential_data, height = 0.3, left=linear_data, color='r')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/061.png' alt='061' width='65%' />

So those are the basics of charting and plotting in `Matplotlib`. I think it's important to realize that there really isn't any magic. The **scripting layer** is really a set of convenience functions on top of the object layer. Some people share a preference for one or the other, but at the core, they manipulate the same data elements. And I don't think you should think of them as being opposed to one another or duplicative. They work together, and being able to move back and forth is really important.