# 1-1 Reading and Writing CSV files

Material: [mpg.csv](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Material/mpg.csv)


`%precision 2` controls how floats display (only works in an IPython interpreter).

```python
import csv

%precision 2

with open('mpg.csv') as csvfile:
    mpg = list(csv.DictReader(csvfile))
    
mpg[:3] # The first three dictionaries in our lists.
```

<br/>

`csv.Dictreader` has read in each row of our `csv` file as a dictionary. `len` shows that our list is comprised of 234 dictionaries:
```python
len(mpg)
```

<br/>

`keys` gives us the column names of our `csv`:
```python
mpg[0].keys()
```

<br/>

This is how to find the average `cty` fuel economy across all cars. All values in the dictionaries are strings, so we need to convert to float:
```python
sum(float(d['cty']) for d in mpg) / len(mpg)
```

<br/>

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

<br/>

Use set to return the unique values for the class types in our dataset:
```python
vehicleclass = set(d['class'] for d in mpg) # what are the class types
vehicleclass
```
```{'2seater', 'compact', 'midsize', 'minivan', 'pickup', 'subcompact', 'suv'}```

<br/>

And here's an example of how to find the average `hwy` `mpg` for each class of vehicle in our dataset:
```python
HwyMpgByClass = []

for t in vehicleclass: # iterate over all the vehicle classes
    summpg = 0
    vclasscount = 0
    for d in mpg: # iterate over all dictionaries
        if d['class'] == t: # if the cylinder amount type matches,
            summpg += float(d['hwy']) # add the hwy mpg
            vclasscount += 1 # increment the count
    HwyMpgByClass.append((t, summpg / vclasscount)) # append the tuple ('class', 'avg mpg')

HwyMpgByClass.sort(key=lambda x: x[1])
HwyMpgByClass
```
```
[('pickup', 16.88),
 ('suv', 18.13),
 ('minivan', 22.36),
 ('2seater', 24.80),
 ('midsize', 27.29),
 ('subcompact', 28.14),
 ('compact', 28.30)]
 ```
