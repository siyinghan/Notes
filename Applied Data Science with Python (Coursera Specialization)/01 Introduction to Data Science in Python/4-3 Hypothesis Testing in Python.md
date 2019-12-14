# 4-3 Hypothesis Testing in Python

**Material**: [grades.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/grades.csv)

<br/>

We use statistics in a lot of different ways in data science. In this lecture, I want to refresh your knowledge of **hypothesis testing**, which is a core data analysis activity behind experimentation. We're starting to see experimentation used more and more commonly outside of academic scientific, and in day to day business environments. Part of the reason for this is the rise of big data and web commerce. It's now easy to change your digital storefront and deliver a different experience to some of your customers, and then see how those customer actions might differ from one another.

For instance, if you sell books, you might want to have one condition where the cover of the book is featured on the web page and another condition where the focus is on the author and the reviews of the book. This is often called **A/B testing**. And while it's not unique to this time in history, it's now becoming so common that if you're using a website, you are undoubtedly part of an **A/B test** somewhere. This raises some interesting ethical questions and I've added a reading to the course resources and I would like to encourage you to check it out and join in the discussion.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/086.png' alt='086' width='60%' />

Let's refocus back on statistics. A **hypothesis** is a statement that we can test. I'll put an example from my own research of educational technology and learning analytics. Let's say that we have an expectation that when a new course is launched on a MOOC platform, the keenest students find out about it and all flock to it. Thus, we might expect that those students who sign up quite quickly after the course is launched with higher performance than those students who signed up after the MOOC has been around for a while. In this example, we have samples from two different groups which we want to compare. The **early sign ups** and the **late sign ups**. When we do hypothesis testing, we hold out that our hypothesis as the alternative and we create a second hypothesis called the **null hypothesis**, which in this case would be that there is no difference between groups. We then examine the groups to determine whether this null hypothesis is true or not. If we find that there is a difference between groups, then we can reject the null hypothesis and we accept our alternative.

There are subtleties in this description. We aren't saying that our hypothesis is true per se, but we're saying that there's evidence against the null hypothesis. So, we're more confident in our **alternative hypothesis**. Let's see an example of this. We can load a file called `grades.csv`:

```python
df = pd.read_csv('grades.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/087.png' alt='087' width='100%' />

Each with a submission time and it looks like there just under 3,000 entries in this data file:

```python
len(df)
```

```2315```

For the purpose of this lecture, let's segment this population in to two pieces. Those who *finish the first assignment by the end of December 2015* and those who *finish it sometimes after that*. I just made this date up and it gives us two data frames, which are roughly the same size:

```python
early = df[df['assignment1_submission'] <= '2015-12-31']
late = df[df['assignment1_submission'] > '2015-12-31']
```

As you've seen, the pandas data frame object has a variety of statistical functions associated with it. If we call the mean function directly on the data frame, we see that each of the means for the assignments are calculated (Note that the date time values are ignored as panda's knows this isn't a number, but an object type.):

```python
early.mean()
```

```
assignment1_grade    74.972741
assignment2_grade    67.252190
assignment3_grade    61.129050
assignment4_grade    54.157620
assignment5_grade    48.634643
assignment6_grade    43.838980
dtype: float64
```

If we look at the mean values for the late data frame as well, we get surprisingly similar numbers:

```python
late.mean()
```

```
assignment1_grade    74.017429
assignment2_grade    66.370822
assignment3_grade    60.023244
assignment4_grade    54.058138
assignment5_grade    48.599402
assignment6_grade    43.844384
dtype: float64
```

There are slight differences, though. It looks like the end of the six assignments, the early users are doing better by about a percentage point.

So, is this enough to go ahead and make some interventions to actually try and change something in the way we teach? When doing hypothesis testing, we have to choose a **significance level** as a **threshold** for how much of a chance we're willing to accept. This significance level is typically called **alpha**.

