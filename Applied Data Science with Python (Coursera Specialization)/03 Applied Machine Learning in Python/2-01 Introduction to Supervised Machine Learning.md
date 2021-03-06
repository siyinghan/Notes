# 2-1 Introduction to Supervised Machine Learning

In the previous module, you saw a basic sample of **supervised machine learning** using a **k-nearest neighbor classifier**, classifying different types of fruit based on their various physical properties. Machine learning algorithms of this type are called **supervised learning algorithms** because they use *labeled examples* in the training set to learn how to predict the labels for new, previously unseen examples. The **supervised** aspect refers to *the need for each training example to have a **label*** in order for the algorithm to learn how to make accurate predictions on future examples. This is in contrast to **unsupervised machine learning** where we *don't have labels for the training data examples*, and we'll cover unsupervised learning in a later part of this course.

This week, we'll explore **supervised learning** in a bit more depth, going beyond **k-nearest neighbors classifiers** to several other widely used **supervised learning algorithms**. Because this is an applied machine learning course, we're not going to cover too much of the mathematical derivation or the detailed innerworkings of these algorithms. For that, you can check out a number of more technical machine learning courses such as Andrew Ng's excellent course on Machine Learning on Coursera. Instead, we'll focus on some higher-level goals. *How to apply a number of specific supervised machine learning algorithms* and *how to interpret their results for important tasks*. This will include understanding:

- how supervised learning algorithms estimate their parameters from data,
- how the train model makes predictions for new instances，
- the strengths, weaknesses and best scenarios to apply a particular method,
- and how to use the method with its parameter settings in `Python` programs using `scikit-learn`.

Across all of these algorithms we'll discuss some general principles that are critical to machine learning, like:

- the issue of overfitting,
- and how overfitting relates to a models complexity,
- and which parameters typically can be used to control model complexity in order to obtain good performance on previously unseen data.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/060.png' alt='060' width='650px'/>

In this module we won't have time to cover all the different parameters for the various **supervise learning methods**. So we'll focus on a small number of the most important parameters. The full details of all the supervised algorithms we'll cover this week are in the excellent online documentation that's provided with **PsychEd Learn**. Which we've included links to in the supplemental material for this course. Before we continue, let's review some basic terms.

So, on the right, here I'm showing the adapt of the first few rows of the **fruit dataset** that you worked with last week.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/061.png' alt='061' width='650px'/>

The first term that we would be using a lot is **feature representation**. And as you might recall what that means is *taking an object like a piece of fruit and converting it into numbers that the computer can understand*. So in this dataset, the **feature representation** for a piece of fruit consists of these columns, the **mass**, **width**, **height**, and **color_score**. These are the things that will be used as the features in the various machine learning algorithms that we'll be applying to try to predict the label of a piece of fruit.

So typically each column in the dataset here corresponds to a different feature that's associated with each instance. So I used the term instance or sample or example somewhat interchangeably. Most of the time I'll be talking about **instances** or **samples**. So each row of this dataset corresponds to one piece of fruit or one specific data instance per sample. When we work with these instances in `Python`, the convention we'll be using is that we'll put the all the variables that represent the features in this variable **capital X** here. So **capital X** refers to *all the feature columns that will be going into as the inputs for the predictor*.

And then we have the very important concept of a **label**. So each **instance** here, each piece of fruit has a **label** that's what's assigned by a human in this case, and the label is an example of a **target value**. So in classification, the target value is label of an object and then regression, it's the particular continuous value you might want to protect from the inputs. And we use **lowercase y** in `Python` for the variable name to hold the target values associated with each instance. So if you look at the dataset as being say this big block here. Typically that'll be a column of labels and then a matrix of multiple columns holding the features that we will be using. And then we have a couple of columns in here. The fruit name and the fruit subtype. That are used only for labeling purposes to make things like plots, more readable for humans. The things that go into the actual machine learning algorithms are the label for training through the Y variable and the features, the mass with height and color score that are in the X variable.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/062.png' alt='062' />

Another concept that we saw from our first example. The concept of **training and test sets**. So by that we mean a just to recap we think of the entire data said here is a rectangle So this could be the fruit which is showed previously. We typically sign a chunk of the original dataset and make that to **training set**, and then we reserve typically a smaller portion, that's the **test set**. So the default split in scikit learn is **typically 75, 25**. The function `train_test_split` here is a very handy function in` scikit-learn` that takes the original set of **features X** and the **labels y**. And does this partitioning into a training and test set. So the variables that we'll be using to denote training and test set are `X_train` for the training set features and `y_train` for the training set labels. And then `X_test` for the test set features and `y_test` for the test set labels.

Once we pass the training data into a classifier, so as you recall, we can create here `KNeighborsClassifier` by invoking this constructor and passing it the number of neighbors that we want the algorithm to use. The training set is used to estimate the parameters for a model. In `scikit-learn`, there's an object called an `estimator`, which is either **classify** or **regressor** for example. And the goal of this `estimator`, this model, is to *learn how to classify or predict target values for new data instances*. So the procedure where we pass in a training set to learn those parameters that are internal to the estimator, is called a **model fitting**, and the result of model fitting is a **trained model**. So an example of that in the code here is after we create the `knn` variable that has the `KNeighborsClassifier` objected, we use the `fit` method on the **training data** and the **training labels**. To update the internal state of the `knn` object, and that's the training process. So after that line of code is finished running, the internal state of the knn classifier has been updated to reflect the training data's influence on the internal parameters of the knn classifier, and now it's ready to be used.

So, **evaluation methods** are typically the next step where after we've `fit` the model, we want to see how well it actually does do on the test data. So in week four of the course we're going to cover in detail. Different ways of evaluating **classifiers** and **regressions**. But for now, we'll look at accuracy. So the `score` method applied to the classifier will take the test data in `X_test` and `y_test` and output the accuracy of this particular classifier on the test set.

And then finally we can also apply the `predict` method to the `knn` end object. To get the label for previously unseen instances.

So these are the terms that would be using throughout the course and we will also be maintaining a fairly consistent use of these variable names throughout all the Python code that we use.

<br/>

**Supervised learning** can be divided into two different types of tasks, **classification** and **regression**. Both classification and regression take a set of training instances and learn a mapping to a target value. For classification, the target value is a **discrete class value**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/063.png' alt='063' width='650px'/>

**For example**, a binary classification problem has a two types of target values. A 0 representing the negative class or 1 representing the positive class. An example of binary classification might be trying to detect a fraudulent credit card transaction. The transaction is either *valid* or invalid.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/064.png' alt='064' width='650px'/>

The second type of classification problem is known as **multi-class classification**, where the target value is more then just a yes or a no, or 1 or 0, it could be one of **a set of discrete values**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/065.png' alt='065' width='650px'/>

**For example**, the labeling fruit example that we saw from the first part of the course is an example of multi-class classification because the object that we're trying to predict the label for can only have one of the possible label types. Something couldn't be for example both an apple and an orange.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/066.png' alt='066' width='650px'/>

The third category of classification is called **multi-label classification** with our **multiple target values**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/067.png' alt='067' width='650px'/>

**For example**, we might want to take a web page and label all the different topics discussed on that page as shown in this example. Here we see a page from Microsoft research where the multi-label classification has decided that the labels *computing*, *science*, and so forth are applicable.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/068.png' alt='068' width='650px'/>

<br/>

In contrast to **classification**, for **regression**, the target we're trying to predict is a **continuous value**. For example, *a model that predicts the market price of a house, given how many rooms it has, where its located, the size of the land that it sits on and so forth, would be a regression problem*. Because the market price is continuous, otherwise known as a real value variable.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/069.png' alt='069' width='650px'/>

You can tell what type of **supervisor learning method** you should apply to a given problem by thinking about the meaning of the **target value**. Does the target value represent something that's one of a set of mutually exclusive class values as in the case of assigning a label to a piece of fruit? Or whether or not a transaction is fraudulent? If so, it's a classification problem. On the other hand, if the target is a real value quantity like **cost**, or **income**, or **height** then it can be treated as a **regression problem**. Finally, we'll see that many supervised learning methods come in both flavors of classification and regression.

For example, **support vector classifiers** which we'll cover shortly also has a regression version called not surprisingly **support vector regression**. In this course, we'll cover both **classification** and **regression** methods, although we'll spend the majority of our time on classification. Since that represents a big set of important machine learning tasks, and because classification involves some additional concepts and methods especially in areas like evaluation that aren't needed as much for regression.

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/070.png' alt='070' width='650px'/>

To start with, we'll look at two simple but powerful prediction algorithms. **K-nearest neighbours**, which we saw in week one and **linear model fitting using least-squares**. These two prediction methods represent two complimentary approaches to supervised learning. K-nearest neighbors doesn't make a lot of assumptions about the structure of the data and gives potentially accurate, but **sometimes unstable predictions**. And by unstable I mean that it can be sensitive to small changes in the training data. On the other hand, linear models make strong assumptions about the structure of the data. In other words, that the target value can be predicted just using a weighted sum of the input variables, a linear function. It can get stable, but potentially **inaccurate predictions**.

In addition to k-nearest neighbors and linear models, we'll cover a variety of widely used supervised learning methods for classification and regression. Including **decision trees**, **kernelized support vector machines** and **neural networks**. For each method we'll explore how it works at a high level without going into too much mathematical details. We'll also look at what kind of feature preprocessing is typically needed. And for almost all of the supervised learning algorithms we'll look at. There are one or more parameters that control its model complexity, so we'll see how to set these parameters to help avoid **under and over fitting**.

Finally, we'll discuss the positives and negatives of each supervised learning approach to help understand what are the best scenarios in which to apply or not apply that particular method.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/071.png' alt='071' width='650px'/>

One consistent pattern you'll see as we look at all these different methods, is the relationship between **model complexity** and **model accuracy**, as shown in this plot. The relationship is different depending on whether the classifier performance is measured on the training set, what is labeled here as **training set score**, or in the test set labeled here as **test set score**. When measuring performance against the training set, the same one that was used to train the classifier, this plot shows that as a model's complexity increases, so think of the k and n classifier with k decreasing. And with more and more highly variable and a detailed decision boundaries. The model's accuracy and the training set trends upward as the more complex models fit the training data better and better. However, when the same trained model is evaluated on the held out test set, there's typically an initial accuracy gain from the increasing model complexity up to some optimal point. But then a decrease in test set accuracy as the increasingly complex models begin to overfit too specifically to the training data, and don't capture more global patterns that help it generalize well to unseen testing. Now the specifics of these trends will vary from situation to situation, but overall we'll see this pattern across the supervised learning methods that we'll examine.

You'll be hearing a lot about models in this course. What is a **model**? Well, it's *a specific mathematical or computational description that expresses the relationship between a set of input variables and one or more outcome variables that are being studied or predicted*. In statistical terms the **input variables** are called **independent variables** and the **outcome variables** are termed **dependent variables**. In Machine Learning we use the term **features** to refer to the input, or independent variables. And **target value** or target label to refer to the output, dependent variables. Models can be either used to understand and explore the structure within a given dataset, as we'll see in unsupervised learning. Or in the case of supervised learning methods, our goal is to develop predictive models that can accurately predict the outcome. In other words, the target value or label for previously unseen input data.