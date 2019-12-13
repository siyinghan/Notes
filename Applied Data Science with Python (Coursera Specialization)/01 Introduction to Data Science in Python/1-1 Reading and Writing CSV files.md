# 1-1 Reading and Writing CSV files

`%precision 2` controls how floats display (only works in an IPython interpreter).

```python
import csv

%precision 2

with open('mpg.csv') as csvfile:
    mpg = list(csv.DictReader(csvfile))
    
mpg[:3] # The first three dictionaries in our lists.
```

`csv.Dictreader` has read in each row of our csv file as a dictionary. `len` shows that our list is comprised of 234 dictionaries:
```python
len(mpg)
```

`keys` gives us the column names of our `csv`:
```python
mpg[0].keys()
```

This is how to find the average `cty` fuel economy across all cars. All values in the dictionaries are strings, so we need to convert to float:
```python
sum(float(d['cty']) for d in mpg) / len(mpg)
```

We are grouping the cars by number of cylinder, and finding the average `cty` `mpg` for each group:
```python
# set() 函数创建一个无序不重复元素集，可进行关系测试，删除重复数据，还可以计算交集、差集、并集等
cylinders = set(d['cyl'] for d in mpg)

CtyMpgByCyl = []

for c in cylinders: # iterate over all the cylinder levels
    summpg = 0
    cyltypecount = 0
    for d in mpg: # iterate over all dictionaries
        if d['cyl'] == c: # if the cylinder level type matches,
            summpg += float(d['cty']) # add the cty mpg
            cyltypecount += 1 # increment the count
    CtyMpgByCyl.append((c, summpg / cyltypecount)) # append the tuple ('cylinder', 'avg mpg')

CtyMpgByCyl.sort(key=lambda x: x[0])
CtyMpgByCyl
```
```[('4', 21.01), ('5', 20.50), ('6', 16.22), ('8', 12.57)]```