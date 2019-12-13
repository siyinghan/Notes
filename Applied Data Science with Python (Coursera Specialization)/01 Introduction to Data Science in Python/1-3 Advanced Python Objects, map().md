# 1-3 Advanced Python Objects, map()

The `map` function is one of the basis of functional programming in `Python`. Functional programming is a programming paradigm in which you explicitly declare all parameters which could change through execution of a given function. This functional programming is referred to as being side-effect free, because there is a software contract that describes what can actually change by calling a function.

`Python` isn't a functional programming language in the pure sense. Since you can have many side effects of functions, and certainly you don't have to pass in the parameters of everything that you're interested in changing. But functional programming causes to think more heavily while chaining operations together. And this really is a sort of underlying theme in much of data science and data cleaning in particular.

So, functional programming methods are often used in Python, and it's not uncommon to see a parameter for a function, be a function itself.

The `map` build-in function is one example of a functional programming feature of Python, that I think ties together a number of aspects of the language. The map function signature looks like this:

<img src="https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/001.png" alt="001" width='80%'/>

Example
------
Imagine we have two list of numbers, maybe prices from two different stores on exactly the same items. And we wanted to find the minimum that we would have to pay if we bought the cheaper item between the two stores.

To do this, we could iterate through each list, comparing items and choosing the cheapest. With map, we can do this comparison in a single statement.

```python
store1 = [10.00, 11.00, 12.34, 2.34]
store2 = [9.00, 11.10, 12.34, 2.01]
cheapest = map(min, store1, store2)
cheapest
```

But when we going to print out the map, we see that we get an odd reference value instead of a list of items that we're expecting. This is called lazy evaluation. In Python, the map function returns to you a map object. It doesn't actually try and run the function min on two items until you look inside for a value. This is an interesting design pattern of the language, and it's commonly used when dealing with big data. This allows us to have very efficient memory management, even though something might be computationally complex.

```<map at 0x7f6014049630>```

`map` are iterable, just like lists and tuples, so we can use a for loop to look at all of the values in the map. This passing around of functions and data structures which they should be applied to, is a hallmark of functional programming. It's very common in data analysis and cleaning.

```python
for item in cheapest:
    print(item)
```
```
9.0
11.0
12.34
2.01
```

