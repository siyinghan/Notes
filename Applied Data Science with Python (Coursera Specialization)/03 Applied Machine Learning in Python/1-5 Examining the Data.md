# 1-5 Examining the Data

In general, if you're thinking about applying **machine learning** to a **data set**, it's a really good first step to actually look at the data set first, maybe using some simple visualization methods. Or even simply scrolling through to look at the various values in the different rows before proceeding. And there are several reasons for doing this.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/040.png' alt='040'/>

First, it's helpful to simply *get a sense for what's actually in the data set*. because it may be that in inspecting the features of each object, you might get a better idea of what type of cleaning or preprocessing still needs to be done to the data. And of the range of values or the distribution of values that is typical for each attribute or each feature. This initial exploration can be especially valuable when you're dealing with complex objects like text that may be represented by many features that are extracted using a series of several pre-processing steps.

- For example, you might discover that the data set you got has a single column with person's name that still needs to be split into two separate first and last name columns.
- For example, if you're using the name as one of the prediction feature, that might be important.

Second, you might *notice missing or noisy data*. Or maybe some specific inconsistencies, such as the wrong data type being used for a column. Incorrect or inconsistent units of measurement for a particular column, particular feature. Or maybe you'll notice that there aren't enough examples of a particular labeled class.

- You might notice, for example, that some measurements of a person's weight. Let's say you're doing a health application with a patient record for each row. Some might accidentally have the weight in grams instead of kilograms and so forth. And that can make obviously a huge difference in how accurate your results are.

So inspecting and visualizing the data will help you detect and understand these potential source of noise or errors.

And finally, it might turn out that for your data set, *your problem is actually solvable without machine learning*. Now, this doesn't happen all that often. But if it does, you can save yourself considerable time by simply looking at what data exists in your data set. So one scenario, your data set might actually contain a feature of that, is clearly a strong indicator of the label that you want to predict.

- For example, if your goal was to predict whether a house's location was in New York City versus San     Francisco based on attributes like its sales price, its elevation above sea level, how big its rooms are and so forth. It could be that your data set might also include, let's say a URL to a photo of the house. And that image might contain GPS coordinates to the house within its metadata. Or maybe the URL encodes location in a slightly non-obvious but human recognizable way that you can pick out. And you solve your problem just by looking at the data.

So, as I said, this scenario isn't all that common, but it does happen. And so, a brief check of your data set could save you a lot of unnecessary work.

Okay, so we'll make sure we've got a training set from our original set using train test split. And we'll do all our initial visualization and feature analysis on this training set. And we're only going to use the test set for actually evaluating the classifier once it's trained. This complete separation of training and test sets is very important and we'll go into more depth later about specific reasons why it's important in a later class. So now that we have a training set selected, let's create some simple visualizations to look at how the features in the objects in the training set, in our case different fruits, relate to each other and to the labels. So with these visualizations, we get at least two major benefits.

- First, we can get an idea of the range of values that each feature takes on. And we could immediately see any unusual outliers that are very different from other points. And that might indicate noise or a missing feature or other problem with the data set.
- And second, we may be able to get a better idea how likely it is that a machine learning algorithm could do well at predicting the different classes. By seeing how well clustered and well separated the different types of objects are in **feature space**. So feature space refers to the representation of an object using specific features that are in certain columns of the data that we have. So for example, if the features for objects with the same label, for example, all the lemons have similar feature values, we should see a well-defined cluster appear in the visualization. While if the features for objects that have different     labels tend to be quite different, we should see these well separated into visibly different areas of the plot. So having objects whose classes are well defined and well separated in feature space is a good indication that suggests the classifier is likely to be able to predict the class label from the features with good accuracy.

Now the visualization techniques that I'll be showing here work well when you have a relatively small number of features, let's say *less than 20*. Later, when we cover **unsupervised learning**, you'll learn how to create visualizations of data sets that use a *very large number of feature dimensions*, so hundreds or even thousands or millions, to represent each object.

But for now, the first visualization tool we'll use is called a **feature pair plot** and that's shown here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/041.png' alt='041'/>

So this plot shows all possible pairs of features and produces a scatter plot for each pair, showing how the features are correlated to each other or not. Each point in the scatter plot represents a piece of fruit, colored according to the class it belongs to. And positioned using the parafeatures assigned to that scatter plot. Along the diagonal is a histogram showing the distribution of feature values for that feature. So in this pair plot, the dimensions shown here in order are, **height**, **width**, **mass**. And **color score** of the fruit examples in our training set. So the upper left corner of the histogram here shows the distribution of the **height feature** for all samples in the training set. And the scatter plot to its immediate right plots the **width** of each sample on the **x-axis** and the **height** of the sample on the **y-axis**. Just by looking at this pair plot, we can already see that some pairs of features, like the height and color score in the top right corner here, are *good for separating out different classes of fruit*. And this suggests that a classifier that was trained using those features could likely learn to classify the various fruit types reasonably well.

```python
# plotting a scatter matrix
from matplotlib import cm

X = fruits[['height', 'width', 'mass', 'color_score']]
y = fruits['fruit_label']
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

cmap = cm.get_cmap('gnuplot')
scatter = pd.plotting.scatter_matrix(X_train, c= y_train, marker = 'o', s=40, hist_kwds={'bins':15}, figsize=(9,9), cmap=cmap)
```

Here's the code that we'll use to create this plot, and let's run this now on our training set. Note that *a pair plot like this does not show interactions between all features that might exist, just between pairs of them*. So the plot itself may not show all the interesting relationships that do exist between the features. But it does give you a rough idea of some of the interactions that might exist.

We can also look at features that use a subset of three features by creating a three dimensional plot. And here's the code that we can use to do this:

```python
# plotting a 3D scatter plot
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = fig.add_subplot(111, projection = '3d')
ax.scatter(X_train['width'], X_train['height'], X_train['color_score'], c = y_train, marker = 'o', s=100)
ax.set_xlabel('width')
ax.set_ylabel('height')
ax.set_zlabel('color_score')
plt.show()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/042.png' alt='042'/>

So in this example, we plot different fruits using three coordinates. So here we'll the show the **width**, the **height**, and the **color score**. Here again, each point represents a single piece of fruit and its color according to its fruit label value. So in this 3D plot, you could actually rotate the plot along the various axes by holding down the mouse button and then dragging. And you can clearly see that the different fruit types are in pretty well-defined clusters that are also well-separated in feature space. So now that we've taken a look at the data, next we'll look at a simple prediction task for this data set in a bit more detail.