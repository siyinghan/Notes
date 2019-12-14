# 2-5 Querying a DataFrame

**Material**: [olympics.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/olympics.csv)

<br/>

**Boolean masking** is the heart of fast and efficient querying in `NumPy`. It's analogous a bit to masking used in other computational areas. A Boolean mask is an array which can be of one dimension like a series, or two dimensions like a data frame, where each of the values in the array are either true or false. This array is essentially overlaid on top of the data structure that we're querying. And any cell aligned with the true value will be admitted into our final result, and any sign aligned with a false value will not. **Boolean masking** is powerful conceptually and is the cornerstone of efficient `NumPy` and `Pandas` querying. This technique is well used in other areas of computer science, for instance, in graphics. But it doesn't really have an analogue in other traditional relational databases, so I think it's worth pointing out here.

Boolean masks are created by applying operators directly to the pandas series or DataFrame objects. For instance, in our Olympics data set, you might be interested in seeing only those countries who have achieved a gold medal at the summer Olympics. To build a Boolean mask for this query, we project the gold column using the indexing operator and apply the greater than operator with a comparison value of zero:

```python
df['Gold'] > 0
```

