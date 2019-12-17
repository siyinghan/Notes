# 1-6 Display and Visibility

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/051.jpg' alt='051' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/052.jpg' alt='052' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/053.jpg' alt='053' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/054.jpg' alt='054' width='500px' />

<br/>

**Example:**

---

```html
<body>
  <span>Span A</span>
  <span>Span B</span>
  <span>Span C</span>
  <hr />
  <div>Div A</div>
  <div>Div B</div>
  <div>Div C</div>
  <hr />
  <p>Paragraph A</p>
  <p>Paragraph B</p>
  <p>Paragraph C</p>
</body>
```

```css
span {
  height: 50px;
  width: 75px;
  background: #00ff00;
  /*display:Try block and inline block;*/
  /*float:;*/
}
div {
  height: 100px;
  width: 45px;
  background: #00ffff;
  /*display:;*/
  /*float:;*/
}
p {
  background: #ff00ff;
  width: 200px;
  height: 100px;
}
```

A simple file that is going to have three `span` elements, three `div` elements and three `paragraph` elements.

**Span** elements are inline, they're only going to take up as much space as they need.

The **divs** and the **paragraphs** are block, so they are going to take up more space.

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/086.png' alt='086' width='300px' />

Modify in browser:

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/087.png' alt='087' />

Modify **Span A**: `display:inline-block`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/088.png' alt='088' />

Modify **Span A**: `display:block`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/089.png' alt='089' />

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/056.jpg' alt='056' width='500px' />

<br/>

**Example:**

---

I am going to play with the spans up here and I am going to try floating them.

When you float something, you're basically saying put it as far over to the side as you can and the other elements are almost going to act as if they're not there but they are not going to overlap it.

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/090.png' alt='090' />

Modify **Span A**: `float:left`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/091.png' alt='091' />

Modify **Span A**: `float:right`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/092.png' alt='092' />

Modify **Div C**: `float:left`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/093.png' alt='093' />

Modify **Paragraph A**: `clear:both`

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/094.png' alt='094' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/095.png' alt='095' />

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/058.jpg' alt='058' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/059.jpg' alt='059' width='500px' />

**visible:** basically means if you are drawn a box, and there is a whole bunch of text inside of it, the text is actually going to go outside the box. So no matter what, the content is visible even if it goes outside the lines.

**hidden:** hidden does pretty much the opposite. If you have something inside this box and it is too big, it's gone. You can't see it. This is not a great idea, because it is going to cause problems if the user increases the font size on their browser.

**scroll:** it will give a horizontal and vertical scrollbar to the element. Even if it is just a paragraph, all of a sudden your paragraph has a scrollbar so people can see everything that is in it.

**auto:** it only adds scrollbars as needed, depending on how the person's viewing the site right now.

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/061.jpg' alt='061' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/062.jpg' alt='062' width='500px' />

You don't make an actual table with your HTML code, nor do you have the tag table. But you are telling your browser that you want to structure it as if it is a table.

So, you would make any type of containing element `display:table`. And then anything that you want to line up in nice columns, you would use `display:table-cell`.

<br/>

**Example:**

---

```css
div {
  width: 30%;
  background: #00ffff;
  height: 400px;
  display: inline-block;
  /*float:;*/
}
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/096.png' alt='096' width='500px' />

Each of the **divs** is now next to each other because we've told it we don't want them to be underneath each other.

Add: `float:left`

```css
div {
  width: 30%;
  background: #00ffff;
  height: 400px;
  display: inline-block;
  float: left;
}
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/097.png' alt='097' width='500px' />

But this would have some problems when zoom out the browser:

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/098.png' alt='098' width='350px' />

Add: `overflow:scoll`

```css
div {
  width: 30%;
  background: #00ffff;
  height: 400px;
  display: inline-block;
  float: left;
  over: scroll;
}
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/099.png' alt='099' width='350px' />

Display example for `table-cell` (may not supported by some browsers):

```css
body {
  display: table;
}
div {
  width: 30%;
  background: #00ffff;
  display: table-cell;
}
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/100.png' alt='100' width='500px' />

<br/>

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/064.jpg' alt='064' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/065.jpg' alt='065' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/066.jpg' alt='066' width='500px' />
