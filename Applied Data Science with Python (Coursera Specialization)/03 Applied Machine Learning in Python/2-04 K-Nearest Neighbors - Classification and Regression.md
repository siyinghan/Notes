# 2-4 K-Nearest Neighbors: Classification and Regression

Let's revisit the first example of machine learning that we encountered in week one, **k-Nearest Neighbor** models. Those were a good starting point to continue our exploration of supervised learning because they're simple to understand and can be used for both **classification** and **regression**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/088.png' alt='088' width='600px'/>

Let's recall that, for **classification**, the **k-Nearest Neighbor Classifier** simply memorizes the entire training set. And then to classify a new instance does 3 steps.

- First, it finds the **k-Nearest most similar instances** to the new instance in the training set.
- Then it gets the labels of those training instances.
- And then it predicts the label of the new instance as a function of the nearby training labels typically by a simple majority vote.

Here's how a **k-Nearest Neighbor Classifier** using only one nearest neighbor, that is with **k = 1**, makes these predictions for the simple binary synthetic dataset.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/089.png' alt='089' width='410px'/>

So as you might recall from week one where we applied a nearest neighbors classifier to our multi-class fruit dataset. Here we're applying the nearest neighbors classifier to our simple **binary classification problem**. Where the points in class zero are labeled with yellow dots and the points in class one are labeled with black dots. And just as we did for the week one problem with fruit classification, here we're also showing how the entire feature space is broken up into different decision regions according to the predictions that the k-Nearest Neighbor Classifier would make at each point in the decision space. So for example, a point out here in the yellow region represents a point that the classifier would classify as class zero. And a point, let's say, over here, the classifier would classify as class one. So because this is a one nearest neighbors classifier, to make a classification prediction for any given query point, the Classifier simply looks back into its trading set. So these points here represent all the points on the training set. So for any given point, let's say here, The Classifier would simply find the training point that's closest, namely this one, and assign the predict a class to simply the class of the nearest point in the training set. Likewise, if we have a point over here. The nearest point in the training says actually this point right here that has a class zero label and so that point would get assigned a class zero. And in fact, this whole region right here represents all the points that are closer to the class zero training point than any of the other class one training points. So this whole region here represents a one nearest neighbors prediction of class zero. So the k-Nearest Neighbor's Classifier with k = 1, you can see that the **decision boundaries** that derived from that prediction are quite **jagged** and have **high variance**. This is an example of a model, classification model, it has high model complexity. And in fact, you can see that the one nearest neighbors classifier is **overfitting** the training data in this case. It's trying to get correct predictions for every single training point while ignoring the general this trend between the two classes, namely that most of the yellow points are in this side of the future space and most of the black points are on this side. So the **one nearest neighbor's classifier** can be said to be **overfitting** in this case.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/090.png' alt='090' width='410px'/>

And here is what happens when we increase k from 1 to **11**. Now the classifier must combine the votes of the 11 nearest points, not just 1. So single training data points no longer have as dramatic an influence on the prediction. The result is a **much smoother decision boundary**, which represents a model with **lower model complexity** where the decision boundary has much less variance. Actually if we increased k even higher to be the total number of points in the training set, the result would be a single decision region where all predictions would be the most frequent class in the training data.

As we saw for the fruit data set, k-Nearest Neighbor Classifiers can be applied to any number of classes, not just 2.

```python
from adspy_shared_utilities import plot_two_class_knn

X_train, X_test, y_train, y_test = train_test_split(X_C2, y_C2,
                                                   random_state=0)

plot_two_class_knn(X_train, y_train, 1, 'uniform', X_test, y_test)
plot_two_class_knn(X_train, y_train, 3, 'uniform', X_test, y_test)
plot_two_class_knn(X_train, y_train, 11, 'uniform', X_test, y_test)
```

The code for this example in the notebook uses a special function, in the `shared_utilities` library for this course, called `plot_two_class_knn`. If you run this code and compare the resulting training and test scores for k equals 1, 3, and 11, which are shown in the title of each plot, you can see the effect of model complexity on a models ability to generalize.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/091.png' alt='091' width='500px'/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/092.png' alt='092' width='500px'/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/093.png' alt='093' width='500px'/>

In the k = 1 case, the training score is a perfect 1.0. But the test score is only 0.80. As k increases to 3, the training score drops to 0.88 but the test score rises slightly 2.88, indicating the model is generalizing better to new data. When k = 11, the training score drops a bit further to 0.81, but the test score even better at 0.92, indicating that this simple model is much more effective at ignoring minor variations in training data. And instead capturing the more important global trend in where the classes tend to be located with the best overall generalization performance as a result.

<br/>

The **nearest neighbors** approach isn't useful just for classification. You can use it for **regression** too. So here are three plots that show the same simple **regression problem** with one input feature and the corresponding target values in the training data.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/094.png' alt='094' />

The left most plot here, this one, shows just the original training data points. And the middle and right plots show the predictions made by k and n regression algorithm, when k = 1 and k = 3. So in these plots, you can see the training points are actually in green. These **green circles** are the **training points** and the **blue triangles** are the **output of the k-nearest neighbor regression** for any given input value of x. So for example the knn regression prediction for this point here is this y value here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/095.png' alt='095' width='300px'/>

So how did the nearest neighbors regressor compute this value. Well I did it in similar way to what we saw for classification. So if the query point we're interested in is predicting value associated with this x value, we simply find the training point that has the X value that's closest to this query point. So in this case, that would be this training point.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/096.png' alt='096' width='300px'/>

And because this is a one nearest neighbor problem, we simply take the target value associated with this training point and use that as the output target for the query point. Similarly, if this were the query point here then the nearest neighbor in the training set would be this point here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/097.png' alt='097' width='300px'/>

And so the output prediction for this particular X-value would be the target value of the nearest neighbor or this value that's just above 100. And so, if we do that for all these different X values, we'll get these different predictions using the one nearest neighbor approach.

Similarly, if we look at the **k = 3** case, where we now look at three nearest neighbors, let's take this example here of -1.25, let's say. Well, what are the three training points that have x values closest to -1.25? They would be this training point, that training point and this training point.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/098.png' alt='098' width='300px'/>

Now with regression, what we do is instead of taking a majority vote, we don't have class values here as targets, we have continuous values. So we can average these three target values. And if we do that, we find that the output, when the query point is this X-value, is going to be **the average of the y-values of the three nearest training points**, or this value here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/099.png' alt='099' width='300px'/>

Similarly, if we have a query point that is here. Then the three nearest neighbor points are here, here and here. And the average target value of these three training points is something like this.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/100.png' alt='100' width='300px'/>

Here's the corresponding code in the notebook that produced these regression plots.

```python
from sklearn.datasets import make_classification, make_blobs

# synthetic dataset for classification (binary) 
plt.figure()
plt.title('Sample binary classification problem with two informative features')
X_C2, y_C2 = make_classification(n_samples = 100, n_features=2,
                                n_redundant=0, n_informative=2,
                                n_clusters_per_class=1, flip_y = 0.1,
                                class_sep = 0.5, random_state=0)
plt.scatter(X_C2[:, 0], X_C2[:, 1], c=y_C2,
           marker= 'o', s=50, cmap=cmap_bold)
plt.show()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/102.png' alt='102' width='500px'/>

```python
from sklearn.neighbors import KNeighborsRegressor

X_train, X_test, y_train, y_test = train_test_split(X_R1, y_R1, random_state = 0)

knnreg = KNeighborsRegressor(n_neighbors = 5).fit(X_train, y_train)

print(knnreg.predict(X_test))
print('R-squared test score: {:.3f}'
     .format(knnreg.score(X_test, y_test)))
```

```
[ 231.71  148.36  150.59  150.59   72.15  166.51  141.91  235.57  208.26
  102.1   191.32  134.5   228.32  148.36  159.17  113.47  144.04  199.23
  143.19  166.51  231.71  208.26  128.02  123.14  141.91]
R-squared test score: 0.425
```

These use the `KNeighborsRegressor` Class, which like the classification case, takes the end neighbor setting as a key parameter.

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/101.png' alt='101' width='600px'/>

Because the target values in a regression problem are continuous as compared to the discrete values that we see for classifier target labels. To assess how well a regression model fits the data, we use a regression score called **r-squared** that's between 0 and 1. We'll cover some additional types of regression evaluation scores later in the course. For the **r-squared** value, a value of **1** corresponds to the **best possible performance**. A model that makes perfect predictions. A value of **0** corresponds to a model that makes a constant value prediction that's always **just a mean value** of all the training target values. The r-squared value is sometimes known as the **coefficient of determination**.



Just as we did for classification, let's look at the connection between **model complexity** and **generalization ability** as measured by the **r-squared** training and test values on the simple regression dataset. The series of plots on the notebook shows how the KNN regression algorithm fits the data for k = 1, 3, 7, 15, and in an extreme case of k = 55. It represents almost half the training points. We can see the same pattern in model complexity for k and N regression that we saw for k and N classification. Namely, that small values of k give models with higher complexity. And large values of k result in simpler models with lower complexity. Starting on the left when k = 1, the regression model fits the training data perfectly with a r-squared score of 1.0. But it's very bad at predicting the target values for new data samples, as reflected in the r-squared test score of only 0.155. As the value of k increases, which we can see acts to smooth out these local variations to capture more of the global trend. Again the training set score drops, but the model gets better at generalizing to new data and the test score goes up as K increases. Finally in this series, the model with k = 15 has the best test set performance, with an r-squared score of 0.485. Increasing k much further however to k = 55, results in both the training and test set scores dropping back down to lower levels, as the model now starts to under-fit. In other words, it's too simple to do well, even on the training data. The pro's of the nearest neighbor approach are that it's simple and easy to understand why a particular prediction is made. A k-nearest neighbor approach can be a reasonable baseline against what you can compare more sophisticated methods. When the training data has many instances, or each instance has lots of features, this can really slow down the performance of a k-nearest neighbors model. So in general, if your data set has hundreds or thousands of features, you should consider alternatives to k-nearest neighbors models, especially if your data is sparse. Meaning that each instance has lots of features, but most of them are zero. So to sum up, and as a review of what we saw in week one. The two key parameters for both regression and classification in nearest neighbors models are naturally n-neighbors which controls the value of the number of neighbors to consider and thus the model complexity, as we saw. And the metric parameter which controls the distance function between points and thus which points are considered as nearest in finding neighbors. We didn't explore the metric parameter here and that's beyond the scope of this course. But in most cases, the default Euclidean setting words pretty well with most datasets.