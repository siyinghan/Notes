# 3-1 Subplots

In module one, we talked about principles, which underly good visualizations, we pulled from work by Cairo and Tufty. In Module 2, we opened up the `Matplotlib` `Python` Library. Starting with the architecture and working our way through some the most common kinds of plots. Scatter plots, line graphs and bar charts. In this module, we're going to do a bit deeper and talk about multiple plots with the same figure, interaction, animation and a few more kinds of plots which you might find useful in your data science journey. 

Now, if you've been doing these assignments, you've undoubtedly been visiting our course discussion forms, going to stack overflow, and reading the map plot live API documentation. I want to point you to the Matplotlib mailing list as well is another great resource. There would be resource posted below on how to browse that list. It's pretty common with open source projects to have two mailing lists. One for developers and the other for users. The users place is where most of the question answering happens. But I encourage to you look at the developer archives, too. To get an idea as to what these kind of projects look like behind the scenes.

Let's start this module with a deeper look at subplots. Thus far we have been using a signal axis object to plot a single graph or figure. Sometimes it is useful to show two complex plot side by side for the viewer to compare. Matplotlib handles this with a single figure. Let's first set our rendering backend to the **NPA backend**, then import our `pyplot` module and `NumPy`, as we'll need then both:

```python
%matplotlib notebook

import matplotlib.pyplot as plt
import numpy as np

plt.subplot?
```

```
Signature: plt.subplot(*args, **kwargs)
Docstring:
Add a subplot to the current figure.

Wrapper of `.Figure.add_subplot` with a difference in behavior
explained in the notes section.

Call signatures::

   subplot(nrows, ncols, index, **kwargs)
   subplot(pos, **kwargs)
   subplot(ax)

Parameters
----------
*args
    Either a 3-digit integer or three separate integers
    describing the position of the subplot. If the three
    integers are *nrows*, *ncols*, and *index* in order, the
    subplot will take the *index* position on a grid with *nrows*
    rows and *ncols* columns. *index* starts at 1 in the upper left
    corner and increases to the right.

    *pos* is a three digit integer, where the first digit is the
    number of rows, the second the number of columns, and the third
    the index of the subplot. i.e. fig.add_subplot(235) is the same as
    fig.add_subplot(2, 3, 5). Note that all integers must be less than
    10 for this form to work.

projection : {None, 'aitoff', 'hammer', 'lambert', 'mollweide', 'polar', 'rectilinear', str}, optional
    The projection type of the subplot (`~.axes.Axes`). *str* is the name
    of a costum projection, see `~matplotlib.projections`. The default
    None results in a 'rectilinear' projection.

polar : boolean, optional
    If True, equivalent to projection='polar'.

sharex, sharey : `~.axes.Axes`, optional
    Share the x or y `~matplotlib.axis` with sharex and/or sharey. The
    axis will have the same limits, ticks, and scale as the axis of the
    shared axes.

label : str
    A label for the returned axes.

Other Parameters
----------------
**kwargs
    This method also takes the keyword arguments for
    the returned axes base class. The keyword arguments for the
    rectilinear base class `~.axes.Axes` can be found in
    the following table but there might also be other keyword
    arguments if another projection is used.
      adjustable: {'box', 'datalim'}
  agg_filter: a filter function, which takes a (m, n, 3) float array and a dpi value, and returns a (m, n, 3) array
  alpha: float
  anchor: 2-tuple of floats or {'C', 'SW', 'S', 'SE', ...}
  animated: bool
  aspect: {'auto', 'equal'} or num
  autoscale_on: bool
  autoscalex_on: bool
  autoscaley_on: bool
  axes_locator: Callable[[Axes, Renderer], Bbox]
  axisbelow: bool or 'line'
  clip_box: `.Bbox`
  clip_on: bool
  clip_path: [(`~matplotlib.path.Path`, `.Transform`) | `.Patch` | None]
  contains: callable
  facecolor: color
  fc: color
  figure: `.Figure`
  frame_on: bool
  gid: str
  in_layout: bool
  label: object
  navigate: bool
  navigate_mode: unknown
  path_effects: `.AbstractPathEffect`
  picker: None or bool or float or callable
  position: [left, bottom, width, height] or `~matplotlib.transforms.Bbox`
  rasterization_zorder: float or None
  rasterized: bool or None
  sketch_params: (scale: float, length: float, randomness: float)
  snap: bool or None
  title: str
  transform: `.Transform`
  url: str
  visible: bool
  xbound: unknown
  xlabel: str
  xlim: (left: float, right: float)
  xmargin: float greater than -0.5
  xscale: {"linear", "log", "symlog", "logit", ...}
  xticklabels: List[str]
  xticks: list
  ybound: unknown
  ylabel: str
  ylim: (bottom: float, top: float)
  ymargin: float greater than -0.5
  yscale: {"linear", "log", "symlog", "logit", ...}
  yticklabels: List[str]
  yticks: list
  zorder: float

Returns
-------
axes : an `.axes.SubplotBase` subclass of `~.axes.Axes` (or a subclass     of `~.axes.Axes`)

    The axes of the subplot. The returned axes base class depends on
    the projection used. It is `~.axes.Axes` if rectilinear projection
    are used and `.projections.polar.PolarAxes` if polar projection
    are used. The returned axes is then a subplot subclass of the
    base class.

Notes
-----
Creating a subplot will delete any pre-existing subplot that overlaps
with it beyond sharing a boundary::

    import matplotlib.pyplot as plt
    # plot a line, implicitly creating a subplot(111)
    plt.plot([1,2,3])
    # now create a subplot which represents the top plot of a grid
    # with 2 rows and 1 column. Since this subplot will overlap the
    # first, the plot (and its axes) previously created, will be removed
    plt.subplot(211)

If you do not want this behavior, use the `.Figure.add_subplot` method
or the `.pyplot.axes` function instead.

If the figure already has a subplot with key (*args*,
*kwargs*) then it will simply make that subplot current and
return it.  This behavior is deprecated. Meanwhile, if you do
not want this behavior (i.e., you want to force the creation of a
new subplot), you must use a unique set of args and kwargs.  The axes
*label* attribute has been exposed for this purpose: if you want
two subplots that are otherwise identical to be added to the figure,
make sure you give them unique labels.

In rare circumstances, `.add_subplot` may be called with a single
argument, a subplot axes instance already created in the
present figure but not in the figure's list of axes.

See Also
--------
.Figure.add_subplot
.pyplot.subplots
.pyplot.axes
.Figure.subplots

Examples
--------
::

    plt.subplot(221)

    # equivalent but more general
    ax1=plt.subplot(2, 2, 1)

    # add a subplot with no frame
    ax2=plt.subplot(222, frameon=False)

    # add a polar subplot
    plt.subplot(223, projection='polar')

    # add a red subplot that shares the x-axis with ax1
    plt.subplot(224, sharex=ax1, facecolor='red')

    # delete ax2 from the figure
    plt.delaxes(ax2)

    # add ax2 to the figure again
    plt.subplot(ax2)
    
File:      ~/anaconda3/lib/python3.7/site-packages/matplotlib/pyplot.py
Type:      function
```

If we look at the `subplot` documentation, we see that the first argument is the *number of rows*, the second the *number of columns*, and the third is the *plot number*.

In `matplotlib`, a conceptual grid is overlayed on the figure. And a `subplot` command allows you to create axis to different portions of this grid. For instance, if we want to to create two plots side by side, we would call subplot with the parameters 1, 2, and 1. This would allow us to use 1 row, with 2 columns, and set the first axis to be the current axis. Let's do this now. We'll create a new figure and then a new subplot with one row and two columns. And we'll ask for the left hand side axis. The greatest number alternatively from left to right and top to bottom. So subsequent calls to plot would create the left hand side plot:

```python
plt.figure()
# subplot with 1 row, 2 columns, and current axis is 1st subplot axes
plt.subplot(1, 2, 1)

linear_data = np.array([1,2,3,4,5,6,7,8])

plt.plot(linear_data, '-o')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/068.png' alt='068' width='65%' />

Okay, great we've got a skinny plot on the left hand side. We can then call `subplot` again with the last parameter as a two to plot new data to a plot on the right hand side:

```python
exponential_data = linear_data**2 

# subplot with 1 row, 2 columns, and current axis is 2nd subplot axes
plt.subplot(1, 2, 2)
plt.plot(exponential_data, '-o')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/069.png' alt='069' width='65%' />

And that's nice. Now we have two plots, each with their own axis objects.

Now the norm with `matplotlib` is that you store the axis object that you get back from the subplot. But you can call `subplot` again. At any time with the parameters that interest you in order to get back a given axis. Here, let's put exponential on the linear graph 2:

```python
plt.figure()
# subplot with 1 row, 2 columns, and current axis is 1st subplot axes
plt.subplot(1, 2, 1)
linear_data = np.array([1,2,3,4,5,6,7,8])
plt.plot(linear_data, '-o')

# plot exponential data on 1st subplot axes
plt.subplot(1, 2, 1)
plt.plot(exponential_data, '-x')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/070.png' alt='070' width='65%' />

This demonstrates a common problem, it looked like linear had roughly the same area under the line on the chart until we asked matplotlib to put them into one graph. Then the y axis was refreshed. There would be a big problem with misleading the reader if we didn't find a way to lock axis between two plots. When you create a new subplot you are able to share the x, y, or both axis using the share x and share y parameters.

Here's how we could clean this up, we create a new figure. Then created a subplot on the left-hand side store it in AX1. After plotting that data we create the axis on the right-hand side, and we indicate explicitly we want to share the y-axis. Now we don't have to store the subplot to a variable like we did with AX1. Remember that when you use the scripting interface, high plot is going to get the current axis object with `GCA` or get current axis underneath. So a call to pipeplot.plot will transparently work with the last axis objects that we're using:

```python
plt.figure()
ax1 = plt.subplot(1, 2, 1)
plt.plot(linear_data, '-o')
# pass sharey=ax1 to ensure the two subplots share the same y axis
ax2 = plt.subplot(1, 2, 2, sharey=ax1)
plt.plot(exponential_data, '-x')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/071.png' alt='071' width='65%' />

There we go. Two plots side by side and we've locked the y axis.

Now, those of you who have been playing close attention will note that I used the add subplot function in the last module. But I didn't pass in three parameters, just one. The maplotlib developers allow you to specify the row, columns, and number of the plot that you want with either three parameters or a single parameter. Where the hundreds values the first argument, the tens the second argument, and the ones the third argument. So we will call subplot with three parameters, one, two, and one. And the axis that return should be equal to 1, which is created with the 1 parameter, 121:

```python
plt.figure()
# the right hand side is equivalent shorthand syntax
plt.subplot(1,2,1) == plt.subplot(121)
```

```True```

I'm frankly not a big fan of this second syntax. It feels pretty hacky and it really only saves typing two commas and yet limits us to single digit radius.

Now computer science folks might feel a little twitch inside like something's wrong with this notation. And I'll say that it certainly bugged me the first few times I saw it. An important fact to remember is that the plot location in the matrix of items is index starting at one and not at zero, as would be the convention if you were using something like NumPy. So if you're iterating through a matrix or list, create subplots. Remember to start at position plus one. Now, there's a nice function called `subplots`, note the plural, which allows you to get many axis objects at once, and I think this is great.

So, if we wanted to get a three by three grid with all of the axis x and y ranges locked, we can do so like this. The syntax looks a little goofy maybe since we're unpacking the results of the subplots function directly. Wherein it's an effective way to build a grid where everything shares an axis. And of course, you could just return the tuple of plots and iterate it over if you wanted to.

```python
# create a 3x3 grid of subplots
fig, ((ax1,ax2,ax3), (ax4,ax5,ax6), (ax7,ax8,ax9)) = plt.subplots(3, 3, sharex=True, sharey=True)
# plot the linear_data on the 5th subplot axes 
ax5.plot(linear_data, '-')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/072.png' alt='072' width='70%' />

The results however look really nice. Note that this method turns off the y and x labels except for those plots which are on the left hand side or the bottom of the figure. If you want to turn the labels back on, you need to iterate through the axis objects and do it yourself. You could do this directly through the axis objects you have or iterate through all the axis objects in the figure and change the x and y tick labels to be visible. Unfortunately, on the notebook backend on my installation, this doesn't redraw the figure:

```python

```



But you can force the figure to redraw by calling the canvas draw function. Remember you can get the current figure at any time using `pyplots.gcf` or get current figure or function:

```python
# necessary on some systems to update the plot
plt.gcf().canvas.draw()
```