# 2-3 Scatterplots

In the previous lecture, I introduced the `plot` function, which generates a series of lines which get rendered against an axis object. Matplotlib actually has a number of useful plotting methods in the **scripting layer** which correspond to different kinds of plots. We are not going to go through all of them here but we'll touch on a few of the major ones. Regardless, there are a few things to keep in mind which we learned in the previous lecture:

* One, `pyplot` is going to retrieve the current figure with the function `gcf` and then get the current axis with the function `gca`. Pyplot is keeping track of the axis objects for you. But don't forget that they're there and we can get them when we want to get them.
* Two, also pyplot just mirrors the API of the axis objects. So you can call the `plot` function against the pyplot module. But this is calling the axis plot functions underneath, so be aware.
* And three, finally, remember that the function declaration from most of the functions in matplotlib end with an open set of keyword arguments. There are a lot of different properties you can control through these keyword arguments. And I'll start peppering in some of them this week to demostrate that the matplotlib documentation is really key in gaining a full understanding of the options available.

With that in mind let's move on to talk first about **scatterplots**.

A **scatterplot** is a two dimensional plot similar to the line plots I've shown. The scatter function takes an x-axis value as a first argument and y-axis value as the second. If the two arguments are the same, we get a nice diagonal alignment of points. Let's do this now. I'll bring in `numpy` as we're going to use it later and matplotlib is really based on numpy arrays. I'll create a short array for **x** and make **y** the same. Then create a new figure and scatterplot. You can see in this plot a nice diagonal line and `matplotlib` has sized our axises accordingly:

```python
import numpy as np
x = np.array([1,2,3,4,5,6,7,8])
y = x

plt.figure()
plt.scatter(x, y) # similar to plt.plot(x, y, '.'), but the underlying child objects in the axes are not Line2D
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/042.png' alt='042' width='65%' />

Now, `scatter` doesn't represent items as a series. Instead, we can pass it a list of colors which correspond to given points. Let's use some list arithmetic to create a new list just short of the number of data points we need and set all of the values to green. Then we'll add a final value of red. Then we'll plot this, and we'll set the size of the data points to 100 to make it a little easier to see. The separation of data points into lists, which describes them as components is a pretty common pattern in `matplotlib`:

```python
import numpy as np
x = np.array([1,2,3,4,5,6,7,8])
y = x

# create a list of colors for each point to have
# ['green', 'green', 'green', 'green', 'green', 'green', 'green', 'red']
colors = ['green']*(len(x)-1)
colors.append('red')

plt.figure()
# plot the point with size 100 and chosen colors
plt.scatter(x, y, s=100, c=colors)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/043.png' alt='043' width='65%' />

You have some set of items, but they're actually described as the same slice across many different data sources. It's in one object-based language, but you might expect that each data point is represented with its own instance, which encapsulates all of its properties. For instance, it's called an x value and a y value and a color and a size. That's not the case here. This is where it's useful to have some knowledge of list comprehensions and lambdas as we talked about in the first course. Also important is the zip function and list unpacking. And because this is so common in the Python data science world, I'm going to take a brief aside and talk about that here. Recall that the zip method takes a number of iterables and creates tuples out of them, matching elements based on index. So if we have two lists of numbers, zip will take the first from each and create a tuple, then the second from each and create a tuple, and so on. Also remember that zip has lazy evaluation because it's actually a generator in Python 3 which means we need to use the list function if we want to see the results of iterating over zip. Let's demonstrate.

Here we'll create a new `zip` generator with a zip function passing in two lists of numbers. When we convert this generator to a list, we see there's a list of pairwise tuples:

```python
# convert the two lists into a list of pairwise tuples
zip_generator = zip([1,2,3,4,5], [6,7,8,9,10])
print(list(zip_generator))
```

```[(1, 6), (2, 7), (3, 8), (4, 9), (5, 10)]```

```python
# The single star * unpacks a collection into positional arguments
print(*zip_generator)
```

```(1, 6) (2, 7) (3, 8) (4, 9) (5, 10)```

Storing point data as tuples is common and you should be familiar with being able to convert data to and from this form. If we want to turn the data back into two lists, one with the **x component** and one with the **y component**, we can use parameter unpacking with zip. When you pass a list or an interval more generally to a function and prepend it with an asterisk, each item is taken out of the iterable and passed as a separate argument.

So we can do that here, passing into a new `zip` function five parameters, each of length two.`zip` will then create a new two value list which is identical to our original x and y values. If we want to get even fancier, we can unpack this result into two variables directly, **x** and **y**:

```python
# use zip to convert 5 tuples with 2 elements each to 2 tuples with 5 elements each
print(list(zip((1, 6), (2, 7), (3, 8), (4, 9), (5, 10))))
```

```[(1, 2, 3, 4, 5), (6, 7, 8, 9, 10)]```

```python
zip_generator = zip([1,2,3,4,5], [6,7,8,9,10])
# let's turn the data back into 2 lists
x, y = zip(*zip_generator) # This is like calling zip((1, 6), (2, 7), (3, 8), (4, 9), (5, 10))
print(x)
```

```(1, 2, 3, 4, 5)```

```python
print(y)
```

```(6, 7, 8, 9, 10)```

So that's a brief aside on a variable tool. When it comes to manipulating and cleaning data in the wild. Now, let's get back to plotting. Let's take these two lists and plot them to a new figure using `scatter`. Instead of plotting them as one data series, we'll slice the lists and plot them as two data series. You'll note that we can color each series with a single value if we want to. We can also do things like change the color or transparency of an entire series, or individual data points as well. Finally, we have the ability to label the data series, and I'll do that now:

```python
plt.figure()
# plot a data series 'Tall students' in red using the first two elements of x and y
plt.scatter(x[:2], y[:2], s=100, c='red', label='Tall students')
# plot a second data series 'Short students' in blue using the last three elements of x and y 
plt.scatter(x[2:], y[2:], s=100, c='blue', label='Short students')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/044.png' alt='044' width='65%' />

Now before we leave the scatter plot, let's talk a bit more about the properties of axis. The axis generally have labels to them to explain what they represent or the units that they describe. Charts tend to have titles as well, so let's put this in place now. Since `pyplot` mirrors much of the axis API, we can make calls directly on `pyplot`. Let's do this now, adding in an `xlabel`, a `ylabel`, and then a `title`:

```python
# add a label to the x axis
plt.xlabel('The number of times the child kicked a ball')
# add a label to the y axis
plt.ylabel('The grade of the student')
# add a title
plt.title('Relationship between ball kicking and grades')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/045.png' alt='045' width='65%' />

And let's add a `legend` as well:

```python
# add a legend (uses the labels from plt.scatter)
plt.legend()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/046.png' alt='046' width='65%' />

You'll see that matplotlib places this in the upper left hand corner and puts a little visual about our data series there. In the docs for the legend, you'll see that there are a number of different parameters and one of them is called `loc`. And a value of **4**, we'll put it in the lower right hand corner of the axis:

```python
# add the legend to loc=4 (the lower right hand corner), also gets rid of the frame and adds a title
plt.legend(loc=4, frameon=False, title='Legend')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/047.png' alt='047' width='65%' />

| Location String | Location Code |
| --------------- | ------------- |
| 'best'          | 0             |
| 'upper right'   | 1             |
| 'upper left'    | 2             |
| 'lower left'    | 3             |
| 'lower right'   | 4             |
| 'right'         | 5             |
| 'center left'   | 6             |
| 'center right'  | 7             |
| 'lower center'  | 8             |
| 'upper center'  | 9             |
| 'center'        | 10            |

We could also get rid of the frame and add a title, and do any number of different transformations.

The legend itself is an `artist`, which means it can contain `children`. Let's take advantage of this and write a little routine to recursively go through the list of `children` in an `artist`:

```python
# get children from current axes (the legend is the second to last item in this list)
plt.gca().get_children()
```

```
[<matplotlib.collections.PathCollection at 0x11d50a5c0>,
 <matplotlib.collections.PathCollection at 0x11d50a898>,
 <matplotlib.spines.Spine at 0x11c05f278>,
 <matplotlib.spines.Spine at 0x11c05f198>,
 <matplotlib.spines.Spine at 0x11c05fa20>,
 <matplotlib.spines.Spine at 0x11c04b748>,
 <matplotlib.axis.XAxis at 0x11c05f550>,
 <matplotlib.axis.YAxis at 0x11cb31e80>,
 Text(0.5, 1, 'Relationship between ball kicking and grades'),
 Text(0.0, 1, ''),
 Text(1.0, 1, ''),
 <matplotlib.legend.Legend at 0x11d5a3278>,
 <matplotlib.patches.Rectangle at 0x11cabce10>]
```

First, we'll import the `artist` class from matplotlib. Then we'll make a recursive function which takes in an artist and some depth parameter. Then checks if the object is an artist and if so, prints out its string name. Then recurses and increases the depth for pretty printing. Finally, we can call this on the `legend` object itself:

```python
# import the artist class from matplotlib
from matplotlib.artist import Artist

def rec_gc(art, depth=0):
    if isinstance(art, Artist):
        # increase the depth for pretty printing
        print("  " * depth + str(art))
        for child in art.get_children():
            rec_gc(child, depth+2)

# Call this function on the legend artist to see what the legend is made up of
rec_gc(plt.legend())
```

```
Legend
    <matplotlib.offsetbox.VPacker object at 0x11d586278>
        <matplotlib.offsetbox.TextArea object at 0x11d586588>
            Text(0, 0, '')
        <matplotlib.offsetbox.HPacker object at 0x11d586ba8>
            <matplotlib.offsetbox.VPacker object at 0x11d586da0>
                <matplotlib.offsetbox.HPacker object at 0x11d586cc0>
                    <matplotlib.offsetbox.DrawingArea object at 0x11d5ae5c0>
                        <matplotlib.collections.PathCollection object at 0x11d5ae550>
                    <matplotlib.offsetbox.TextArea object at 0x11d5ae2e8>
                        Text(0, 0, 'Tall students')
                <matplotlib.offsetbox.HPacker object at 0x11d586940>
                    <matplotlib.offsetbox.DrawingArea object at 0x11d5ae3c8>
                        <matplotlib.collections.PathCollection object at 0x11d5aedd8>
                    <matplotlib.offsetbox.TextArea object at 0x11d5aec50>
                        Text(0, 0, 'Short students')
    FancyBboxPatch((0, 0), width=1, height=1)
```

So you can see the `legend` `artist` is just made up of a number of different offsetboxes for drawing, as well as `TextArea`s and `PathCollections`.

What I want you to take away from this is that there is nothing magical about what matplotlib is doing. Calls to the scripting interface, just create figures, subplots, and axis. Then load those axis up with various artists, which the back-end renders to the screen or some other medium like a file. While you'll spend 95% of your time at the scripting layer, happily creating graphs and charts, it's important to understand how the library works underneath for the other 5% of the time. And the time that you will use this is when you really want to have control over and to create your own charting functions, and you'll have a chance to do that by the end of this course.