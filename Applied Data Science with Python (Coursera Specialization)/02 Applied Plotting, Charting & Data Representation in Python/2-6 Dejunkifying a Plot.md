# 2-6 Dejunkifying a Plot

In this lecture, I want to walk you through the process of taking a regular `Matplotlib` plot and applying Tufte's principles of data-ink ratio and char junk to make it just a little bit better. I'm going to walk through all of the steps using the Jupiter notebooks and you're welcome to follow along. But if you want a bit more of a challenge, I'll be including in video quizzes along the way which prompts you to solve the problem before I address. This is good practice. The video will pause and you can do a quick Google to try and find an appropriate API for solving a specific issue. You can try it out in the system, then you can compare it to my solution right after. Let's get started.

We use a plot of data on the popularity of programming languages taken from stack overflow. Here there are five different languages, `Python`, `SQL`,  `Java`, `C++`, and `JavaScript`. We'll find their positions as a rank using NumPy as a range function. And here are the popularity values from stack overflow.

| Language   | % Popularity |
| ---------- | ------------ |
| Python     | 56           |
| SQL        | 39           |
| Java       | 34           |
| C++        | 34           |
| JavaScript | 29           |

We'll create a bar chart based on rank and popularity, then add x and y ticks and set a title. Then when we call `plot.show`, the figure will render. Okay, here's the first challenge. The tics along both axis are annoying and sort of clutter the document up a bit. And the labels on the y axis really should be direct. So let's remove all of these.

```python
import matplotlib.pyplot as plt
import numpy as np

plt.figure()

languages = ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
pos = np.arange(len(languages))
popularity = [56, 39, 34, 34, 29]

plt.bar(pos, popularity, align='center')
plt.xticks(pos, languages)
plt.ylabel('% Popularity')
plt.title('Top 5 Languages for Math & Data \nby % popularity on Stack Overflow', alpha=0.8)

# remove all the ticks (both axes), and tick labels on the Y axis
plt.tick_params(top=False, bottom=False, left=False, right=False, labelleft=False, labelbottom=True)
plt.show()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/062.png' alt='062' width='65%' />

I use the `tick_params` method of plot to turn them all off except for the bottom label. It's nice to have a single function which can handle all of this. Now our plot still has this frame around it, but it's not really necessary and it seems a little heavyweight. Let's remove that ink. This is a bit more involved, but we can get the current axis, then iterate through all the `spine`, setting their visibility to false:

```python
# remove the frame of the chart
for spine in plt.gca().spines.values():
    spine.set_visible(False)
plt.show()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/063.png' alt='063' width='65%' />

Already, this chart looks much more lightweight. Now, the blue is okay, but it doesn't really help us differentiate between the bars at all. How about we soften all of the hard blacks to gray, then we change the bar colors to gray as well. Also, let's keep the Python bar the same color of blue that it was originally to make it stand out:

```python
import matplotlib.pyplot as plt
import numpy as np

plt.figure()

languages = ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
pos = np.arange(len(languages))
popularity = [56, 39, 34, 34, 29]

# change the bar colors to be less bright blue
bars = plt.bar(pos, popularity, align='center', linewidth=0, color='lightslategrey')
# make one bar, the python bar, a contrasting color
bars[0].set_color('#1F77B4')

# soften all labels by turning grey
plt.xticks(pos, languages, alpha=0.8)
plt.ylabel('% Popularity', alpha=0.8)
plt.title('Top 5 Languages for Math & Data \nby % popularity on Stack Overflow', alpha=0.8)

# remove all the ticks (both axes), and tick labels on the Y axis
plt.tick_params(top=False, bottom=False, left=False, right=False, labelleft=False, labelbottom=True)
plt.show()

# remove the frame of the chart
for spine in plt.gca().spines.values():
    spine.set_visible(False)
plt.show()
```

