# 1-4 Lambda and List Comprehensions

`lambda's` are Python's way of creating anonymous functions. These are the same as other functions, but they have no name. The intent is that they're simple or short lived and it's easier just to write out the function in one line instead of going to the trouble or creating a named function. The lambda syntax is fairly simple. But it might take a bit of time to get used to.

You declare a `lambda` function with the word lambda followed by a list of arguments, followed by a colon and then a single expression and this is key. There's only one expression to be evaluated in a lambda. The expression value is returned on execution of the lambda. The return of a lambda is a function reference.
```python
my_function = lambda a, b, c : a + b
```

So in this case, you would execute `my_function` and pass in three different parameters. Note you can't have default values for lambda parameters and you can't have complex logic inside of the lambda itself. Because you're limited to a single expression.
```python
my_function(1, 2, 3)
```
```3```

<br/>

Python has built in support for creating these collections using a more abbreviated syntax called `list comprehensions`. Here is an example:
```python
# iterate from 0 to 999 and return the even numbers
my_list = []
for number in range(0, 1000):
    if number % 2 == 0:
        my_list.append(number)
```
We can rewrite this as a `list comprehension` by pulling the iteration on one line:
```python
my_list = [number for number in range(0,1000) if number % 2 == 0]
```
