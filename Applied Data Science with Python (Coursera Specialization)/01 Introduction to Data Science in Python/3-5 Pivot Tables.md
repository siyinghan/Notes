# 3-5 Pivot Tables

**Material**: [cars.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/cars.csv)

<br/>

A pivot table is a way of summarizing data in a data frame for a particular purpose. It makes heavy use of the aggregation function. A pivot table is itself a data frame, where the rows represent one variable that you're interested in, the columns another, and the cell's some aggregate value. A pivot table also tends to includes marginal values as well, which are the sums for each column and row. This allows you to be able to see the relationship between two variables at just a glance. Let's take a look at an example. Here we'll load a new data set, `cars.csv`. This data set comes from the Open Data Initiative of the Canadian government. And has information about the efficiency of different electric cars which are available for purchase.

```python
#http://open.canada.ca/data/en/dataset/98f1a129-f628-4ce4-b24d-6f16bf24dd64
df = pd.read_csv('cars.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/066.png' alt='066' width='100%' />

When we look at the head of the data frame, we'll see that there are model years, vendors, sizes of cars, and statistics, like how big the battery is in kilowatt hours. A pivot table allows us to pivot out one of these columns into a new column headers and compare it against another column as row indices. For instance, let's say we wanted to compare the makes of electric vehicles versus the years and that we wanted to do this comparison in terms of battery capacity. To do this, we tell pandas we want the values to be **kilowatts**, the index to be the **year** and the columns to be the **make**. Then we specify that the aggregation function, and here we'll use the `numpy.mean`:

```python
df.pivot_table(values='(kW)', index='YEAR', columns='Make', aggfunc=np.mean)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/067.png' alt='067' width='70%' />

Here's the results. We see there are NaN values for vendors who didn't have an entry in a given year like Ford in 2012. And we see that most vendors don't have a change in battery capacity over the years, except for Tesla, as they've introduced several new models.

Now, pivot tables aren't limited to one function that you might want to apply. You can pass aggfunc, a list of the different functions to apply, and pandas will provide you with the result using hierarchical column names. Here, I'll also pass margins equals true. And that you can see for each of the functions there's now an all category, which shows the overall mean and the minimum values for a given year and a given vendor:

```python
pd.pivot_table(df, values='(kW)', index='YEAR', columns='Make', aggfunc=np.mean)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/067.png' alt='067' width='70%' />

So that's pivot tables. This has been a pretty short description, but they're incredibly useful when dealing with numeric data. And of course, you can pass any function you want to the aggregate function, including those that you define yourself.