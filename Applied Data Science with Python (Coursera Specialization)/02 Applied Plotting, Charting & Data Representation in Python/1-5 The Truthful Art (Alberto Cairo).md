# 1-5 The Truthful Art (Alberto Cairo)

I consider Alberto Cairo's book, The Truthful Art to be required reading for any data scientist. In one book, he has managed to pack in a plethora of references to experts in the field while still distilling down details into memorable lessons. While we won't have an opportunity to cover everything he talks about. I want to talk in this lecture about the foundation of the book in particular which is a **five part frame work** for considering the qualities of an information graphic.

Importantly, Cairo says that these qualities are not independent of one another and that they're interrelated. So while I tend to be prone to reductionism, keep in mind that the different qualities interact with one another as we go through the lecture.

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/026.png' alt='026' width='80%' />

The first quality of a good visualization is that it's **truthful**. Now Cairo admits that truth could be considered subjective and it's certainly on a continuum with some things being more truthful than others. And then it might be impossible to establish an absolute truth. But as data scientists, he argues, we have two obligations when it comes to protecting the truth.

* First, we have to be honest with ourselves when we clean and summarize data. Are the activities we're engaging in likely to obscure a message because of the limitations that we've applied? We should consider explicitly each modification that we're making to the data. And make sure we are practicing what he calls self deception. **Skepticism** is an important skill for data scientist. And we often get so focus on looking for patterns that we reduce or present data in ways which are inauthentic to the phenomena being described.
* The second obligation is to our audience. That is there are techniques and data science and information visualization, which we can use to shine light on to specific pieces of data. Indeed this is generally the point of the fields. But if we omitted the ability of the reader to explore the phenomena more fully this will generate doubt and cast distrust.

Cairo gives us a great examples of this, using a chart inspired by one put out by the lobbying association. The national cable and telecommunications association. This association lobbies on behalf of US cable companies. And provided a graphic which suggested that, after regulations were relaxed, cable companies invested four times as much in the industry. Now the original chart has been taken down, but Cairo provides an example of what was visualized:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/027.png' alt='027' width='50%' />

And we can see here, the title of the chart alone, was intended to draw the reader to the conclusion, less regulation means more industry investment. But there's some immediate problems with this graphic.

* First, it's unclear whether the monies are adjusted for inflation, which is a big issue when providing     charts of financial data.
* Second, the time spans for the two bars are different. One covers a span of three years, while the other     covers a span of four years. Think of this through the lens of Tufts' Live     Factor Analysis. The bars have the same width, but don't represent the same     period of time. This is a completely unforgivable design choice.
* And finally, there seems to be a bunch of missing data from years 1997 and 1998. And the chart stops in the year 2003, but the information was tweeted in 2014.

What does a more honest view of the data look like? Well Cairo tracked this down, and provided a line graph:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/028.png' alt='028' width='100%' />

We can see that after regulation, there were in fact years of sustained industry investment. We see a slight drop after deregulation, then a massive spike in spending. And then a significant fall from the period post 2002, much of which is excluded from the original chart. While it's unclear whether the dollar values are in fact corrected for inflation, seems pretty unreasonable to suggest from this data alone that regulations stems cable company investment and infrastructure.The lesson here is that, while there's maybe no absolute truth, there are ways of displaying data which are more truthful than others.

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/029.png' alt='029' width='80%' />

The second quality of a visualization to consider is whether it is functional or not. This again is continuum when we saw an example previously with the slides on data-ink-ratio provided by Darkhorse Analytics:

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/030.png' alt='030' width='100%' />

If you expect your audience would want to compare two data series. Direct labeling of them is one way to increase comprehension. Well there are many heuristics for increasing functionality, I would like you to remember the user test we did with. I think now is an exciting time for understating situated human behavior. The web has dramatically increased trainability to test social and behavioral hypothesis that scale across diverse populations. And crowd power and mechanical tuck are just two example of this. Understanding how functional a given approach to a visualization is doesn't necessarily require expensive ethnographic research. It's now much easier to test hypotheses directly with crowd sources. 

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/031.png' alt='031' width='80%' />

The third quality of visualization, Cairo shares is whether it is beautiful or not. I think that this requires knowing a great deal about your audience. There are different perceptions based on people's lived experiences and aspects about themselves such as gender and culture. There's a lot to building a beautiful information visualization experience, which depends on situational and contextual factors too.

For instance, if you're building a chart for a report, the colors and styles that you might choose, even down the font choice, might be more related to beauty than for instance, function. But the interplay of these elements is something which is difficult to ignore. I wonder is this broad topic of beauty one of the conflationary factors of the chart junk memorability issue? Where as Tufte argued that the duck junk is distracting and misleading, the study by Bateman et al showed that it can make visualizations more memorable. Is this disconnect an issue of beauty in information graphics? Here's one parting thought on beauty in information that perhaps drives home this quality. One of the most popular tech magazines, well known for it's full page information graphic spreads is Wired Magazine. On Wired's website, they tag these articles as info porn. A reference to the visceral reaction that they hope readers will view when viewing the articles.

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/032.png' alt='032' width='80%' />

The fourth quality of visualization from Cairo is that information graphics should be insightful. They shouldn't just replicate data in tables, but they should draw the viewer in such that the viewer has an aha or eureka moment. I think about this largely in the context of academic papers where I do most of my work. A common issue that novice writers have in this area is the inclusion of a figure for every piece of data they have. This is really unnecessary and adds bloat and contributes to reader fatigue. But the right figure drives home the results of a study quickly. Scientific peer review is common in my field, but readers don't have the large amounts of time that they need to do full reviews. When flipping through a submitted paper, the reviewer sees an image which jumps off the page and gives them immediate insight. This sets them up to understand the more nuanced story to be told throughout the rest of the paper.

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/033.png' alt='033' width='80%' />

The final quality of visualization which Cairo proposes is information graphics should be enlightening. This is different than insightful. In fact, Cairo argues that this quality is composed of the previous four, truthful, functional, beautiful and insightful. But he separates and then adds a social responsibility dimension.

I don't think there's an obvious answer to this question. But without a doubt, Cairo's Five Qualities of Great Visualizations being truthful, functional, beautiful, insightful, and enlightening are well worth considering. Cairo has more great work, and following this lecture I have assigned a reading of his as well as a discussion question to encourage you to weigh in on the immorality of information visualization as it relates to data science. And this ends the week of the course. We've covered a lot of material very quickly. But I really do believe that these two authors Alberto Ciro and Edward Tufty are fundamental in building a strong foundation for the applied data science skills, we'll focus on in the second week of the course.