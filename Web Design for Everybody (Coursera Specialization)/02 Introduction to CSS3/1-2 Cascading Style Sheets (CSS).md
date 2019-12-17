# 1-2 Cascading Style Sheets (CSS)

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/012.jpg' alt='012' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/013.jpg' alt='013' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/014.jpg' alt='014' width='500px' />

However, this still kind of breaks our rule of wanting to separate content from style.

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/015.jpg' alt='015' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/016.jpg' alt='016' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/017.jpg' alt='017' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/018.jpg' alt='018' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/019.jpg' alt='019' width='500px' />

So now the browser knows, everything in HTML, that is the content. Everything in `.css`, that is the layout.

```html
<link rel="stylesheet" href="style.css" />
```

`rel`: relationship

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/020.jpg' alt='020' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/021.jpg' alt='021' width='500px' />

**Recent file**: means it goes up into the head section, and it goes one, two, three, and it kind of looks at what order you listed them, and the last one you listed is the one that is going to have precedence.

```css
h1 {
  color: blue;
  font-family: Arial;
}
h1 {
  font-family: Times;
}
```

The last one will be used (**Times** in the above example).

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/022.jpg' alt='022' width='500px' />

```css
h1 {
  color: blue;
  font-family: Arial !important;
}
h1 {
  font-family: Times;
}
```

The first one will be used (**Arial** in the above example).

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/023.jpg' alt='023' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/024.jpg' alt='024' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/02%20Introduction%20to%20CSS3/Image/025.jpg' alt='025' width='500px' />
