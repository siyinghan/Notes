# 1-1 Reading and Writing CSV files

`%precision 2` controls how floats display (only works in an IPython interpreter)


```python
import csv

%precision 2

with open('mpg.csv') as csvfile:
    mpg = list(csv.DictReader(csvfile))
    
mpg[:3] # The first three dictionaries in our lists.
```
