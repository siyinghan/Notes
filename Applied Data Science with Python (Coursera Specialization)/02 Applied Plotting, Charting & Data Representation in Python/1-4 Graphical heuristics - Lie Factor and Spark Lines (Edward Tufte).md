# 1-4 Graphical heuristics: Lie Factor and Spark Lines (Edward Tufte)

Edward Tufte's emphasis on simplicity and minimalism has grown a great following. He's largely seen as one of the most influential writers on the topic of visualizations for charts and graphs. In his book, Beautiful Evidence, he introduced the idea that took minimalism in charts to a new level. Instead of making a chart a separate artifact to be studied on it's own, he suggested it be reduced and embedded within the context of discussion. He argued that a small graph, say a time series line graph, could convey so much more information quickly that it would be invaluable to readers. He called these items sparklines and referred to them as data words. An intriguing way to bridge the gap between text and figures. He suggested that sparklines could not only be represented directly in text, but also could be embedded in tables along with the data they describe. This thought became so natural that it's even been pick up by one of the most common pieces of spreadsheet analysis software, **Microsoft Excel**.

Here is a picture of tabular data from the NASDAQ stock exchange, showing the opening price of four technology stocks over one-month period:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/021.png' alt='021' width='40%' />

Take a moment to consider this data. Which stock has had a bad month with a downward trend? And which has had a good month with an upward trend? What if I added sparklines in the cells below?

Here you can see immediately that Apple has had a poor month with decreased stock price. And IBM has had good month with increasing stock prices. With Amazon and Intel it's a little less clear, and we see some spikes throughout.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/022.png' alt='022' width='100%' />

Now these sparklines don't help us to answer who has the highest stock price, or who had the greatest wins or losses. But they do give us a general feeling for the trend behind the data.

And actually, sparklines are used for data where trends or distribution characteristics are important. Here's another example of sparklines used in Google Finance's website:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/023.png' alt='023' width='100%' />

Notice how you can actually quickly zoom in on pieces of the distribution with these sparklines. So they're not just a representation of the data but a method of interacting with them.

There have been lots of different uses of **sparklines**. And customized interfaces, such as video games, are a great example. A modern take on sparklines, which I think of as kind of neat, is called the **sparktweet**. Where Unicode block characters are used to display a bar graph inside the 140 characters allotted by Twitter.

For instance, here a user has tweeted her hours of sleep over the month of April as a bar graph:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/024.png' alt='024' width='40%' />

The last Tufte principle that I want to share with you is one called **lie factor**. Lie factor is the size of an effect shown in the graphic divided by the size of the effect actually in the data. It's often done unconsciously, to try and help tell a narrative, however, it's misleading to the observers. There are lots of different examples of lie factor. This one from Time Magazine in 1979 provides a great example, I think.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/025.png' alt='025' width='100%' />

In it, various barrels of oil are shown, showing the price of oil over six years. But it's unclear to the viewer what the size of one barrel means in relation to the others, in part because there's an element of perspective here. Are the barrels different sizes, or do they just appear to be so because some are in front of the others? Is it the volume of the barrel that represents the growth of the cost, or the height of the barrel?

Sparklines and lie factor are just two more tools that Edward Tufte has given us to understand and communicate data.