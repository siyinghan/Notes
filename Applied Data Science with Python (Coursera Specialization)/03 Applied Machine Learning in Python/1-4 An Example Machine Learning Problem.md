# 1-4 An Example Machine Learning Problem

**Material**: [fruit_data_with_colors.txt](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Material/fruit_data_with_colors.txt)

<br/>

For our first machine learning exploration, we're going to build an extremely simple form of object recognition system. Now although the example we'll use is very simple, it does reflect many of the same key machine learning concepts that go into building real world commercial systems. The dataset we're going to use is a small, very simple, example dataset derived from one originally created by Dr. Iain Murray at the University of Edinburgh for the task of training a classifier to distinguish between different types of fruit.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/034.png' alt='034'/>

So to create the original dataset, Dr. Murray went to a nearby store, bought a few dozen oranges, lemons, and apples of different varieties, and recorded their measurements in a table. So he sat down and he looked at the **height** and the **width**, estimated their **mass**, and so forth. So, we've formatted his original data slightly and added one or two extra simulated features such as a **color score** for instructional purposes. This dataset is called **fruit_data_with_colors.txt**. And it's included in the folder of materials that you downloaded for this course. Now you might think that **fruit prediction** is a sort of silly and impractical scenario. And given the limited nature of this dataset, it is a bit of a toy example. But actually, food companies do indeed now rely on machine learning systems that aren't all that different in concept from the ones we're about to build, so they can do **automated quality control**. And in fact, there do exist for example, real systems used by fruit shipping companies that screen for rotten oranges during processing. Now the features that they use in building these systems are a little more sophisticated than the ones we'll look at here. So for example, quality control systems for rotten orange detection use ultraviolet light that can detect interior decay, which is often less visible than just by looking on the surface. Anyway, to solve machine learning problems, you can think of the input data as a **table**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/035.png' alt='035'/>

Where each object, so in our case a piece of fruit, is represented by a row, and the attributes of the object, the measurement, the color, the size, and so forth in our case for a piece of fruit, the features of the fruit are represented by the values that you see across the columns. In a **supervised learning problem**, the dataset will also typically contain a special column with the label of the object, if the dataset does not have such a field already. Sometimes you can derive it from information that's in one or more columns. So, to make sure you're ready to continue, make sure you've run the following code snippet that loads the proper libraries we're going to need to proceed. And we'll show those here now.

So the first thing we are going to do is to load the fruit dataset file using the very handy read table command in pandas:

```python
%matplotlib notebook
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.model_selection import train_test_split

fruits = pd.read_csv('fruit_data_with_colors.txt', delimiter='\t')
```

Now, this will read the dataset from disk, and store it into a data frame variable that we'll call **fruits** here. Okay, let's look at this dataset and dump out the first few rows of the data frame.

```python
fruits.head()
```

