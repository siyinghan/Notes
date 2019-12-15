# 3-5 Animation

So far we focused on static images, but matplotlib does have some support for both **animation** and **interactivity**. We call this the backend that renders the plot to the stream. Animation and interactivity heavily depend on support from this backend layer. And using a backend like the image png1 doesn't provide this. However, the NBN backend or the matplotlib notebook magic function does provide for some interactivity, so we can leverage that here. The `Maplotlib.animation` module contains important helpers for building animations. For our discussion, the important object here is to call `FuncAnimation`. And it builds an animation by iteratively calling a function which you define. Essentially, your function will either clear the axis object and redraw the next frame, which you want users to see or will return a list of objects which need to be redrawn.

Let's see an example. First, let's import the `animation` module. Next, let's define a cut-off for our animation. I'd like to show you how the histogram is built from one sample through 100 samples. So let's set our cut off to 100 then randomly pick 100 numbers and put them into a variable:

```python
import matplotlib.animation as animation

n = 100
x = np.random.randn(n)
```

Okay, next we want to actually create a function which will do the plotting. We'll call this function update. Now the `matplotlib` `FuncAnimation` object is going to call this every few milliseconds and pass in the frame number we are on starting with frame zero. So we can use this is as the index into our array values, which we called x. The very first thing we want to do is see if the current frame is at the end of our list. If so, we need to tell the animation to stop. We do this by calling the stop object on the event source object attached to the FuncAnimation object. We're going to call our animation a. So, I'll just use that here. I didn't know we can just drop plot as per normal. So lets first clear the current axis with cla, then create a histogram using a set of value in the x up to the current value. Slicing is great for this. Now we also need to consider the bins. Previously we just passed a single number in for the bins eg 10 or 100. But we can also pass in the spacing in between bins. Since we want all of our bins set and evenly spaced, because we're redrawing the animation in each clock tick, we can use the `numpy.arange` function. This will ensure that the bins don't change. We use the balance of minus 4 to plus 4, in half-step increments. We also need to set the axis values since otherwise, the histogram will continually autoscale between frames which could be annoying. So I'll just hard code some values here, often the bin sizes and use 30 as an x and a couple of labels and titles to make the chart look a little better. Finally, let me show you another text function called `annotate`. This places text at a certain position in the chart and we'll use it to show how many samples are currently being rendered to the screen:

```python
# create the function that will do the plotting, where curr is the current frame
def update(curr):
    # check if animation is at the last frame, and if so, stop the animation a
    if curr == n: 
        a.event_source.stop()
    plt.cla()
    bins = np.arange(-4, 4, 0.5)
    plt.hist(x[:curr], bins=bins)
    plt.axis([-4,4,0,30])
    plt.gca().set_title('Sampling the Normal Distribution')
    plt.gca().set_ylabel('Frequency')
    plt.gca().set_xlabel('Value')
    plt.annotate('n = {}'.format(curr), [3,27])
```

Now let's just generate a new figure, then call the FuncAnimation constructor and we'll assign this to variable **a**. The first parameter is the figure that we're working with. This isn't so important here, since we're using the pipe plot scripting interface to manage the figure. Then the name of our function and then the amount of time we want between updates. Let's set this to 100 milliseconds. Also, remember that we have to set this to variable a. Otherwise, our function isn't going to know how to stop the animation:

```python
fig = plt.figure()
a = animation.FuncAnimation(fig, update, interval=100)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/092.gif' alt='092' width='65%' />

save the gif:

```python
Writer = animation.writers['pillow']
writer = Writer(fps=15, metadata=dict(artist='Me'), bitrate=1800)
a.save('a.gif', writer='imagemagick')
```

