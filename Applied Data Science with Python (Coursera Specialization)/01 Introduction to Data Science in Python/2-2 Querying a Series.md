# 2-2 Querying a Series

A `panda.Series` can be queried, either by the index position or the index label. As we saw, if you don't give an index to the series, the position and the label are effectively the same values. To query by numeric location, starting at zero, use the iloc attribute. To query by the index label, you can use the `loc` attribute.

Here's an example using national sporting event data from Wikipedia. Let's say we want to have a list of all of the sports in our index and a list of countries as values. You might keep these in a dictionary and create a series as we discussed:
```python
sports = {'Archery': 'Bhutan',
          'Golf': 'Scotland',
          'Sumo': 'Japan',
          'Taekwondo': 'South Korea'}
s = pd.Series(sports)
s
```
```
Archery           Bhutan
Golf            Scotland
Sumo               Japan
Taekwondo    South Korea
dtype: object
```

If you wanted to see the fourth country on this, we would use the `iloc` attribute with the parameter 3:
```python
s.iloc[3]
```
```'South Korea'```

If you wanted to see which country has golf as its national sport, we would use the `loc` attribute with parameter **Golf**:
```python
s.loc['Golf']
```
```'Scotland'```

Keep in mind that `iloc` and `loc` are not methods, they are attributes. So you don't use **parentheses** `()` to query them, but **square brackets** `[]` instead, which we'll call the indexing operator. Though in Python, this calls get and set an item methods depending on the context of its use.


