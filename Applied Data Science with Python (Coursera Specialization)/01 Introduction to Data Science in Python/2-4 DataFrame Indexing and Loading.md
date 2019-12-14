# 2-4 DataFrame Indexing and Loading

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)

<br/>

The common work flow is to read your data into a DataFrame then reduce this DataFrame to the particular columns or rows that you're interested in working with. As you've seen, the Panda's toolkit tries to give you views on a `DataFrame`. This is much faster than copying data and much more memory efficient too. But it does mean that if you're manipulating the data you have to be aware that any changes to the DataFrame you're working on may have an impact on the base data frame you used originally.

Here's an example using our same purchasing DataFrame from earlier. We can create a series based on just the cost category using the square brackets `[]`:

```python
costs = df['Cost']
costs
```

```
Store 1    22.5
Store 1     2.5
Store 2     5.0
Name: Cost, dtype: float64
```

Then we can increase the cost in this series using broadcasting:

```python
costs+=2
costs
```

```
Store 1    24.5
Store 1     4.5
Store 2     7.0
Name: Cost, dtype: float64
```

Now if we look at our original DataFrame, we see those costs have risen as well:

```python
df
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/017.png' alt='017' width='36%' />

This is an important consideration to watch out for. If you want to explicitly use a copy, then you should consider calling the `copy` method on the DataFrame for it first.

<br/>

In this course, we'll be largely using smaller, moderate-sized datasets. As I mentioned, a common workflow is to read the dataset in, usually from some external file. We saw previously how you can do this using Python, and lists, and dictionaries. You can imagine how you might use those dictionaries to create a Pandas DataFrame. Thankfully, Pandas has built-in support for delimited files such as CSV files as well as a variety of other data formats including relational databases, Excel, and HTML tables. I've saved a CSV file called **olympics.csv**, which has data from Wikipedia that contains a summary list of the medal various countries have won at the Olympics.

We can take a look at this file using the shell command cat. Which we can invoke directly using the exclamation point:

```python
!cat olympics.csv
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/018.png' alt='018' width='70%' />

What happens here is that when the Jupyter notebook sees a line beginning with an exclamation mark, it sends the rest of the line to the operating system shell for evaluation. So cat works on Linux and Macs, as well as in the Coursera platform, but might not work on Windows. You don't need to worry too much about this. I just wanted to show how a Jupyter notebook can integrate with the operating system to provide you with even more tools to look at your data.

 We see from the cat output that there seems to be a numeric list of columns followed by a bunch of column identifiers. The column identifiers have some odd looking characters in them. This is the **unicode numero sign**, which means number of:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/019.png' alt='019' width='55%' />

Then we have rows of data, all columns separated.

We can read this into a DataFrame by calling the `read_csv` function of the module:

```python
df = pd.read_csv('olympics.csv')
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/020.png' alt='020' width='90%' />

When we look at the DataFrame we see that the first cell has an NaN in it since it's an empty value, and the rows have been automatically indexed for us. It seems pretty clear that the first row of data in the DataFrame is what we really want to see as the column names. It also seems like the first column in the data is the country name, which we would like to make an index.

Read `csv` has a number of parameters that we can use to indicate to Pandas how rows and columns should be labeled. For instance, we can use the *index call* to indicate which column should be the index and we can also use the *header parameter* to indicate which row from the data file should be used as the header.

Let's re-import that data and center index value to be 0 which is the first column and let set a column headers to be read from the second row of data. We can do this by using the skip rows parameters, to tell Pandas to ignore the first row, which was made up of numeric column names:

```python
df = pd.read_csv('olympics.csv', index_col=0, skiprows=1)
df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/021.png' alt='021' width='100%' />

<br/>

Now this data came from the all time Olympic games medal table on Wikipedia. If we head to the page we could see that instead of running gold, silver and bronze in the pages, these nice little icons with a one, a two, and a three in them. In our csv file these were represented with the strings **01 !**, **02 !**, and so on. We see that the column values are repeated which really isn't good practice. Panda's recognize this in a panda.1 and .2 to make things more unique. But this labeling isn't really as clear as it could be, so we should clean up the data file. We can of course do this just by going and editing the CSV file directly, but we can also set the column names using the Pandas name property.

Panda stores a list of all of the columns in the `.columns` attribute:

```python
df.columns
```

```
Index(['№ Summer', '01 !', '02 !', '03 !', 'Total', '№ Winter', '01 !.1',
       '02 !.1', '03 !.1', 'Total.1', '№ Games', '01 !.2', '02 !.2', '03 !.2',
       'Combined total'],
      dtype='object')
```

We can change the values of the column names by iterating over this list and calling the rename method of the data frame. Now, I'm going to copy and paste this in to speed up things but we can walk through what is going on here. Here we just iterate through all of the columns looking to see if they start with a 01, 02, 03 or numeric character. If they do, we can call rename and set the column parameters to a dictionary with the keys being the column we want to replace and the value being the new value we want. Here we'll slice some of the old values in two, since we don't want to lose the unique appended values. We'll also set the ever-important `inplace` parameter to true so Pandas knows to update this data frame directly:

```python
for col in df.columns:
    if col[:2]=='01':
        df.rename(columns={col:'Gold' + col[4:]}, inplace=True)
    if col[:2]=='02':
        df.rename(columns={col:'Silver' + col[4:]}, inplace=True)
    if col[:2]=='03':
        df.rename(columns={col:'Bronze' + col[4:]}, inplace=True)
    if col[:1]=='№':
        df.rename(columns={col:'#' + col[1:]}, inplace=True) 

df.head()
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/022.png' alt='022' width='100%' />

