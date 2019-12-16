# 1-2 Key Concepts in Machine Learning

Machine learning tasks, including the ones I've described as examples. Credit card fraud detection, movie recommendations, speech recognition, and so on. Can be categorized into two main types.

The first type is known as **supervised learning**.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/013.png' alt='013' width='700px' />

And here our goal is to predict some output variable that's associated with each input item. So if the output is a category a finite number of possibilities such as a fraudulent or not fraudulent prediction for a credit card transaction. Or maybe it's the English word associated with an audio signal for speech recognition. We call this a **classification problem within supervised learning**, and the function that we learn is called the **classifier**. If the output variable we want to predict is not a category, but a real valued number like the amount of time in seconds it would likely take a car to accelerate from 0 to 100 kilometers per hour. We call that **regression problem**. And we're learning something called a regression function.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/014.png' alt='014' width='700px' />