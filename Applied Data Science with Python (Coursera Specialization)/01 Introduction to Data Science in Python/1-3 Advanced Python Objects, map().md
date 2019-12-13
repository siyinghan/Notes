# 1-3 Advanced Python Objects, map()

The `map` function is one of the basis of functional programming in `Python`. Functional programming is a programming paradigm in which you explicitly declare all parameters which could change through execution of a given function. This functional programming is referred to as being side-effect free, because there is a software contract that describes what can actually change by calling a function.

`Python` isn't a functional programming language in the pure sense. Since you can have many side effects of functions, and certainly you don't have to pass in the parameters of everything that you're interested in changing. But functional programming causes to think more heavily while chaining operations together. And this really is a sort of underlying theme in much of data science and data cleaning in particular.

So, functional programming methods are often used in Python, and it's not uncommon to see a parameter for a function, be a function itself.

The `map` build-in function is one example of a functional programming feature of Python, that I think ties together a number of aspects of the language. The map function signature looks like this:

![alt text](https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/001.png "001")

![DQmbgzru4YUCtQnwiZkMBQHEzTxCUTzbUn5tSytrWUeukos.jpg](https://steemitimages.com/DQmY53DiVGm6EqeH6EjhMK4fXoQS1S1mvrtCMkg16NibYvM/DQmbgzru4YUCtQnwiZkMBQHEzTxCUTzbUn5tSytrWUeukos.jpg)

<img src="https://github.com/siyinghan/Notes/blob/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/001.png" alt="001" width="70%"/>
