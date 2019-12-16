# 1-2 Key Concepts in Machine Learning

Machine learning tasks, including the ones I've described as examples. Credit card fraud detection, movie recommendations, speech recognition, and so on. Can be categorized into two main types.

The first type is known as **supervised learning**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/013.png' alt='013' width='700px' />

And here our goal is to predict some output variable that's associated with each input item. So if the output is a category a finite number of possibilities such as a fraudulent or not fraudulent prediction for a credit card transaction. Or maybe it's the English word associated with an audio signal for speech recognition. We call this a **classification problem within supervised learning**, and the function that we learn is called the **classifier**. If the output variable we want to predict is not a category, but a real valued number like the amount of time in seconds it would likely take a car to accelerate from 0 to 100 kilometers per hour. We call that **regression problem**. And we're learning something called a regression function.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/014.png' alt='014' width='700px' />

More formally we typically denote a table of data items using capital letter X and there's one data item per row. And the labels that we associate with each item are stored in the variable y. And our goal is to learn some function that maps data item in X to a label in Y. And to do this, the system's given a set of label training examples, of inputs X sub i and outputs Y sub i. And this set of label training examples is what's used to identify the function that best maps the input to the desired output.

For example, if the supervised learning problem is image recognition. This involves building a **classifier** where the input X sub i could be a set of pixels that describe a single image. And the desired label Y sub i might be the label of the object in the image.

Now there're many algorithms that scientists have developed that can do supervise learning. That could be used to estimate this function F from the training data, and we'll cover a number of those algorithms in the course.

Supervised learning needs to have this training set with labeled objects in order to make its predictions. But if the whole point is to predict these labels, where does this initial set of label items come from?

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/015.png' alt='015'/>

The answer is that the training labels are typically provided by human judges. Now obtaining labels for some problems can be easy or difficult, depending on how much labeled data is needed. The level of human expertise or expert knowledge that is needed to provide an accurate label. And the complexity of the labeling task among other factors. Now, the use of **crowdsourcing platforms**, like Amazon's Mechanical Turk, or Crowd Flower or others. Have been a significant source of explicitly provided labels from human workers where customers with machine learning tasks that need labeling can connect with groups of workers that can provide labels using human intelligence.

So those are more explicitly obtained labels. We can also obtain implicit labels. So, for example, if a search engine detects a user clicking on a result link and then sees no more activity for another minute or two before the user comes back to the search engine. The system might use that activity as a kind of an implicit label for that page. In other words, if the user took some time to visit the page, it was more likely that that page was relevant to their query. 

The second major class of machine learning algorithms is called **unsupervised learning**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/016.png' alt='016' width='700px' />

In many cases we only have input data, we don't have any labels to go with the data. And in those cases the problems we can solve involve taking the input data and trying to find some kind of useful structure in it.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/017.png' alt='017' width='700px' />

Now what do I mean by **structure**? Well typically this means finding interesting clusters or groups within the data. So once we can discover this structure in the form of clusters, groups or other interesting subsets. The structure can be used for tasks like producing a useful summary of the input data maybe visualizing the structure. For example, if you run an e-commerce site that sells products to customers. Let's suppose you've got many thousands or even millions of customers. You might want to know if you can **categorize or group the customers into different types**. For example, there might be power users who use more advance features of the site. There might be quick browser-type users who only look for a cheap discount and stay for very little time on the side itself. There could be sort of careful researcher type users who spend a lot of time comparing different items. And if you could take your data of how people interact with the site and use unsupervised learning to discover these different groups. You can imagine then maybe tailing your site's offerings to each group so that prove the chance that a user from that group would maybe purchase a product or have a better experience using your site. Now you don't know how many groups there are out there ahead of time or even what they look like. And you don't have any label examples. And so this is a classic example of an unsupervised learning problem.

Another type of unsupervised learning problem that is very important is something like **flagging abnormal access to a web server**. So for security reasons, you might want to be notified if a website user is making requests that could be a cyber attack, or is somehow very different from typical user behavior on your site. Since there can be many different types of hacking or intrusion attempts to break into the server or exploit in some way. We don't have reliable training labels that we could use to train the classifier using supervised learning. Instead, we need unsupervised approach that allows us to perform something called **outlier detection**. That doesn't assume future attacks will be of the same form as previous attacks. But that does assume features of attacks on the site will look different some how than the average users behavior.

Okay, so suppose you have a situation where you think machine learning might be applicable, either using a **supervised** or an **unsupervised** approach. How would you apply Machine Learning to solve your problem?

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/018.png' alt='018' width='750px' />

Well, there're three basic steps and I'm going to use classification as my typical Machine Learning scenario. So I'll often just use the term classifiers as an example of a machine learning task. But what I am about to describe applies to other forms of supervised learning, like regression, that we'll cover later, or unsupervised learning like clustering as well.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/019.png' alt='019' width='230px' />

So the first step in solving a problem with machine learning is you have to figure out how to **represent** the learning problem in terms of something the computer can understand. You need to be able to take your data or even formulate the description of your object that you're interested in recognizing, for example, in a way that you can use input to an algorithm. And you also need to decide what type of learning algorithm to apply to this data. For example, there're many different ways you could represent an image. Typically, it's represented as an array of colored pixels. There could also be metadata associated with the image. You could think about how you might represent a credit card transaction if you want to do fraud detection. So that might be represented by the time, the place and amount of a transaction. So you need some way, some representation of the data you have and the choice of what kind of algorithm you want to apply to the data.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/020.png' alt='020' width='230px' />

The second thing need to do is decide on an **evaluation** method that provides some type of quality or accuracy score. For the predictions or the output that is coming out of the machine learning algorithm typically I say classifier. So if you have any violation method this allows you to access and compare the effectiveness of different classifiers. So you can tell what classifiers are doing well, which are the good ones, and which are the bad ones for your particular problem. For example, a good classifier will have high accuracy that will make a prediction that matches the correct true label a high percentage of the time.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/021.png' alt='021' width='250px' />

The third thing you need to do in applying machine learning to solve a problem is. Once we've decided on how to represent the input data, the type of classifier and the evaluation method. We need to then search for the **optimal classifier** that gives the best evaluation outcome for that problem. And we'll go into all three of these areas in this course. And then, we'll use Python in this course as well to solve some specific examples. And we're about to see a concrete example of how we use machine learning at libraries in Python to solve a classification problem.

So let's go through these three three steps in a little more detail now. Let's first talk about what it means to convert the problem into a **representation** that a computer can deal with. This involves two things.

* You need to convert each input object, which we often call a sample, into a set of features that describe the object.
* Second, we need to pick a learning model, typically the type of classifier that you want the system     to learn.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/022.png' alt='022'/>