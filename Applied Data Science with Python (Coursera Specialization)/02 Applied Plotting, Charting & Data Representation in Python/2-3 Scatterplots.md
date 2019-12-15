# 2-3 Scatterplots

In the previous lecture, I introduced the `plot` function, which generates a series of lines which get rendered against an axis object. Matplotlib actually has a number of useful plotting methods in the **scripting layer** which correspond to different kinds of plots. We are not going to go through all of them here but we'll touch on a few of the major ones. Regardless, there are a few things to keep in mind which we learned in the previous lecture:

* One, `pyplot` is going to retrieve the current figure with the function `gcf` and then get the current axis with the function `gca`. Pyplot is keeping track of the axis objects for you. But don't forget that they're there and we can get them when we want to get them.
* Two, also pyplot just mirrors the API of the axis objects. So you can call the `plot` function against the pyplot module. But this is calling the axis plot functions underneath, so be aware.
* And three, finally, remember that the function declaration from most of the functions in matplotlib end with an open set of keyword arguments. There are a lot of different properties you can control through these keyword arguments. And I'll start peppering in some of them this week to demostrate that the matplotlib documentation is really key in gaining a full understanding of the options available.

With that in mind let's move on to talk first about **scatterplots**.

