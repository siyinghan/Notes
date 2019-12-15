# 2-6 Dejunkifying a Plot

In this lecture, I want to walk you through the process of taking a regular `Matplotlib` plot and applying Tufte's principles of data-ink ratio and char junk to make it just a little bit better. I'm going to walk through all of the steps using the Jupiter notebooks and you're welcome to follow along. But if you want a bit more of a challenge, I'll be including in video quizzes along the way which prompts you to solve the problem before I address. This is good practice. The video will pause and you can do a quick Google to try and find an appropriate API for solving a specific issue. You can try it out in the system, then you can compare it to my solution right after. Let's get started.

We use a plot of data on the popularity of programming languages taken from stack overflow. Here there are five different languages, `Python`, `SQL`,  `Java`, `C++`, and `JavaScript`. We'll find their positions as a rank using NumPy as a range function. And here are the popularity values from stack overflow.

