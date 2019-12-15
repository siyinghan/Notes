# 3-6 Interactivity

**Interactivity** and **animation** are very similar in Matplotlib. For interactivity though, we have to head down to the artist layer a bit more. In particular, we have to reference the canvas object of the current figure. The canvas object handles all of the drawing events and it's tightly connected with a given back end. If event listening is something you're not familiar with, it can be a bit of a tough concept to grasp. For decades, computers have had abstract methods for doing multiple things at once and now with multiprocessing and multi-core machines, there's actually physical ways Is to do many thing at once. But even before that, the abstraction news was largely focused on the notion of events. Moving a mouse pointer for instance would create an event, clicking will create an event, pressing on keys on the keyboard would create an event. And this didn't only happen at the hardware level such as IRQ interrupts but at the software level as well. In fact, event driven programming has infiltrated most of the ways computer programmers regularly engage with software. From HTML and JavaScript, down to lower level C code. You can think of an event as a piece of data which is associated with a function call. And when the event happens, the software environment, in our case this is Matplotlibs backend, will call the function with the relevant data.

Let's look at a trivial example. We'll create a new figure and plot some random data to it. Then we'll create a new function called onclick. And this takes one parameter, which is the **event object**. So what's in an event object? Well, that depends on the type of the event. Here we're going to deal with mouse events. And they have both an x and a y value as far as the location of the mouse in pixels on the canvas. As well as an x and a y values first location of the mouse relative to our data and axis. So for our onclick we'll clear the current axis then plot our data then set the title of the plot to be variance location of the mouse. Finally, we have to connect this events to an event listener and this process is usually called wiring it up. In this case very easy, get the current figure and its canvas subject then call the `mpl_connect` function. Passing in the string for `button_press_event` as well as reference to the function onclick, which will be call when the event is detected:

```python
plt.figure()
data = np.random.rand(10)
plt.plot(data)

def onclick(event):
    plt.cla()
    plt.plot(data)
    plt.gca().set_title('Event at pixels {},{} \nand data {},{}'.format(event.x, event.y, event.xdata, event.ydata))

# tell mpl_connect we want to pass a 'button_press_event' into onclick when the event is detected
plt.gcf().canvas.mpl_connect('button_press_event', onclick)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/093.png' alt='093' width='65%' />

Now when we click on our plot we see the most information printed to the title. The `Matplotlib` documentation describes the kinds of events you can listen from. But whether they work or not, depends on the backend you're using, and some backends are not interactive. Button presses, key presses, scroll events and figuring axis enter and leave events are almost common. But the most important event for us is the **pick event**. The pick event allows you to respond when the user is actually clicked on a visual element in the figure. Let's look at an example. For this, I want to create a list of countries in randomized order. We can do this with the shuffle function from the random module. Then I'll create a new DataFrame with random values for height and weight, and another column for origin:

```python
from random import shuffle
origins = ['China', 'Brazil', 'India', 'USA', 'Canada', 'UK', 'Germany', 'Iraq', 'Chile', 'Mexico']

shuffle(origins)

df = pd.DataFrame({'height': np.random.rand(10),
                   'weight': np.random.rand(10),
                   'origin': origins})
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/094.png' alt='094' width='30%' />

