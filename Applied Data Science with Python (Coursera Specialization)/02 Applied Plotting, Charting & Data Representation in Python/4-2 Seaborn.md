# 4-2 Seaborn

Hi, everyone. Today, we'll be looking at `Seaborn`, a Python visualization library based on `matplotlib`. `Seaborn` is really just a wraparound matplotlib. It adds styles to make default data visualizations much more visually appealing and makes creation of specific types of complicated plots much simpler. To get us started, I've imported `seaborn` as `sns`:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib notebook
```

Now, let's set the seed for the random number generator. Which lets us reproduce the data. Next, let's make a panda series v1 that's 1000 numbers drawn from a normal distribution with a mean of 0, and a standard deviation of 10. Let's also make a second pandas series, v2, which is 2 times v1, plus 1,000 numbers drawn from a normal distribution with a mean of 60 and standard deviation of 15:

```python
np.random.seed(1234)

v1 = pd.Series(np.random.normal(0,10,1000), name='v1')
v2 = pd.Series(2*v1 + np.random.normal(60,15,1000), name='v2')
```

Now let's see what the histograms of these two variables look like when we plot them side by side. We can set alpha equal to 0.7 so the histograms don't cover one another up. For the bin parameter, instead of integer denoting the number of bins we want we can also pass in a specific sequence using `np.arange` to specify the specific bins we want to use. This is useful for the one when we want to plot two histograms in the same figure to make sure the bin sizes are equivalent for both histograms. We also add labels so we can see which histogram belongs to which variable using a `legend`:

```python
plt.figure()
plt.hist(v1, alpha=0.7, bins=np.arange(-50,150,5), label='v1');
plt.hist(v2, alpha=0.7, bins=np.arange(-50,150,5), label='v2');
plt.legend();
```

