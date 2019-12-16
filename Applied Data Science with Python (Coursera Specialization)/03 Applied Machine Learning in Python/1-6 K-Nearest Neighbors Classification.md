# 1-6 K-Nearest Neighbors Classification

Now that we've gotten a sense for what's in our data set, as a simple example to get started, we're going to use this data set to train a **classifier** that will automatically identify any future pieces of fruit that might come our way. Based on the features available to the classifier such as the object's color, size and mass. To do this, we'll use a popular and easy to understand type of machine learning algorithm known as **k-nearest neighbors** or **k-NN**. *The K-Nearest Neighbors algorithm can be used for* **classification** *and* **regression**. Though, here we'll focus for the time being on using it for classification. **k-NN classifiers** are an example of what's called *instance based or memory based supervised learning*. What this means is that instance based learning methods work by memorizing the labeled examples that they see in the training set. And then they use those memorized examples to classify new objects later. The **k** in **k-NN** refers to **the number of nearest neighbors** the classifier will retrieve and use in order to make its prediction.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/043.png' alt='043' width='650px'/>

In particular, the k-NN algorithm has **three steps** that can be specified.

- First of all, when     given a new previously unseen instance of something to classify, a **k-NN classifier** will look into its set of memorized training examples to find the k examples that have closest features. And we'll talk about what closest means in a minute.
- Second, the classifier will look up the class labels for those **k-Nearest Neighbor** examples.
- And then once it's done that, it will combine the labels of those examples to make a prediction for the     label of the new object. Typically, for example, by using simple majority vote.

Let's look at a visual example of a **k-NN classifier** that is based on our **fruit data set**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/044.png' alt='044' width='600px'/>

So what I've done here is taken our training set and plotted each piece of fruit using two of its features. The **width** and the **height**. These two features together form what is called the feature space of the classifier. And I've shown each data point's label using the colors shown in the legend. So as you can see, there are four different colors here that correspond to the four types of fruit that are in our data set. These broad areas of color show how any point, given a width and height, could be classified according to a one nearest neighbor rule. So, in other words, I've set **k = 1** here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/045.png' alt='045' width='350px'/>