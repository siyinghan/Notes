# 2-2 Basic Plotting with Matplotlib

With the `Matplotlib` magic having set the back end for us, we're going to start our plotting journey by making a graph using the `plot` function. A plot has **two axes**, an x-axis along the horizon, and a y-axis which runs vertically. First, let's input the pyplot scripting layer as `plt`:

```python
import matplotlib.pyplot as plt
```

All of the functions which will run against the Pyplot module are part of the **scripting layer** of the architecture. Let's take a look at the plot function by looking at the docstring:

```python
plt.plot?
```

```
Signature: plt.plot(*args, scalex=True, scaley=True, data=None, **kwargs)
Docstring:
Plot y versus x as lines and/or markers.

Call signatures::

    plot([x], y, [fmt], *, data=None, **kwargs)
    plot([x], y, [fmt], [x2], y2, [fmt2], ..., **kwargs)

The coordinates of the points or line nodes are given by *x*, *y*.

The optional parameter *fmt* is a convenient way for defining basic
formatting like color, marker and linestyle. It's a shortcut string
notation described in the *Notes* section below.

>>> plot(x, y)        # plot x and y using default line style and color
>>> plot(x, y, 'bo')  # plot x and y using blue circle markers
>>> plot(y)           # plot y using x as index array 0..N-1
>>> plot(y, 'r+')     # ditto, but with red plusses

You can use `.Line2D` properties as keyword arguments for more
control on the appearance. Line properties and *fmt* can be mixed.
The following two calls yield identical results:

>>> plot(x, y, 'go--', linewidth=2, markersize=12)
>>> plot(x, y, color='green', marker='o', linestyle='dashed',
...      linewidth=2, markersize=12)

When conflicting with *fmt*, keyword arguments take precedence.


**Plotting labelled data**

There's a convenient way for plotting objects with labelled data (i.e.
data that can be accessed by index ``obj['y']``). Instead of giving
the data in *x* and *y*, you can provide the object in the *data*
parameter and just give the labels for *x* and *y*::

>>> plot('xlabel', 'ylabel', data=obj)

All indexable objects are supported. This could e.g. be a `dict`, a
`pandas.DataFame` or a structured numpy array.


**Plotting multiple sets of data**

There are various ways to plot multiple sets of data.

- The most straight forward way is just to call `plot` multiple times.
  Example:

  >>> plot(x1, y1, 'bo')
  >>> plot(x2, y2, 'go')

- Alternatively, if your data is already a 2d array, you can pass it
  directly to *x*, *y*. A separate data set will be drawn for every
  column.

  Example: an array ``a`` where the first column represents the *x*
  values and the other columns are the *y* columns::

  >>> plot(a[0], a[1:])

- The third way is to specify multiple sets of *[x]*, *y*, *[fmt]*
  groups::

  >>> plot(x1, y1, 'g^', x2, y2, 'g-')

  In this case, any additional keyword argument applies to all
  datasets. Also this syntax cannot be combined with the *data*
  parameter.

By default, each line is assigned a different style specified by a
'style cycle'. The *fmt* and line property parameters are only
necessary if you want explicit deviations from these defaults.
Alternatively, you can also change the style cycle using the
'axes.prop_cycle' rcParam.


Parameters
----------
x, y : array-like or scalar
    The horizontal / vertical coordinates of the data points.
    *x* values are optional and default to `range(len(y))`.

    Commonly, these parameters are 1D arrays.

    They can also be scalars, or two-dimensional (in that case, the
    columns represent separate data sets).

    These arguments cannot be passed as keywords.

fmt : str, optional
    A format string, e.g. 'ro' for red circles. See the *Notes*
    section for a full description of the format strings.

    Format strings are just an abbreviation for quickly setting
    basic line properties. All of these and more can also be
    controlled by keyword arguments.

    This argument cannot be passed as keyword.

data : indexable object, optional
    An object with labelled data. If given, provide the label names to
    plot in *x* and *y*.

    .. note::
        Technically there's a slight ambiguity in calls where the
        second label is a valid *fmt*. `plot('n', 'o', data=obj)`
        could be `plt(x, y)` or `plt(y, fmt)`. In such cases,
        the former interpretation is chosen, but a warning is issued.
        You may suppress the warning by adding an empty format string
        `plot('n', 'o', '', data=obj)`.

Other Parameters
----------------
scalex, scaley : bool, optional, default: True
    These parameters determined if the view limits are adapted to
    the data limits. The values are passed on to `autoscale_view`.

**kwargs : `.Line2D` properties, optional
    *kwargs* are used to specify properties like a line label (for
    auto legends), linewidth, antialiasing, marker face color.
    Example::

    >>> plot([1,2,3], [1,2,3], 'go-', label='line 1', linewidth=2)
    >>> plot([1,2,3], [1,4,9], 'rs',  label='line 2')

    If you make multiple lines with one plot command, the kwargs
    apply to all those lines.

    Here is a list of available `.Line2D` properties:

  agg_filter: a filter function, which takes a (m, n, 3) float array and a dpi value, and returns a (m, n, 3) array
  alpha: float
  animated: bool
  antialiased or aa: bool
  clip_box: `.Bbox`
  clip_on: bool
  clip_path: [(`~matplotlib.path.Path`, `.Transform`) | `.Patch` | None]
  color or c: color
  contains: callable
  dash_capstyle: {'butt', 'round', 'projecting'}
  dash_joinstyle: {'miter', 'round', 'bevel'}
  dashes: sequence of floats (on/off ink in points) or (None, None)
  drawstyle or ds: {'default', 'steps', 'steps-pre', 'steps-mid', 'steps-post'}, default: 'default'
  figure: `.Figure`
  fillstyle: {'full', 'left', 'right', 'bottom', 'top', 'none'}
  gid: str
  in_layout: bool
  label: object
  linestyle or ls: {'-', '--', '-.', ':', '', (offset, on-off-seq), ...}
  linewidth or lw: float
  marker: marker style
  markeredgecolor or mec: color
  markeredgewidth or mew: float
  markerfacecolor or mfc: color
  markerfacecoloralt or mfcalt: color
  markersize or ms: float
  markevery: None or int or (int, int) or slice or List[int] or float or (float, float)
  path_effects: `.AbstractPathEffect`
  picker: float or callable[[Artist, Event], Tuple[bool, dict]]
  pickradius: float
  rasterized: bool or None
  sketch_params: (scale: float, length: float, randomness: float)
  snap: bool or None
  solid_capstyle: {'butt', 'round', 'projecting'}
  solid_joinstyle: {'miter', 'round', 'bevel'}
  transform: `matplotlib.transforms.Transform`
  url: str
  visible: bool
  xdata: 1D array
  ydata: 1D array
  zorder: float

Returns
-------
lines
    A list of `.Line2D` objects representing the plotted data.

See Also
--------
scatter : XY scatter plot with markers of varying size and/or color (
    sometimes also called bubble chart).

Notes
-----
**Format Strings**

A format string consists of a part for color, marker and line::

    fmt = '[marker][line][color]'

Each of them is optional. If not provided, the value from the style
cycle is used. Exception: If ``line`` is given, but no ``marker``,
the data will be a line without markers.

Other combinations such as ``[color][marker][line]`` are also
supported, but note that their parsing may be ambiguous.

**Markers**

=============    ===============================
character        description
=============    ===============================
``'.'``          point marker
``','``          pixel marker
``'o'``          circle marker
``'v'``          triangle_down marker
``'^'``          triangle_up marker
``'<'``          triangle_left marker
``'>'``          triangle_right marker
``'1'``          tri_down marker
``'2'``          tri_up marker
``'3'``          tri_left marker
``'4'``          tri_right marker
``'s'``          square marker
``'p'``          pentagon marker
``'*'``          star marker
``'h'``          hexagon1 marker
``'H'``          hexagon2 marker
``'+'``          plus marker
``'x'``          x marker
``'D'``          diamond marker
``'d'``          thin_diamond marker
``'|'``          vline marker
``'_'``          hline marker
=============    ===============================

**Line Styles**

=============    ===============================
character        description
=============    ===============================
``'-'``          solid line style
``'--'``         dashed line style
``'-.'``         dash-dot line style
``':'``          dotted line style
=============    ===============================

Example format strings::

    'b'    # blue markers with default shape
    'or'   # red circles
    '-g'   # green solid line
    '--'   # dashed line with default color
    '^k:'  # black triangle_up markers connected by a dotted line

**Colors**

The supported color abbreviations are the single letter codes

=============    ===============================
character        color
=============    ===============================
``'b'``          blue
``'g'``          green
``'r'``          red
``'c'``          cyan
``'m'``          magenta
``'y'``          yellow
``'k'``          black
``'w'``          white
=============    ===============================

and the ``'CN'`` colors that index into the default property cycle.

If the color is the only part of the format string, you can
additionally use any  `matplotlib.colors` spec, e.g. full names
(``'green'``) or hex strings (``'#008000'``).
File:      ~/anaconda3/lib/python3.7/site-packages/matplotlib/pyplot.py
Type:      function
```

If you're not used to seeing it, this Python function declaration with two arguments, the `*args`, and the `**kwargs` can be a bit obscure. This being said here by the `*args` is that the function supports any number of unnamed arguments. The `**kwargs` also means that it supports any number of named arguments. This makes the function declaration very flexible since you can pass in basically any number of arguments stained or not, but it makes it difficult to know what is an appropriate argument. Reading on, we see that the arguments will be interpreted as `x`, `y` pairs.

<br/>

So let's try with just one data point at position 3,2:

```python
# because the default is the line style '-', 
# nothing will be shown if we only pass in one point (3,2)
plt.plot(3, 2)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/037.png' alt='037' width='65%' />

Here, we see that the return value is a line to the object, and we see our first figure up here. We don't see the data points though, which is a bit odd. It turns out that the third argument should be a string which signifies how we want that data point to be rendered.

Let's use a period for a dot, and we'll see that our data point shows up:

```python
# we can pass in '.' to plt.plot to indicate that we want
# the point (3,2) to be indicated with a marker '.'
plt.plot(3, 2, '.')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/038.png' alt='038' width='65%' />

There we go. You'll notice that the subsequent calls to plot have actually updated our visualization.

This is a particular feature of this interactive backend, other backends might not. For instance, you might see some web tutorials using the older `%matplotlib inline` magic instead of the `%matplotlib notebook` magic. The inline magic is not interactive, so subsequent calls create new plots as new cells in the notebook, and this can be handy to.

Here's where some of the confusion with matplotlib as a library tends to come from. In the last lecture, I explained that there's an **artist's layer**, and that it is figures with subplots and axes and data points, which are rendered as patches onto these axes, but we haven't seen any of that here. Instead, we just called one function on a module named **plot**, so what's going on? The `pyplot` scripting interface is managing a lot of objects for you. It keeps track of the latest figure of subplots, and of the axis objects. Moreover, it actually hides some of these behind methods of its own. So the `pyplot` module itself has a function which is called **plot**, but it redirects calls to this function to the current axes object. This makes for a significant learning curve, and you'll see many discussions in web tutorials, and Stack Overflow, where people are confused by these two different approaches to making figures show up.

<br/>

So let's take a look at a comparable approach that's a bit more verbose, and some people would call this the **matplotlib object API**, but I think it's more accurate to think of it as directly interfacing with the **artist layer** instead. First, I'm going to import a new **backend** called `FigureCanvasAgg`. I don't have to use the module or level use function since we're not calling this from the scripting API. Also import, the figure object. Then we'll go ahead and create a new figure and associate it with the backend. We can then add a subplot directly to this. We're going to talk more about subplots in a future lecture, but this number 111 actually means that we just want one plot. The return value for the subplot is the axes object, which contains methods for plotting, so we can plot our image as per usual. Now, the backend that we're using, the one for the Jupyter Notebooks isn't able to render this directly, since it expects the **scripting layer**, pyplot to create it all of the objects. So here we'll save the figure to a ping file instead.

 ```python
# First let's set the backend without using mpl.use() from the scripting layer
from matplotlib.backends.backend_agg import FigureCanvasAgg
from matplotlib.figure import Figure

# create a new figure
fig = Figure()

# associate fig with the backend
canvas = FigureCanvasAgg(fig)

# add a subplot to the fig
ax = fig.add_subplot(111)

# plot the point (3,2)
ax.plot(3, 2, '.')

# save the figure to test.png
# you can see this figure in your Jupyter workspace afterwards by going to
# https://hub.coursera-notebooks.org/
canvas.print_png('test.png')
 ```

Then, we'll do a quick `HTML` cell magic, and execute that and see the rendered image:

```python
%%html
<img src='test.png' />
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/039.png' alt='039' width='65%' />

That's a lot more work than using the **scripting layer**. The scripting layer though isn't magic, it's just doing some of the behind the scenes work for us. For instance, when we make the call to pyplots plotup plot, the **scripting layer** actually looks to see if there's a figure that currently exists, and if not it creates a new one. It then returns the axis for this figure. We can actually get access to the figure using the `GCF` function, which stands for get current figure of pyplot, and get access to the axis as well using the `GCA` function, get current axis.

Okay. Let's create a new figure with `pyplot`. This means it won't update our figure at the top of this file. Then, let's make a plot, grab the axes, and set the x and y limits. We can do this using the axis function. This function takes four parameters, a minimum value for x which we'll put it zero, a maximum value for x which we'll put at six Then, corresponding minimum and maximum values for y which we'll put it zero and 10:

```python
# create a new figure
plt.figure()

# plot the point (3,2) using the circle marker
plt.plot(3, 2, 'o')

# get the current axes
ax = plt.gca()

# Set axis properties [xmin, xmax, ymin, ymax]
ax.axis([0,6,0,10])
```

