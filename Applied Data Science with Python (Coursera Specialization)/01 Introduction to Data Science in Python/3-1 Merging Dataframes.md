# 3-1 Merging Dataframes

Last week, we were introduced to the pandas data manipulation and analysis library. We saw that there is really *two-core data structures* which are very similar, the *one-dimensional series object* and the *two-dimensional DataFrame object*. Querying these two data structures is done in a few different ways, such as using the `iloc` or `loc` attributes for row-based querying, or using the square brackets on the object itself for column-based querying. Most importantly, we saw that one can query the DataFrame and Series objects through **Boolean masking**. And Boolean masking is a powerful filtering method which allows us to use broadcasting to determine what data should be kept in our analysis.

In this week's lecture, we're going to go into more detail on how to manipulate DataFrame, in particular. We're going to explore how to reduce and process data using `GroupBy` and `Apply`, and how to join data sets from multiple files together into one. We'll also talk about some features that pandas has which are useful for both traditional statistical analyses and machine learning.

Let's start with how to merge data sets. We've already seen how we add new data to an existing DataFrame. We simply use the square bracket operator with the new column name, and the data is added as long as an index is shared. If there is no shared index and a scalar value is passed in, which remember a scalar value is just a single value like an integer or a string. The new value column is added with the scalar value as the default value. What if we wanted to assign a different value for every row? Well, it gets trickier. If we could hardcode the values into a list, then pandas will unpack them and assign them to the rows. But if the list we have isn't long enough, then we can't do this, since Pandas doesn't know where the missing values should go. Here's an example. We used the DataFrame of store purchases from one of our previous lectures, where the index is a list of stores and the columns store purchase data:

```python
import pandas as pd

df = pd.DataFrame([{'Name': 'Chris', 'Item Purchased': 'Sponge', 'Cost': 22.50},
                   {'Name': 'Kevyn', 'Item Purchased': 'Kitty Litter', 'Cost': 2.50},
                   {'Name': 'Filip', 'Item Purchased': 'Spoon', 'Cost': 5.00}],
                  index=['Store 1', 'Store 1', 'Store 2'])
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/040.png' alt='040' width='30%' />

If we want to add some new column called *Date* to the DataFrame, that's fine. We just use the square bracket operator directly on the DataFrame, as long as the column is as long as the rest of the records:

```python
df['Date'] = ['December 1', 'January 1', 'mid-May']
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/041.png' alt='041' width='40%' />

If we want to add some new field, may be a delivery flag, that's easy too since it's a scalar value:

```python
df['Delivered'] = True
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/042.png' alt='042' width='49%' />

The problem comes in when we have only a few items to add. In order for this to work, we have to supply pandas the list which is long enough for the DataFrame, so that each row could be populated. This means that we have to input none values ourselves:

```python
df['Feedback'] = ['Positive', None, 'Negative']
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/043.png' alt='043' width='59%' />

If each of our rows has a unique index, then we could just assign the new column identifier to the series. For instance, if we reset the index in this example so the DataFrame is labeled from 1 through 2, then we create a new series with these labels, we can apply it. And the results we get are as we expected:

```python
adf = df.reset_index()
adf['Date'] = pd.Series({0: 'December 1', 2: 'mid-May'})
adf
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/044.png' alt='044' width='64%' />

The nice aspect of this approach is that we could just ignore the items that we don't know about, and pandas will put missing values in for us. So this is a really nice way to do it.

<br/>

More commonly, we want to join two larger DataFrames together, and this is a bit more complex. Before we jump into the code, we need to address a little relational theory, and to get some language conventions down.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/045.png' alt='045' width='50%' />

This is a Venn Diagram. A Venn Diagram is traditionally used to show set membership. For example, the circle on the left is the population of students at a university. The circle on the right is the population of staff at a university. And the overlapping region in the middle are all of those students who are also staff. Maybe these students run tutorials for a course, or grade assignments, or engage in running research experiments.

We could think of these two populations as indices in separate DataFrames, maybe with the label of Person Name. When we want to join the DataFrames together, we have some choices to make.

First what if we want a list of all the people regardless of whether they're staff or student, and all of the information we can get on them? In database terminology, this is called a *full outer join*. And in set theory, it's called a *union*. In the Venn diagram, it represents everyone in any circle. It's quite possible though that we only want those people who we have maximum information for, those people who are both staff and students. In database terminology, this is called an *inner join*. Or in set theory, the *intersection*. And this is represented in the Venn diagram as the overlapping parts of each circle.

Okay, so let's see an example of how we would do this in pandas, where we would use the `merge` function. First we create two DataFrames, staff and students. There's some overlap in these DataFrames, in that James and Sally are both students and staff, but Mike and Kelly are not. Importantly, both DataFrames are indexed along the value we want to merge them on, which is called **Name**:

```python
staff_df = pd.DataFrame([{'Name': 'Kelly', 'Role': 'Director of HR'},
                         {'Name': 'Sally', 'Role': 'Course liasion'},
                         {'Name': 'James', 'Role': 'Grader'}])
staff_df = staff_df.set_index('Name')
student_df = pd.DataFrame([{'Name': 'James', 'School': 'Business'},
                           {'Name': 'Mike', 'School': 'Law'},
                           {'Name': 'Sally', 'School': 'Engineering'}])
student_df = student_df.set_index('Name')
print(staff_df.head())
print()
print(student_df.head())
```

```
Role
Name                 
Kelly  Director of HR
Sally  Course liasion
James          Grader

            School
Name              
James     Business
Mike           Law
Sally  Engineering
```

If we want the *union* of these, we would call merge passing in the DataFrame on the left and the DataFrame on the right, and telling merge that we want it to use an outer join. We tell merge that we want to use the left and right indices as the joining columns:

```python
pd.merge(staff_df, student_df, how='outer', left_index=True, right_index=True)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/046.png' alt='046' width='30%' />

We see in the resulting DataFrame that everyone is listed. And since Mike does not have a role, and John does not have a school, those cells are listed as missing values.

If we wanted to get the intersection, that is, just those students who are also staff, we could set the how attribute to inner. And we set the resulting DataFrame has only James and Sally in it:

```python
pd.merge(staff_df, student_df, how='inner', left_index=True, right_index=True)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/047.png' alt='047' width='30%' />

Now there are two other common use cases when merging DataFrames. Both are examples of what we would call set addition. The first is when we would want to get a list of all staff regardless of whether they were students or not. But if they were students, we would want to get their student details as well. To do this we would use a left join:

```python
pd.merge(staff_df, student_df, how='left', left_index=True, right_index=True)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/048.png' alt='048' width='30%' />

You could probably guess what comes next. We want a list of all of the students and their roles if they were also staff. To do this we would do a right join:

```python
pd.merge(staff_df, student_df, how='right', left_index=True, right_index=True)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/049.png' alt='049' width='30%' />

The merge method has a couple of other interesting parameters. First, you don't need to use indices to join on, you can use columns as well. Here's an example:

```python
staff_df = staff_df.reset_index()
student_df = student_df.reset_index()
pd.merge(staff_df, student_df, how='left', left_on='Name', right_on='Name')
```

