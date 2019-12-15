# 1-2 Graphical heuristics: Data-ink ratio (Edward Tufte)

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/008.png' alt='008' width='100%' />

In this book, he introduced two interesting graphical heuristics, the **data-ink ratio** and **chart junk**.

What is a heuristic? A **heuristic** is a process or rule that is meant to guide you in decision making, is by definition not known to be optimal or perfect, but to be practical in nature. Heuristics are meant to be followed until you have reason to deviate from them.

Tufte's first graphical heuristic is **data-ink ratio**. Tufte defines **data-ink** as the non-erasable core of a graphic. The non-redundant ink arranged in response to variation in the numbers represented. In other words, the **data-ink** is essential to the sense-making process for a given variable. Tufte defines the **data-ink ratio** as the amount of data-ink divided by the total ink required to print the graphic.

Now I don't think that he's actually suggesting we measure the amount of ink laid down on the page, but instead is suggesting that we remove those elements which don't add new information to the graphic. Perhaps one of the best known examples showing data-ink reduction was done by Darkhorse Analytics, an information, visualization, and design company in Edmonton, Alberta, Canada.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/009.png' alt='009' width='100%' />

They've put together four examples of how the data-ink ratio can be approved. And I'm going to link to those in the next reading assignment. But I'm going to walk through the first one of those here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/010.png' alt='010' width='50%' />

We start with the table of the data about *food items* and the *number of calories* in those items. The first step is to remove unwanted background imagery since it provides no value to understanding the chart. We also remove the gray background behind the bars since it provides no conceptual value.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/011.png' alt='011' width='50%' />

Then we get rid of the redundancy throughout. This includes getting rid of the legend, since each bar is labeled directly along the x-axis. The title in the y-axis labels are trimmed, since there's plenty of reference throughout the image to this being about calories for food items.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/012.png' alt='012' width='50%' />

This leaves us with a much smaller image. There are some heavy lines forming borders which add no value, so we can remove them too.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/013.png' alt='013' width='50%' />

Color is a tricky item to include in charts and graphs. We won't be going into depth on color theory in this course. But color is a challenge when trying to engage with persons who might be color vision deficient or color blind. There are some tactics to work around. For instance, it used to be best practice to replace coloration with patterns, sometimes called hatching in graphics. This brings its own challenges, which we'll see in a bit. Instead, the solution is almost always to remove all color, except for one which you can use as emphasis and link to that color in your text. Someone then viewing a chart out of context would still get the sense of emphasis without being overwhelmed by a rainbow of data. So let's drop colors except for bacon, with the presumption that this text is clearly referenced in the data.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/014.png' alt='014' width='50%' />

Three-dimensional bars and drop shadows can go as well, since these don't add extra value. We could also drop the bolding throughout.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/015.png' alt='015' width='50%' />

There's still a lot of gridwork left in this image and it's a bit unclear what the value of this gridwork is, so we're going to drop it. Now grids can be valuable, but they're often just a distraction. For the moment though, study the image. What's the difference in the number of calories between bacon, our data point of interest, and say, potato chips or chili dogs? Just removing the lines doesn't make it easier to read. But the values of the data are pretty simple here.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/016.png' alt='016' width='50%' />

So let's directly label each bar in the graphic.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/017.png' alt='017' width='50%' />

Now, how big is the difference between bacon and potato chips or bacon and chili dogs? Certainly, you have to do a bit of math, but you can still get a quick estimate by glancing at the graphic, and an exact value through comparing numbers directly. And there you have it.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/018.png' alt='018' width='100%' />

By **increasing the data-ink ratio**, we have made the graphic not only simpler and more readable, but increased the amount of information the viewer sees.

I encourage you to check out the other examples from Darkhorse Analytics linked in the next reading. As they've done this clean up for a variety of different visuals including maps. We'll continue our exploration of Tufte's heuristics by looking at chart junk in the next lecture.