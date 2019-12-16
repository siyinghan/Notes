# 1-3 Python Tools for Machine Learning

Okay, now that we've covered a little bit of background on what machine learning is and some of the major types of machine learning problems, there's nothing like getting started with our own machine learning application in Python. And we're going to get started on that right now. So to do that, we're going to make use of several important Python libraries that will support our work. These include `scikit-learn`, `SciPy`, `NumPy`, `pandas`, and `matplotlib`. We recommend installing all of these using the Anaconda Python distribution since it comes with all the libraries we'll need in this part of the course. If you have some other existing Python installation, you can install the libraries we'll be using from the command line using pip, like this.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/028.png' alt='028' width='650px'/>

https://scikit-learn.org/stable/

https://scikit-learn.org/stable/user_guide.html

https://scikit-learn.org/stable/modules/classes.html

The most important library we'll be using for machine learning is called `scikit-learn`. `Scikit-learn` is the most widely used Python library for machine learning and it will be the basis for this course. It's an open source project that's under continual development and improvement, and supports a very wide array of important machine learning algorithms. It has excellent online documentation and a very active user community. Because of this broad adoption, scikit-learn has many sample applications, tutorials, and code examples that are available online. So one valuable reference that we recommend you use while you take this course is the **scikit-learn User Guide** and the **API documentation** which contains further details on the different algorithms that are in the library, along with details on the various options that these algorithms support.

`Scikit-learn` makes use of two other Python scientific computing libraries called `SciPy` and `NumPy`.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/029.png' alt='029' width='650px'/>

https://www.scipy.org/

`SciPy` is a Python library that supports data manipulation and analysis methods that are commonly used in scientific computing. So this includes support for statistical distributions, optimization of functions, linear algebra, and a variety of specialized mathematical functions. In some parts of this course, we'll make use of SciPy's ability to provide what are called **sparse matrices**, which are a way to store large tables that contain mostly zeros, so more on that later.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/030.png' alt='030' width='600px'/>

https://numpy.org/

`NumPy` is a Python library for scientific computing that contains support for some fundamental data structures used by `scikit-learn`, such as **multi-dimensional arrays**. Typically, data that's input to scikit-learn will be in the form of a `NumPy` array.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/031.png' alt='031' width='600px'/>

https://pandas.pydata.org/

`Pandas` is a Python library for data manipulation and analysis. And if you took course one in this series, you've already had experience with what pandas can do. The key data structure pandas supports that we'll be using is called a **DataFrame**, which is basically like a spreadsheet table with rows and named columns. So unlike the arrays supported by NumPy, the columns in a DataFrame can be of all different types. You can have one column holding string values, another column holding a date, another column holding a floating point number and so on. Pandas also has great support for reading and writing data in a variety of formats, everything from comma separated **CSV files** to **SQL**, the Structured Query Language used by databases and more.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/032.png' alt='032' width='600px'/>

https://matplotlib.org/

`Matplotlib` is a widely used **Python 2D plotting library** that produces high quality figures in a variety of formats and interactive environments across platforms. Matplotlib can be used in Python scripts, the Python and iPython shell, web application servers, and a variety of different graphical user interface toolkits. If you've taken course two in this data science series, you'll already have some experience with using matplotlib. Here, we'll primarily be using `matplotlib.pyplot` for data analysis since it can create **histograms**, **bar charts**, **error charts**, **scatter plots**, and so forth with just a few lines of code.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/03%20Applied%20Machine%20Learning%20in%20Python/Image/033.png' alt='033' width='600px'/>

So, for reference, this course will be using the following versions of these libraries as shown on the slide. It's okay if your versions don't match our versions exactly, as long as the version of `scikit-learn` you're using is the same or later than the one we've shown here.