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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/036.png' alt='036' width='520px'/>

So, here we can see that each row of the dataset represents one piece of fruit as represented by several features that are in the table's columns. So, in order, the columns that we see are **fruit label**. So this is the training label that we used. It's a number that corresponds to the general type of fruit. So for example, one is an apple, two is a mandarin orange, three is a regular orange, and so forth. So this label was supplied by the human creator of the dataset. The fruit name and fruit subtype columns contain text descriptions of the general and specific fruit categories. And the fruit name corresponds, it's a text form of the corresponding fruit label in the same row. Now, we won't be using these name columns as features. I've just included them here to make the dataset a bit more readable for our purposes. After that, the features in this representation include measurements for each fruit that capture its mass in grams and its width and height in centimeters. And finally, there's a feature stored in a column called **color score** that's meant to be a single number that captures a rough idea of the color of the fruit.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/037.png' alt='037' width='520px'/>

So in a real system, this would actually be something more sophisticated, like a histogram of the distribution of colors, or maybe the pixels from an actual image or video of the fruit. But for our purposes, we're going to just summarize the color along a spectrum scale that'll be a handy summary that we can use that will just be easy to visualize. So scores close to one mean the fruit is red. Scores around 0.7 indicate yellow, and so forth.

```python
fruits.shape
```

```(59, 7)```

So, looking at this data frame, we can see that it contains 59 rows corresponding to 59 different pieces of fruit that have been measured and entered into the table. So our goal here is to build a **classifier** from this data that can predict the correct type of fruit for any given observation of its features such as **mass**, **height**, **width**, and **color score**. So for example, can we tell based on the color score and the dimensions, the difference between an orange and a lemon and have the classifier predict the type of piece of fruit correctly just from its observed measurements.

Now, assuming for the moment that we already we had a classifier ready to go, how would we know if its predictions were likely to be accurate? Well, we could choose a fruit sample, called a test sample, for which we already had a label. So we could feed the features of that piece of fruit into the classifier, and then compare the label that the classifier predicts with the actual true label of the fruit type. So, here's a very important point though, *if we use one of our labeled fruit examples in the data that we use to train the classifier, we can't also use that same fruit sample later as a test sample to also evaluate the classifier*. Why is that? Well, a key ability that our classifier needs to have is that it needs to work well on any input sample, any new pieces of fruit that we might see in the future, not just on the ones that we have on our training set. Because our classifier could simply memorize every sample in the training set, it'd be pretty trivial to just give back the correct label for any one of the same samples later, right? So, measuring the classifier's performance later using the same samples that we've used to train it in the first place doesn't tell us anything about how well the classifier is likely to work for a fruit that we haven't seen before. It will only tell us what we already know about what's in the training set.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/038.png' alt='038'/>

So since our only source of labeled data is the dataset we've been given, to estimate how well the classifier will do on future samples, what we'll do is split the original dataset into two parts. We'll have an array of labeled samples called the **training set** that will be used to train the classifier. And then we'll hold out the remaining labeled samples and put them into a second separate array called the **test set** that will be used to then evaluate the trained classifier. So to create training and test sets from a input dataset, `Scikit-learn` provides a handy function that will do this split for us, called, not surprisingly, `train_test_split`. And here's an example of how we're going to use it.

```python
# For this example, we use the mass, width, and height features of each fruit instance
X = fruits[['mass', 'width', 'height']]
y = fruits['fruit_label']

# default is 75% / 25% train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)
```

This function randomly shuffles the dataset and splits off a certain percentage of the input samples for use as a training set, and then puts the remaining samples into a different variable for use as a test set. So in this example, we're using a 75-25% split of training versus test data. And that's a pretty standard relative split that's used. It's a good rule of thumb to use in deciding what proportion of training versus test might be helpful. As a reminder, when we're using Scikit-learn, we'll denote the data that we have using different flavors of the **variable X**, capital X, which is typically a two dimensional array or data frame. And the notation we'll use for labels will be typically based on **lowercase y**, which is usually a one dimensional array, or a scalar. Now, note the use of the random state parameter in the `train_test_split function`. So this random state parameter provides a seed value (random_state=0) to the function's internal random number generator. If we choose different values for that seed value, that will result in different randomized splits for training and test. So, if we want to get the same training and test split each time, we just make sure to pass in the same value of the random state parameter. And so here, we're going to set that parameter to zero for all our examples. The training test split function will put the training set here into **X_train**, the test set into **X_test**, the training labels into **y_train**, and the test labels into **y_test**. So this is a 75-25 partitioning of the original data into these two parts.

And this is the variable naming **convention** we'll use for pretty much all of our coding. We'll put the rows of the data without the label, the training instances into this capital X variable, and the list of corresponding labels for those rows into a variable called lowercase y. When using the training set and the test set, we'll then use X_train that holds the training instances to train the classifier, and X_test to evaluate the classifier after it's been trained. And we're going to show a short snippet of code here now that illustrates how to do that.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/039.png' alt='039'/>

So here we can see the results of the function, applying this `train_test_split function`, you can see that it has indeed split our fruit dataset into training and test sets with the correct proportion of samples. Now that we have a training and a test set, we're ready for the next step. And we'll look now into more depth at the data itself before we proceed with giving it to a machine learning algorithm.