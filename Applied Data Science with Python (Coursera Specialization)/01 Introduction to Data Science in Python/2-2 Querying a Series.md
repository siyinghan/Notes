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


Pandas tries to make our code a bit more readable and provides a sort of smart syntax using the indexing operator directly on the series itself. For instance, if you pass in an integer parameter, the operator will behave as if you want it to query via the `iloc` attribute. If you pass in an object, it will query as if you wanted to use the label based `loc` attribute:

```python
s[3]
```
```'South Korea'```
```python
s['Golf']
```
```'Scotland'```

<br/>

So what happens if your index is a list of integers? This is a bit complicated, and `pandas` can't determine automatically whether you're intending to query by index position or index label. So you need to be careful when using the indexing operator on the series itself. And the safer option is to be more explicit and use the `iloc` or `loc` attributes directly. 

Here's an example using some new sports data, where countries are indexed by integer:
```python
sports = {99: 'Bhutan',
          100: 'Scotland',
          101: 'Japan',
          102: 'South Korea'}
s = pd.Series(sports)
s
```
```
99          Bhutan
100       Scotland
101          Japan
102    South Korea
dtype: object
```

If we try and call s sub zero, we get a key error, because there's no item in the sports list with an index of zero:
```python
s[0] #This won't call s.iloc[0] as one might expect, it generates an error instead
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/005.png' alt='005' width='90%' />

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/005.png' alt='005' width='80%' />
































