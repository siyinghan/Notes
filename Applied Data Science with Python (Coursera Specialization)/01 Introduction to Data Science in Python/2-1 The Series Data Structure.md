# 2-1 The Series Data Structure

The `series` is one of the core data structures in `pandas`. You think of it a cross between a `list` and a `dictionary`. The items are all stored in an order and there's labels with which you can retrieve them.

An easy way to visualize this is two columns of data. The first is the special index, a lot like the dictionary keys. While the second is your actual data. It's important to note that the data column has a label of its own and can be retrieved using the `.name` attribute.

<img src="https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/002.png" alt="001" width="60%"/>
