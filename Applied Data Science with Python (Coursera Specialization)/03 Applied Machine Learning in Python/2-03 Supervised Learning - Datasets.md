# 2-3 Supervised Learning: Datasets

**Material**: [fruit_data_with_colors.txt](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Material/fruit_data_with_colors.txt), [adspy_shared_utilities.py](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Material/adspy_shared_utilities.py)

<br/>

To explore different **supervised learning algorithms**, we're going to use a combination of small synthetic or artificial datasets as examples, together with some larger real world datasets. `scikit-learn` has a variety of methods in the `sklearned.datasets` library to create **synthetic datasets**. The synthetic dataset will use, for illustration purposes are typically low dimensional examples. Because they only use a *small number of features, typically one or two*. This makes them easy to explain and visualize. Many real world datasets, on the other hand have a *higher dimensional feature space*. In other words they have dozens, hundreds, or even thousands, or millions of features. So some of the intuition we gain from looking at low dimensional examples doesn't always translate to high dimensional datasets, and we'll discuss that a bit more later. For example, **high dimensional data sets** in some sense have most of their data in corners with lots of empty space and that's kind of difficult to visualize. We'll go through some examples later in the course. But the **low dimensional examples** are still useful so that we can understand things like how a model's complexity changes with changes in some **key parameters**.

<br/>

So for basic regression we'll start with the simple problem that has one informative input variable. **One noisy linear output** and **100 data set samples**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/083.png' alt='083' width='500px'/>

Here's a plot of a data set using **scatter plot** with each point represented by one dot. The x-axis shows the **future value**, and the **y-axis** shows the **regression target**. To create this we use the make regression function in `sklearned.datasets`. Here is the code in the notebook.

```python
from sklearn.datasets import make_classification, make_blobs
from matplotlib.colors import ListedColormap
from sklearn.datasets import load_breast_cancer
from adspy_shared_utilities import load_crime_dataset

cmap_bold = ListedColormap(['#FFFF00', '#00FF00', '#0000FF','#000000'])

fruits = pd.read_csv('fruit_data_with_colors.txt', delimiter='\t')

feature_names_fruits = ['height', 'width', 'mass', 'color_score']
X_fruits = fruits[feature_names_fruits]
y_fruits = fruits['fruit_label']
target_names_fruits = ['apple', 'mandarin', 'orange', 'lemon']

X_fruits_2d = fruits[['height', 'width']]
y_fruits_2d = fruits['fruit_label']

# synthetic dataset for simple regression
from sklearn.datasets import make_regression
plt.figure()
plt.title('Sample regression problem with one input variable')
X_R1, y_R1 = make_regression(n_samples = 100, n_features=1,
                            n_informative=1, bias = 150.0,
                            noise = 30, random_state=0)
plt.scatter(X_R1, y_R1, marker= 'o', s=50)
plt.show()
```

To illustrate **binary classification** we will include a simple two class dataset with two informative features.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/084.png' alt='084' />

Here's a scatterplot showing each data instance as a dot with the **first feature value** corresponding to the **x-axis**. And the **second feature value** corresponding to the **y-axis**. The color of a point shows **which class that data instance is labeled**. I'm calling this dataset simple because it has only two features, both of which are informative.

In this case, these two classes are approximately **linearly separable**, which means that a **basic linear classifier** placed between them does a pretty good job of discriminating the points in the two classes. So turning to the notebook, to create this data set we used to make classification function in `sklearned.datasets`. Creating 100 points that roughly group the data samples into one cluster per class, with here a 10% chance of randomly flipping the correct label of any point just to make it a little more challenging the classifier.

<br/>

We'll also look at a more **complex binary classification problem** that uses **two features**. But where the two classes are not really linearly separable, instead forming into various clusters in different parts of the feature space. This dataset was created in two steps. First using the make_blobs function in SK learn datasets to randomly generate 100 samples in 8 different clusters. And then by changing the cluster label assigned by make_blobs, which is a number from 1 to 8, to a binary number by converting it using a modulo 2 function. Assigning the even index points to class 0 and odd index points to class 1. To illustrate multi-class classification, we'll use our familiar fruits dataset, which, as you may remember has four features and four possible target labels. Here on the left, I'm showing the array of scatter plots that we saw in week one that shows the relationship between all possible pairs of features and the class labels, with the distribution of values for each feature along the diagonal. To illustrate a real-world regression problem, we'll use a dataset derived from the communities and crime dataset in the UCI repository. Our dataset uses a subset of the original features and target values. Which were originally created from combining several U.S. government data sources, like the U.S. census. Each data instance corresponds to a particular geographic area, typically a town or a region of a city. Our version of this dataset has 88 features that encode various demographic and social economic properties of each location. With 1994 location data instances. The target value that we'll try to predict is the per capita violent crime rate. To use this data set, we use the load_crime_dataset function that's included with the share utilities module for this course